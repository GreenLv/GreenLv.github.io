---
title: "Protecting Context in Long-Running Agent Tasks: Introducing Context Guard"
date: 2026-08-06 13:52:08 +0800
permalink: /blogs/protecting-context-in-long-running-agent-tasks/
categories:
  - blogs
excerpt: "Context Guard keeps a private, verifiable ledger of active requirements and completion evidence so long-running Codex tasks can survive compaction without silently changing their contract."
header:
  teaser: blogs/context-guard-open-source-en.png
  teaser_alt: "A glowing workflow passes through guarded checkpoints in a cover illustration for Context Guard"
chinese_url: https://blog.csdn.net/LvGreat/article/details/163534498
author_profile: true
read_time: false
comments: false
share: false
related: false
---

<p class="blog-post-source">Also available as the <a href="{{ page.chinese_url }}">original Chinese article</a>.</p>

<figure class="blog-cover">
  <img src="{{ '/images/blogs/context-guard-open-source-en.png' | relative_url }}" alt="A glowing workflow passes through guarded checkpoints, illustrating context protection in long-running agent tasks">
  <figcaption>Context Guard protects the requirements and evidence that determine whether a long-running task is actually complete.</figcaption>
</figure>

<div class="blog-post-body" markdown="1">

AI agents are changing the basic unit of work. In the past, we often understood one model call as one question-and-answer exchange or one local code change. Today, agents such as Codex are beginning to take on tasks that last for hours, days, or even longer. They call tools, coordinate multiple agents, and receive new requirements from users while the work is already in progress. [OpenAI's introduction to the Codex app](https://openai.com/index/introducing-the-codex-app/) describes this shift from targeted edits to longer-running collaboration across design, implementation, delivery, and maintenance.

In these long-running, dynamic tasks, the emerging practice of loop engineering reflects a continuous way of working: the agent executes one round, inspects the result, receives revisions, and continues. [The Codex agent loop](https://openai.com/index/unrolling-the-codex-agent-loop/) coordinates the user, model, and tools throughout that process.

Once a task enters this loop, the main correctness problem changes. It is no longer enough to ask how well the model performed in the latest turn. We also need to ensure two things:

1. **The task contract remains stable.** Goals, constraints, acceptance criteria, and later revisions confirmed by the user must not be silently rewritten after context compaction or task recovery.
2. **Completion claims remain traceable to evidence.** Every active requirement should have corresponding successful evidence. Unverified, unauthorized, or unfinished work must not be presented as complete.

The goal is not to make the agent remember the entire conversation, nor to build another planning and scheduling system. The goal is to preserve the small amount of state that determines whether the result is correct: which requirements are currently active, which have been verified, and which still require work.

To address this problem, I built and open-sourced [Context Guard](https://github.com/GreenLv/codex-context-guard). It is a local correctness sidecar for Codex that uses lifecycle hooks to maintain a private, verifiable ledger of requirements and evidence.

A familiar travel-planning example shows what Context Guard does. A user begins with a simple request:

> I want to travel from Wuhan to Beijing next week for seven days. Please plan the trip for me.

After Codex starts checking transportation, hotels, and attractions, the user adds more details: the trip is for the user and their mother; the mother has knee problems and cannot walk too much each day; both directions must use high-speed rail; the total budget for two people must stay below RMB 8,000; Wednesday from 15:00 to 19:00 is reserved for meeting a friend in Haidian; they want to visit the Forbidden City; and every reservation-dependent item must be checked against an official source before it can be described as booked.

As Codex compares train services, hotels, reservation rules, and daily routes, the conversation grows. If context compaction happens at this point, the summary may still remember that the task is a seven-day trip from Wuhan to Beijing, yet omit the mother's walking constraint or schedule another attraction on Wednesday afternoon. It may also find an outdated travel guide and treat unverified opening hours or ticket availability as confirmed.

The model has not forgotten the whole task. It still remembers the destination, but it has lost a few constraints that determine whether the plan can actually be used.

> Current release: [v0.4.9](https://github.com/GreenLv/codex-context-guard/releases/tag/v0.4.9)

## 1. What problem does it solve?

For the Beijing trip, Context Guard focuses on the task contract that develops over time rather than the complete conversation:

```text
[ ] Seven-day round trip from Wuhan to Beijing next week
[ ] Two travelers, the user and their mother; total budget below RMB 8,000
[ ] High-speed rail in both directions; no flights
[ ] The mother has knee problems: limit walking and avoid consecutive strenuous days
[ ] Meet a friend in Haidian on Wednesday from 15:00 to 19:00; this slot is fixed
[ ] Visit the Forbidden City
[ ] Verify reservations, opening hours, prices, and transportation with current official sources
[ ] Mark every unverified or unbooked item as pending confirmation
```

Codex still performs the searches, compares alternatives, builds the itinerary, calculates the budget, and coordinates subagents. Context Guard records only the information directly related to correctness: the user's requirements, later additions or revisions, usable evidence returned by tools, and any remaining work.

After `/compact` or task recovery, the checklist returns to the context. Suppose Codex has created a seven-day itinerary and calculated the budget, but Wednesday afternoon still contains an attraction, or the requirement to verify the Forbidden City reservation against an official source has no successful evidence. Context Guard will not accept the conclusion that the trip has been fully planned. Codex must resolve the schedule conflict and clearly mark any unverified item as pending.

The completion evidence is also straightforward. The seven-day schedule must satisfy the activity and time constraints for every day. The budget total must stay within the limit. Train services, opening hours, and reservation requirements need sources and query dates. An unfinished reservation must never be presented as successful.

Context Guard therefore does not try to make summaries longer. It prevents the task contract from being quietly rewritten inside a summary.

## 2. How does it work with Codex?

Context Guard does not reimplement Codex's native Plan, Goal, compaction, subagents, worktrees, or memories. Their responsibilities can be summarized in six steps:

```text
The user provides requirements and acceptance criteria
                         |
                         v
Context Guard stores a private checklist and revision relationships
                         |
                         v
Codex executes the task, calls tools, and collaborates normally
                         |
                         v
Compaction or recovery reinjects the active task boundaries
                         |
                         v
Each active requirement is checked for successful evidence
                         |
                         v
Complete when all requirements pass; otherwise continue or await a decision
```

Three parts of this design matter most to me.

### 2.1 Later revisions do not erase history

Long tasks rarely keep the same requirements from beginning to end. A user may add a constraint or explicitly replace an older requirement with a new one. Context Guard records that revision relationship instead of directly overwriting the old record.

After compaction and recovery, it can therefore answer two different questions: what was originally requested, and which requirements are active now. When a negation or replacement is ambiguous, the plugin keeps the original requirement and waits for confirmation rather than guessing.

### 2.2 Finding information does not mean satisfying a requirement

Successfully opening a web page proves only that the search ran. It does not prove that the page is official, that its information is current, or that a reservation has been completed. A budget calculation that exits successfully does not prove that local transportation and other necessary expenses are included.

Context Guard prefers structured state, exit codes, and explicit completion markers. Ambiguous output is recorded as `unknown` and cannot directly support a completion claim. In the travel example, the itinerary, budget summary, and dated official sources are separate pieces of evidence. A generic search result cannot automatically replace them.

This does not mean the plugin can understand the full semantics of every piece of evidence. It can check whether each active requirement is bound to successful evidence, but it cannot prove that the evidence is logically sufficient. Codex and the user still own the design of the final validation.

### 2.3 Subagents have explicit provenance but cannot change the root task

In a multi-agent task, a subagent receives a bounded delegation, not new authorization from the user. Context Guard records the agent's start, finish, result, and provenance, but a subagent cannot create, cancel, or replace a root-task requirement.

This prevents a common source of confusion: completing a local subtask does not complete the whole task, and a subagent's suggestion does not mean that the user changed the original requirements.

## 3. Why keep the state private?

A requirements ledger may contain unpublished travel details, code paths, document constraints, or other task context. It should not enter the project's Git history.

The public Context Guard repository contains only the plugin code, hooks, schema, documentation, and tests. Runtime data is written to Codex-managed `PLUGIN_DATA` and remains local by default. The plugin does not store chain-of-thought, copy the complete transcript, or initiate network requests.

Users can explicitly run `context-guard export` or `rollover` to create a redacted handoff or a bounded successor pack. The export process omits common credentials, authorization headers, URL query parameters, original prompt files, and private plugin paths. Automatic redaction is not a substitute for review, however. Any handoff intended for sharing should still be inspected before it leaves the machine.

## 4. Installation and first validation

The project requires Python 3.10 or later. The currently validated minimum baseline for the Codex CLI is `0.146.0`.

On macOS and Linux:

```shell
git clone https://github.com/GreenLv/codex-context-guard.git
cd codex-context-guard
python3 scripts/manage_plugin.py --apply
```

On Windows:

```powershell
py -3.10 scripts\manage_plugin.py --apply
```

After installation, start a new Codex task and inspect the eight hook definitions under `/hooks`. Trust them only after confirming that their commands match the repository contents; plugin installation does not bypass hook trust automatically.

Then enter:

```text
$context-guard
```

And run:

```text
context-guard status
```

To validate the complete recovery path, create a task with several requirements and prohibited actions, run `/compact`, and then verify that continuation restores the same active requirements.

For complete installation, upgrade, and removal instructions, see the project's [English README](https://github.com/GreenLv/codex-context-guard/blob/main/README.md).

## 5. Which tasks benefit from it?

Context Guard is most useful for tasks that last for a while, may receive revised requirements, and need tool results to demonstrate completion. Examples include:

- planning a complex trip while adding budget, companion, fixed-time, or transportation constraints;
- writing or editing a document while preserving a template, terminology, numbers, and protected scope;
- refactoring code while maintaining existing interfaces, data formats, or compatibility behavior;
- running experiments or processing files in batches without presenting partial success as complete;
- coordinating multiple subagents while distinguishing root-task authorization from bounded delegation;
- handing a task to a successor without copying the complete conversation.

For a small change completed within a single conversation, enabling the full protection workflow is usually unnecessary.

## 6. Current validation status and boundaries

Version 0.4.9 has passed source-to-install-cache parity checks, regression tests, installation lifecycle tests, trust checks for all eight hook types, and real manual requirement recovery after `/compact` on macOS and Windows. The public repository's Ubuntu, macOS, and Windows CI matrix also passes. Linux validation remains bounded to CI and isolated lifecycle tests.

Context Guard is not a semantic correctness prover, security sandbox, cloud synchronization service, complete conversation backup, or second agent scheduler. It protects the task contract, revision relationships, a limited plan mirror, agent results with explicit provenance, and completion evidence.

I want the project to remain focused. The immediate priorities are preventing silent requirement loss, making revisions traceable, refusing unsupported completion claims, and keeping private state out of Git. Reproducible problems, rather than feature accumulation, should drive future work.

## 7. Summary

The central idea behind Context Guard is simple:

> Do not infer the task contract from a compacted summary. Maintain a private, verifiable ledger of requirements and evidence locally, restore the active requirements after compaction, and then decide whether the task is complete.

If you use Codex for long-running work and have seen requirements drift after compaction, a task stop after only partial validation, or unclear authorization boundaries in multi-agent collaboration, you are welcome to try it:

**GitHub: [GreenLv/codex-context-guard](https://github.com/GreenLv/codex-context-guard)**<br>
**Release: [Context Guard v0.4.9](https://github.com/GreenLv/codex-context-guard/releases/tag/v0.4.9)**

If the project is useful to you, consider starring it, opening an issue, or sharing a reproducible context failure from a long-running task. Reproducible failures are a better basis for the roadmap than a longer feature list.

</div>
