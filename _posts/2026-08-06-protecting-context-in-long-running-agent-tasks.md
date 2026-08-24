---
title: "Why Can't Agents Remember Your Requirements Even with a 1M-Token Context Window?"
date: 2026-08-06 13:52:08 +0800
permalink: /blogs/protecting-context-in-long-running-agent-tasks/
categories:
  - blogs
excerpt: "Why a 1M-token context window still does not keep an agent's requirements active—and how Context Guard preserves the task contract and completion evidence through long-running Codex work."
header:
  teaser: blogs/context-guard-open-source-en.webp
  teaser_alt: "A guarded context path illustrating why a larger context window does not by itself preserve an agent's requirements"
chinese_url: https://blog.csdn.net/LvGreat/article/details/163534498
author_profile: true
read_time: false
comments: false
share: false
related: false
---

<p class="blog-post-source">Also available as the <a href="{{ page.chinese_url }}">original Chinese article</a>.</p>

<figure class="blog-cover">
  <img src="{{ '/images/blogs/context-guard-open-source-en.webp' | relative_url }}" alt="A guarded context path illustrating why a larger context window does not by itself preserve an agent's requirements">
  <figcaption>A 1M-token context window can carry more material, but it does not automatically preserve the requirements that determine whether a long-running task is complete.</figcaption>
</figure>

<div class="blog-post-body" markdown="1">

You may have seen this happen.

At the start, you tell an agent: “Do not change the existing format.” “Do not invent missing data.” “Keep the total under $2,000.” It follows those instructions for several rounds and repeatedly confirms that it understands them.

Then the task keeps running. Tokens keep burning, time disappears into searches, tool calls, and revisions, and you wait for a result that will finally justify the effort. What comes back is nowhere near what you expected: the format has changed, missing data has been confidently invented, or the budget cap that mattered most has vanished. The result is unusable, and you find yourself furiously typing into the chat box: “Didn't I say this at the very beginning?”

The most frustrating part is that the agent has not forgotten the entire task. It still knows what you asked it to produce and can often repeat most of the background. It has lost one requirement that determines whether the result is usable.

A result like this is easy to blame on the model simply not being smart enough. But that diagnosis is incomplete. Model capability certainly affects performance, yet this exposes a different failure mode: understanding a requirement once does not guarantee that the requirement will continue to govern every later action. Even a capable model still needs an explicit way to maintain active requirements, later revisions, and completion evidence throughout a long-running task.

