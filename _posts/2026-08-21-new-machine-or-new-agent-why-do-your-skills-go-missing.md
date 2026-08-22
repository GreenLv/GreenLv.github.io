---
title: "New Machine or New Agent—Why Do Your Skills Go Missing?"
date: 2026-08-21 20:12:32 +0800
permalink: /blogs/new-machine-or-new-agent-why-do-your-skills-go-missing/
categories:
  - blogs
excerpt: "SkillFerry turns one versioned workspace into Codex, Claude Code, and DeepSeek Harness configurations while grading portability, keeping secrets local, and surfacing conflicts instead of silently overwriting edits."
header:
  teaser: blogs/skillferry-portable-agent-workflows-card-en.webp
  teaser_alt: "A digital ferry carries portable agent capabilities while credential lockboxes remain on each machine"
og_image: blogs/skillferry-portable-agent-workflows-cover-en.webp
author_profile: true
read_time: false
comments: false
share: false
related: false
---

<div class="blog-post-body" markdown="1">

<figure class="blog-diagram blog-leading">
  <img src="{{ '/images/blogs/skillferry-portable-agent-workflows-en.webp' | relative_url }}" alt="A digital ferry carries skill, rules, and MCP modules between agent environments while credential lockboxes remain on each machine">
  <figcaption>The article's leading visual: a portable workspace carries capabilities between agents without copying credentials.</figcaption>
</figure>

You may know the frustration. The agent on your work computer is finally set up the way you want it: Codex knows which skills to load and which rules to follow, and your usual MCP tools are already connected. Then you get home and switch computers—or decide to try Claude Code or DeepSeek Harness (DSH). Suddenly, none of that familiar setup is there.

So you install the skills again, copy the rules, reconnect MCP, and tune each agent one setting at a time. Copying the old computer's entire configuration sounds quicker, but it can also carry sign-in details, past conversations, and paths that only make sense on that machine. Even then, the same configuration does not work unchanged in Codex, Claude Code, and DSH—and it may overwrite changes you already made on the new computer.

What you really want to carry is the familiar way your agents work: the same skills should be discovered, the same rules should apply, and the same MCP tools should be reconnectable.

That's why I built [SkillFerry](https://github.com/GreenLv/skillferry):

> Reproduce your agent capabilities so the skills and MCP connections you have built over time can be reused across platforms and agents.

## The formats are open. The install story isn't.

