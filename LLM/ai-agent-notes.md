OpenCode Tutorial for Beginners: [Learn 90% Of OpenCode in Under 25 Minutes](https://www.youtube.com/watch?v=QzqaZshQcJI)

[Open Code](https://opencode.ai/)

#### OpenCode vs. Claude Code

OpenCode is a terminal-first coding agent (TUI/CLI/Web/Desktop).

Open Code can do everything that [Claude Code](https://github.com/anthropics/claude-code) can do,

###### OpenCode

- MIT + Open Source
- Provider-agnostic (Claude, OpenAI, Google, local machine)

###### Claude Code

- Anthropic' official CLI workflow
- Terminal + IDE + Github workflow
- Plugins + official docs
- Includes feedback/usage data collection

###### Install OpenCode on Windows (WSL)

OpenCode recommends WSL for best performance + terminal compstibility.

```bash
curl -fsSL https://opencode.ai/install | bash
```

####

#### Overview of OpenCode

###### Three Layers of OpenCode

1. Agents (who works)
   - Switch between Build (does work) and Plan (thinks safely).
   - You can also `@` mention subagents
2. Rules (how we behave)
   - `AGENTS.md` tells the model your project conventions, structure, and "do/dont" rules.
3. Extensions (how we automate)
   - `Skills` = reusable SOPs.
   - `Commands` = one-shot macros you run with `/name`

###### Two Modes

- `Build`
  - Full tool access (edits + bash) for implementation
  - Use when you're ready for code changes
  - Best for: adding features, refactors, fixing tests
- `Plan`
  - Restricted by permissions to prevent unintended changes
  - Defaults many risky actions to "ask" (file edits, bash)
  - Best for: design, code review, debugging strategy

#### Skills

###### Overview

`Skills` are folders with a `SKILL.md` file. OpenCode discovers them automatically.

- They are discovered but not fully injected into context until needed.
- They teach "how to do X here" (SOPs, workflows, repo-specific policies)
- Great for tooling usage (gh, docker, release scripts) and team standards.

###### Location to Put Skills

```bash
# Per-project
.opencode/skills/<name>/SKILL.md

# Global (your defaults)
~/.config/opencode/skills/<name>/SKILL.md
```

###### Discovery Behavior

- OpenCode walks up to the git worktree and loads any matching skills
- Global skills are always available in every repo

###### Required Frontmatter

```markdown
--
name: pr-review
description: Review PRs and produce a checklist of fixes
--

# Steps

1. Read diff
2. Flag risks
3. Suggest tests
```

#### Commands

`Commands` are for repeatitive prompts.

- Work flow shortcuts, run with `/{command}`
- Each command expands into a prompt template
- You can optionally force which agent runs it (plan/build)

###### Location

```bash
# Global:
~/.config/opencode/commands/<name>.md

# Per-project
.opencode/commands/<name>.md
```

###### Example

```
---
description: Run tests with coverage
agent: build
model: anthropic/claude-3-5-sonnet-20241022
---

Run the full test suite with coverage.
Focus on failing tests and suggest fixes.
```

######