Users of [Claude Code](https://github.com/anthropics/claude-code/issues/32659) and [Cursor](https://forum.cursor.com/t/critical-rules-do-not-survive-context-compression-events/157249) have reported the same pattern: a constraint is acknowledged early, then stops reliably shaping later actions as the session grows or is compressed. These reports do not prove a single cause. They describe the same practical failure: a requirement that has been present all along, and can still be restated accurately, ultimately fails to reliably constrain the agent's actions and final deliverable.

It is tempting to reduce this to a context-capacity problem. Some models now offer windows on the order of one million tokens. [OpenAI lists GPT-5.6 Sol with a 1,050,000-token context window](https://developers.openai.com/api/docs/models/gpt-5.6-sol). That is a meaningful improvement: an agent can retain more code, tool output, and conversation history before older material has to be compacted. But a larger container does not guarantee that every important instruction remains active.

The harder question is not only how much an agent can see. It is whether the agent can keep track of which requirements still apply, which revision superseded an earlier instruction, and what evidence is needed before the task can honestly be called complete.

## 1. What a 1M-token window solves—and what it does not

### 1.1 A context window is a capacity limit, not a priority list

A context window answers one question: how much input can participate in a model call. It does not assign permanent priority to a sentence such as “never modify the appendix,” or turn that sentence into an invariant across dozens of later actions.

A long-running task can contain the original request, later corrections, tool results, error logs, source material, and several drafts at once. Even when all of it still fits, the model has to decide what matters before every action. In multi-document question answering and key-value retrieval experiments, [*Lost in the Middle*](https://arxiv.org/abs/2307.03172) found that performance was generally strongest when relevant information appeared near the beginning or end and degraded when it appeared in the middle, including for models explicitly designed for long contexts. The information is present, but presence alone does not ensure reliable use.

This distinction becomes more important as the window grows. One million tokens is not a curated requirements document. It is a very large workspace in which a few decisive constraints can be surrounded by a much larger volume of process material. Adding capacity does not perform the work of selecting and maintaining task state.

### 1.2 Following a requirement is harder than retrieving a sentence

Many long-context evaluations use a single-needle task: place one fact inside a large input and ask the model to retrieve it. Real requirements rarely look like one isolated needle. They are distributed across turns and often contain conditions, exceptions, and negation:

- “Do not change the table format, but update these three columns.”
- “Keep the total under $2,000, including local transportation.”
- “Do not schedule anything on Wednesday afternoon,” rather than merely remembering that a meeting exists.
- “Describe a reservation as booked only after checking a current official source.”

The agent must retrieve these statements, combine them, map them to the current action, and check the result before delivery. That is a multi-step constraint problem, not a lookup.

[A recent study of five models with advertised million-token windows](https://arxiv.org/abs/2605.02173) makes the distinction visible. The strongest models still reached 100% on single-needle retrieval at 1M tokens, but every model declined when the task required a three-hop chain across different parts of the context. Some remained above 80% through 512K and degraded modestly at 1M; others fell sharply between 512K and 1M. The corpus was classical Chinese, not agent instructions, but the result supports a narrower point that applies here: nominal window length does not measure how reliably a model can combine everything inside that window.

### 1.3 Conversation history is not current task state

Real tasks also change. A user may begin with “keep it under $2,500” and later revise the limit to $2,000. They may add a fixed appointment, remove an earlier deliverable, or clarify that an instruction applies to only one file.

The full conversation now contains both the old and new versions. The agent still has to determine which requirement is active, which one was superseded, where a constraint applies, and which conflict needs clarification. Conversation history records what was said over time. Task state represents what should happen now. They are not the same data structure.

More history can therefore preserve a conflict without resolving it. Unless revisions are represented explicitly, the agent may continue following the old instruction or treat a local correction as a global replacement.

### 1.4 Remembering a requirement is not satisfying it

Even correct retrieval does not complete the task. An agent may remember that it must check an official source and successfully open a page. That proves the lookup ran. It does not prove that the source is official, that the information is current, or that a reservation was completed. The agent may also produce a seven-day itinerary and a budget total while still placing an activity inside a fixed appointment.

A long task therefore has at least three kinds of state: active requirements, work already performed, and evidence that the requirements were satisfied. Conversation history records much of what happened, but it does not automatically establish a requirement-to-evidence relationship. Without that relationship, “I ran a search,” “the command exited,” or “the file exists” can be mistaken for proof that the full requirement passed.

### 1.5 Compaction is not the root cause, but it amplifies the problem

One million tokens is still finite. As a task grows, an agent may compact earlier material or resume from a summary. Compaction is lossy by design. A summary tends to retain the main storyline while dropping a negative constraint, an acceptance condition, an unresolved conflict, or a recent revision. “Plan a seven-day New York trip” survives; “limit walking” and “do not call an unverified reservation booked” may not.

Public Codex issues show two concrete versions of this failure. In [issue #19910](https://github.com/openai/codex/issues/19910), mid-turn compaction reportedly failed to carry forward the completion-audit requirement attached to the active goal, and local verification was treated as whole-goal completion. In [issue #35226](https://github.com/openai/codex/issues/35226), the agent retained the broad project objective but lost execution progress, repeatedly reread the same files, and restarted the same analysis. These are two public cases, not evidence of how frequently the problem occurs. They do illustrate the same distinction: preserving the main objective is not the same as preserving task state.

A larger window delays compaction and lets the agent access more original material. Using the entire window also costs more. Under [GPT-5.6 Sol's current API pricing](https://developers.openai.com/api/docs/models/gpt-5.6-sol), once the input exceeds 272K tokens, the entire request—not only the excess—is charged at twice the input rate and 1.5 times the output rate. Long context is better treated as a resource than as a target to fill by default.

A 1M-token window therefore relieves capacity pressure without automatically solving priority, revision, progress, or acceptance. The state that needs the strongest protection is usually much smaller than the conversation: the active requirements, their revision relationships, and the evidence needed to close them. That is the design premise of Context Guard.

## 2. What Context Guard protects

<figure class="blog-diagram">
  <img src="{{ '/images/blogs/context-guard-body-leading-en.jpg' | relative_url }}" alt="A large context stream carries task records while Context Guard checkpoints protect critical requirements from drifting away">
  <figcaption>Context Guard protects the requirements that determine whether a long-running task can be completed honestly.</figcaption>
</figure>

[Context Guard](https://github.com/GreenLv/codex-context-guard) is a local correctness layer I built for Codex. It does not store the whole conversation or try to replace model memory. It uses [lifecycle hooks](https://github.com/GreenLv/codex-context-guard/blob/main/docs/ARCHITECTURE.md) to maintain a private, verifiable ledger of requirements and evidence.

Consider an everyday planning task. You begin with a simple request:

> I am taking my mother from Boston to New York next week for seven days. Please plan the trip.

After the assistant starts comparing trains, hotels, and attractions, you add the details that make the plan usable: your mother has knee pain and cannot walk long distances; both directions must be by train, with no flights; the total budget for two must stay below $2,000; Wednesday from 3:00 p.m. to 7:00 p.m. is reserved for meeting a friend in Queens; you want to visit the Statue of Liberty; and anything that depends on a reservation must be checked against a current official source before it can be described as booked.

As the agent compares schedules, hotels, reservation rules, and daily routes, the conversation grows. After compaction, the summary may still remember “a seven-day New York trip from Boston” while dropping the walking constraint or scheduling an attraction on Wednesday afternoon. It may also rely on an outdated travel guide and describe unverified hours or ticket availability as confirmed.

The whole task has not disappeared. A few conditions that determine whether the plan can be used have.

Context Guard focuses on the contract that develops over time:

```text
[ ] Seven-day round trip from Boston to New York next week
[ ] Two travelers: the user and their mother; total budget below $2,000
[ ] Train in both directions; no flights
[ ] The mother has knee pain: limit walking and avoid strenuous days back to back
[ ] Meet a friend in Queens on Wednesday, 3:00–7:00 p.m.; keep this slot free
[ ] Include a visit to the Statue of Liberty
[ ] Verify reservations, opening hours, prices, and transportation with current official sources
[ ] Mark every unverified or unbooked item as pending confirmation
```

Codex still performs the searches, compares options, builds the itinerary, calculates the budget, and coordinates subagents. Context Guard records only the information tied directly to correctness: the user's requirements, later additions or revisions, usable evidence returned by tools, and remaining work.

After `/compact` or task recovery, the checklist returns to context. If no check has established that the Wednesday time slot remains free, or the official-source check for Statue of Liberty tickets has no corresponding successful evidence, Context Guard keeps those requirements open instead of accepting that the trip is fully planned merely because an itinerary was generated. Codex, a checking tool, or the user must still determine whether the itinerary actually satisfies the walking and scheduling constraints.

The point is not to make the summary longer. It is to stop the task contract from being quietly rewritten inside the summary.

## 3. How it works

Context Guard does not replace Codex's native Plan, Goal, compaction, or subagents. It maintains a smaller correctness state: which requirements are active, how they were revised, which evidence succeeded, and what remains unfinished.

<figure class="blog-diagram">
  <img src="{{ '/images/blogs/context-guard-state-flow-en.png' | relative_url }}" alt="Context Guard carries the task boundary into work and evidence collection, then decides whether to finish, continue, or pause safely">
  <figcaption>Context Guard carries the task boundary into work and evidence collection, then separates finishing, continuing, and pausing safely.</figcaption>
</figure>

It has four main jobs:

- **Preserve active requirements.** After compaction or recovery, it restores the current task contract rather than the full transcript.
- **Track revisions.** A new instruction can add to or replace an older one. If the replacement is ambiguous, the original requirement remains active until the conflict is resolved.
- **Constrain completion with evidence.** Opening a page or running a command proves that an action occurred. Evidence must still match the right requirement, subject, and scope; ambiguous output cannot close the task.
- **Separate delegated work from root authority.** A subagent can finish a bounded assignment, but it cannot rewrite the user's root requirements, and local success does not become whole-task success.

Context Guard can also record an execution contract. Once adopted, it records task sources by role:

| Source | What it decides | Boundary |
| --- | --- | --- |
| User instructions | Task goals and write authority | Cannot be expanded by other sources |
| `AGENTS.md` and selected Skills | Workflow and safety constraints | Conflicts resolve in favor of user requirements |
| Codex Plan | Revisable execution steps | Codex may revise it, but the completion gate does not depend on it |
| Tool, file, image, and public-readback results | Which facts are established | Can correct factual assumptions, but cannot expand authority |

Everything stays inside Codex's own permission, sandbox, and Hook-trust boundaries.

The contract is dormant by default: only the user who started the root task can adopt it explicitly (`context-guard adopt <project-relative-json>`), after which Context Guard records, restores, and checks it at completion. If an adopted Skill or the Codex Plan later changes, the old binding is marked for review instead of being followed silently. Context Guard does not rewrite Codex Plan, intercept tools, publish automatically, or grant new authority.

To avoid becoming noisy itself, Context Guard does not trigger the completion gate on every occurrence of “complete.” Questions, quotations, hypotheticals, and explicit negations are not treated as completion claims, while whole-task statements such as “all requirements are complete” still require supporting evidence.

When the next step requires user confirmation, an external system, or an explicit deferral, Context Guard keeps the unfinished item open rather than confusing “safe to stop now” with “the whole task is complete.” Under the project's [privacy and retention design](https://github.com/GreenLv/codex-context-guard/blob/main/docs/PRIVACY.md), its runtime ledger stays local by default, outside the project Git history, and does not copy the full transcript.

## 4. Installation and fit

Under the current [published requirements](https://github.com/GreenLv/codex-context-guard/blob/main/README.md#install), the project requires Python 3.10 or later, and the validated minimum baseline for the Codex CLI is `0.146.0`.

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

After installation, use the following controls in a Codex conversation to activate Context Guard, inspect its status, or run diagnostics:

```text
$context-guard
context-guard status
context-guard diagnose
```

Context Guard is most useful when a task runs for a while, receives revised requirements, and needs tool results to demonstrate completion. Examples include:

- planning a complex trip while adding budget, companion, fixed-time, or transportation constraints;
- writing or editing a document while preserving a template, terminology, numbers, and protected scope;
- refactoring code while maintaining existing interfaces, data formats, or compatibility behavior;
- running experiments or processing files in batches without presenting partial success as complete;
- coordinating multiple subagents while distinguishing root-task authorization from bounded delegation.

For a small change completed in one conversation, the full workflow is usually unnecessary. In the project's [published sample of five completed, tool-heavy desktop tasks](https://github.com/GreenLv/codex-context-guard/blob/main/README.md#observed-token-overhead) using 0.6.1, the observed additional token share ranged from about 0.2% to 2.1%, with a weighted value of about 1.5%. This is a small-sample order of magnitude, not a guarantee for every workload.

The project has scoped native acceptance on macOS and Windows. Linux is currently claimed only for source CI. Context Guard is not a semantic correctness prover, security sandbox, cloud sync service, or complete conversation backup. See the [English README](https://github.com/GreenLv/codex-context-guard/blob/main/README.md), [Compatibility](https://github.com/GreenLv/codex-context-guard/blob/main/docs/COMPATIBILITY.md), and [Local release acceptance](https://github.com/GreenLv/codex-context-guard/blob/main/docs/LOCAL_ACCEPTANCE.md) for the full installation and evidence boundaries.

## 5. Summary

The central idea behind Context Guard is simple:

> Do not infer the task contract from a compacted summary. Keep a private, verifiable ledger of active requirements and completion evidence locally, restore it after compaction, and then decide whether the task is complete.

A 1M-token context window lets an agent carry more material. “Can carry more” and “will not lose a critical requirement” are still different claims. In a long-running task, the information that needs the strongest protection is often not the whole conversation. It is the small set of constraints that determine whether the result can be delivered, together with the evidence that those constraints were met.

If you use Codex for long-running work and have seen requirements drift after compaction, a task stop after partial validation, or unclear authorization boundaries in multi-agent collaboration, you are welcome to try it:

**GitHub: [GreenLv/codex-context-guard](https://github.com/GreenLv/codex-context-guard)**

**Latest release: [GitHub Releases](https://github.com/GreenLv/codex-context-guard/releases/latest)**

If the project is useful to you, consider starring it, opening an issue, or sharing a reproducible context failure.

## References

- [GPT-5.6 Sol model page](https://developers.openai.com/api/docs/models/gpt-5.6-sol)
- [Lost in the Middle: How Language Models Use Long Contexts](https://arxiv.org/abs/2307.03172)
- [Codex issue #19910: active goal and audit requirements can be lost after compaction](https://github.com/openai/codex/issues/19910)
- [Codex issue #35226: auto-compaction can lose progress and repeat file reads](https://github.com/openai/codex/issues/35226)
- [Retrieval and Multi-Hop Reasoning in 1M-Token Context Windows](https://arxiv.org/abs/2605.02173)
- [Claude Code issue #32659: context amnesia in long sessions — constraints silently dropped as context grows](https://github.com/anthropics/claude-code/issues/32659)
- [Cursor forum: “Rules” do not survive context compression events](https://forum.cursor.com/t/critical-rules-do-not-survive-context-compression-events/157249)

</div>
