---
title: "New Machine or New Agent—Why Do Your Skills Go Missing?"
date: 2026-08-21 20:12:32 +0800
permalink: /blogs/new-machine-or-new-agent-why-do-your-skills-go-missing/
categories:
  - blogs
excerpt: "SkillFerry turns one versioned workspace into Codex, Claude Code, and DeepSeek Harness configurations while grading portability, keeping secrets local, and surfacing conflicts instead of silently overwriting edits."
chinese_url: https://blog.csdn.net/LvGreat/article/details/163969269
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

So you install the skills again, copy the rules, reconnect MCP, and tune each agent one setting at a time. Some people copy the old computer's entire configuration directory. That can bring along sign-in details, past conversations, and paths that make sense only on the old machine. Codex, Claude Code, and DSH also use different configuration shapes, so some copied settings fail to load while others overwrite work already done on the new computer.

What you really want to carry is the familiar way your agents work: the same skills should be discovered, the same rules should apply, and the same MCP tools should be reconnectable.

That's why I built [SkillFerry](https://github.com/GreenLv/skillferry):

> Reproduce your agent capabilities so the skills and MCP connections you have built over time can be reused across platforms and agents.

## The formats are open. The install story isn't.

[Agent Skills](https://agentskills.io/home) provides a shared way to save how an agent performs a task. MCP gives different agents a common way to connect to outside tools. With those foundations in place, reusing capabilities across Codex, Claude Code, and DSH—or carrying them to a new machine—should be much easier.

Shared formats solve how the content is stored. Deployment still depends on each agent. Codex, Claude Code, and DSH store skills, read rules, and connect MCP servers in different ways. A skill may work immediately in one agent, need conversion in another, lose part of its behavior, or require manual setup. Paths and commands add another layer of variation across macOS, Windows, and Linux.

Public discussions already contain examples of this experience. The MCP community has filed client-config portability as an open standardization problem ([MCP IG #2761](https://github.com/modelcontextprotocol/modelcontextprotocol/discussions/2761)), and users have reported skills failing to follow them to a new machine in both the Claude Code and Codex trackers ([Claude Code #36693](https://github.com/anthropics/claude-code/issues/36693), [Codex #26691](https://github.com/openai/codex/issues/26691)). These reports show that the problem occurs. They cannot establish how common or urgent it is.

A reliable solution has to answer four questions. Which copy is the source of truth across tools and machines? What can be translated automatically, and what meaning might be lost? Which data must stay on the machine? How can changes be applied without damaging existing local work?

## One workspace; every agent is a render target

SkillFerry keeps skills, global rules, and secret-free MCP templates in one workspace: a reviewable directory that can be stored in Git. You maintain the content there once. When you create a plan, SkillFerry generates the configuration shape required by Codex, Claude Code, or DSH. Those agents receive rendered results, while the workspace remains the shared source of truth.

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

The grades describe what happens during that conversion. `native` uses the target's own format and preserves the full meaning. `translated` works after conversion, as the three MCP entries above do. `degraded` runs with known limits. `manual` provides instructions for a step you must complete. `unsupported` means the target has no equivalent capability. Each grade traces back to capability evidence, so a generic "compatible" label is not enough.

So a new machine and a new agent are the same job: keep one copy of the skills. New machine? Pull it down and set it up. New agent? Same copy, installed in that tool's own format.

<figure class="blog-diagram">
  <picture>
    <source media="(max-width: 700px)" srcset="{{ '/images/blogs/skillferry-portability-flow-en-mobile.svg' | relative_url }}">
    <img src="{{ '/images/blogs/skillferry-portability-flow-en.svg' | relative_url }}" alt="SkillFerry turns a target-neutral workspace into a portability plan and native Codex, Claude Code, and DeepSeek Harness configurations while secret values resolve only on the local machine">
  </picture>
  <figcaption>SkillFerry makes portability grades and local-only secret resolution visible before configuration is applied.</figcaption>
</figure>

## Four boundaries behind what it will promise

**Let capabilities travel while state stays local.** Skills, rules, and MCP server definitions describe a reproducible way of working. Tokens, login state, sessions, caches, and generated memory belong to identity or runtime state. SkillFerry manages only explicitly declared capability definitions and never treats a whole `~/.codex` or `~/.claude` directory as a sync unit. Dotfiles synchronization, provider switching, and agent orchestration remain outside its scope.

**After a file lands, check how the feature loads.** A file in the destination directory proves that the write completed. The target agent may still interpret it differently. The current release renders stdio MCP servers into all three native shapes; HTTP/SSE MCP stays `manual`, while plugins and extensions can be declared but require separate installation. The plan exposes those manual steps before anything is written.

**Keep credentials local while capabilities move.** The workspace schema rejects literal secrets in MCP environments and accepts references such as `secret:env/...` or `secret:file/...`. Real values resolve locally at `apply` time. They stay out of JSON reports and the shareable copy created by `skillferry export <destination>`. OS and directory permissions still protect local values; SkillFerry prevents credentials from entering shareable capability definitions.

**Respect changes made by hand.** An ownership ledger records the paths and hashes SkillFerry last wrote. If a managed file changes later, the next `plan` or `apply` reports a conflict (exit code 3) and stops before overwriting it. You choose `adopt`, `overwrite`, or `keep-local`; files are backed up before writes, and a failed multi-file group rolls back the writes it already completed.

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

Open formats make the content reusable. Deployment still has to account for discovery directories, configuration shapes, operating systems, secret references, and local edits. SkillFerry shows those differences before applying a plan, including what each target can receive, where meaning is lost, and which steps remain manual.

If you are re-installing skills, rewriting rules, or maintaining several copies of the same MCP config, run one isolated `import → plan` first. See which capabilities travel natively, which need translation, and which should never leave the local machine.

Repository: [GreenLv/skillferry](https://github.com/GreenLv/skillferry)<br>
Latest release: [GitHub Releases](https://github.com/GreenLv/skillferry/releases/latest)<br>
Install: [PyPI](https://pypi.org/project/skillferry/)

</div>