[Agent Skills](https://agentskills.io/home) provides a shared way to save how an agent performs a task. MCP gives different agents a common way to connect to outside tools. With those foundations in place, reusing capabilities across Codex, Claude Code, and DSH—or carrying them to a new machine—should be much easier.

But saving something in a shared format is not the same as making it work in every agent. Codex, Claude Code, and DSH still store skills, read rules, and connect MCP servers in different ways. The same skill may work immediately in one agent, need conversion in another, lose part of its behavior, or have to be rebuilt by hand. Add the differences between macOS, Windows, and Linux, and the problem quickly grows again.

This is not a hypothetical. The MCP community has filed client-config portability as an open standardization problem ([MCP IG #2761](https://github.com/modelcontextprotocol/modelcontextprotocol/discussions/2761)), and users have reported skills failing to follow them to a new machine in both the Claude Code and Codex trackers ([Claude Code #36693](https://github.com/anthropics/claude-code/issues/36693), [Codex #26691](https://github.com/openai/codex/issues/26691)). Those issues establish that the problem exists; they do not establish its prevalence or priority rank.

So the real question is not "how do I copy this to more directories." It's: what is the source of truth across tools and machines? What can be translated automatically, and what meaning is lost? What must never leave the machine? And how do you apply changes without stomping on existing local work?

## One workspace; every agent is a render target

SkillFerry's approach is plain: skills, global rules, and secret-free MCP templates live in one reviewable, Git-friendly workspace. Codex, Claude Code, and DSH are all render targets. No "primary agent" is in charge; the workspace is the source of truth.

Say the workspace holds a `release-checklist` skill, a set of global release rules, and a GitHub MCP template. The token never enters the workspace—the template only stores a reference like `secret:env/GITHUB_PERSONAL_ACCESS_TOKEN`. Run `plan` and it tells you, line by line, what each target will receive:

```text
SKILL release-checklist
  codex   native
  claude  native
  dsh     native

MCP github
  codex   translated   secret resolved from local env
  claude  translated   secret resolved from local env
  dsh     translated   inserted as dsh-mcp-client entries
```

In plain English: `native` means it lands in the target's own format with nothing lost. `translated` means it works after a conversion—like the three MCP entries above. `degraded` means it runs with known limits. `manual` means you get instructions and a step to do yourself. `unsupported` means the target has no equivalent at all. Every grade traces back to capability evidence, not a generic "compatible" checkbox.

So a new machine and a new agent are the same job: keep one copy of the skills. New machine? Pull it down and set it up. New agent? Same copy, installed in that tool's own format.

<figure class="blog-diagram">
  <picture>
    <source media="(max-width: 700px)" srcset="{{ '/images/blogs/skillferry-portability-flow-en-mobile.svg' | relative_url }}">
    <img src="{{ '/images/blogs/skillferry-portability-flow-en.svg' | relative_url }}" alt="SkillFerry turns a target-neutral workspace into a portability plan and native Codex, Claude Code, and DeepSeek Harness configurations while secret values resolve only on the local machine">
  </picture>
  <figcaption>SkillFerry makes portability grades and local-only secret resolution visible before configuration is applied.</figcaption>
</figure>

## Four boundaries behind what it will promise

**Capabilities travel; state stays.** Skills, rules, and MCP server definitions are a reproducible way of working. Tokens, login state, sessions, caches, and generated memory are identity or runtime state. SkillFerry manages only the explicitly declared parts of the former, and it never treats a whole `~/.codex` or `~/.claude` directory as a sync unit. That is also why it is not a dotfiles synchronizer, a provider switcher, or an agent orchestration system.

**A file landing is not a feature loading.** Putting a file in a destination directory proves only that the file exists, not that the target loads it with equivalent semantics. The current release renders stdio MCP servers into all three native shapes; HTTP/SSE MCP stays `manual`, and plugins or extensions can be declared but are never auto-installed. Knowing which step still needs a human beats an undifferentiated "sync succeeded."

**Sync capabilities, not credentials.** The workspace schema rejects literal secrets in MCP environments and accepts only references like `secret:env/...` or `secret:file/...`. Real values resolve locally at `apply` time, never into JSON reports, and are never expanded into the shareable copy created by `skillferry export <destination>`. SkillFerry is not a secret manager—OS and directory permissions still protect local values. It just stops credentials from being mistaken for shareable capability definitions.

**Your hand edits are not drift to clean up.** An ownership ledger records the paths and hashes SkillFerry last wrote. If a managed file has since been edited by hand, the next `plan` or `apply` reports a conflict (exit code 3) instead of overwriting it. You choose `adopt`, `overwrite`, or `keep-local`; files are backed up before writes, and a failed multi-file group rolls back what it already wrote.

## import → plan → apply → doctor

The main loop has four steps, and each one lets you look before you leap:

- `import` pulls portable assets out of an existing Codex or Claude Code environment and turns sensitive values into references;
- `plan` shows target paths, grades, origins, and conflicts—and writes nothing;
- `apply` writes only the paths it declares as managed;
- `doctor` uses exit codes 0/1/2/3 to separate in sync, error, safe drift, and a conflict that needs a human decision.

After one loop you can say exactly what moved, which target translated it, which values stayed local, and whether drift remains.

## Try it

SkillFerry is on [PyPI](https://pypi.org/project/skillferry/) and needs Python 3.11 or newer:

```shell
pipx install skillferry
skillferry init my-workspace
cd my-workspace

skillferry plan
skillferry apply
skillferry doctor
```

Already on Codex? Start with `import --from codex` and review the generated workspace instead of writing the schema by hand. Coming from [codex-profile-sync](https://github.com/GreenLv/codex-profile-sync)? There is a `migrate --from codex-profile-sync` command for that. The repo also ships a runnable starter workspace and two seed skills, so you can inspect all three target renderings in an isolated directory before committing to anything.

## Who it's for—and where it draws the line

If you use one agent on one machine and have not accumulated skills or rules yet, manual setup may still be simpler.

SkillFerry earns its keep when:

- you move between Codex, Claude Code, or DSH;
- you want one capability baseline across macOS, Windows, and Linux;
- you treat skills and rules as engineering assets that deserve versioning;
- you want a preview before applying, and explicit disclosure when semantics are lost;
- you want Git to carry shareable definitions without credentials or runtime state.

It deliberately skips GUI, SSH targets, a team layer, session or memory sync, provider management, and lossless conversion of arbitrary plugins. macOS and Windows each have independent native acceptance records—the Windows machine had no Claude Code installed, so it verified the rendered config shape without starting the process. CI is a separate automated gate, not native acceptance. The full boundary is in the [portability contract](https://github.com/GreenLv/skillferry/blob/main/docs/PORTABILITY_CONTRACT.md), the [capability evidence matrix](https://github.com/GreenLv/skillferry/blob/main/docs/AGENT_MATRIX.md), and the [documentation and acceptance records](https://github.com/GreenLv/skillferry/blob/main/docs/README.md).

## Let your way of working follow you

Open formats solved content reuse. The directory differences, config shapes, platform quirks, secret boundaries, and local edits still need someone to handle them honestly. SkillFerry's choice is to put those differences on the table instead of hiding them behind "sync complete."

If you are re-installing skills, rewriting rules, or maintaining several copies of the same MCP config, run one isolated `import → plan` first. See which capabilities travel natively, which need translation, and which should never leave the local machine.

Repository: [GreenLv/skillferry](https://github.com/GreenLv/skillferry)<br>
Latest release: [GitHub Releases](https://github.com/GreenLv/skillferry/releases/latest)<br>
Install: [PyPI](https://pypi.org/project/skillferry/)

</div>
