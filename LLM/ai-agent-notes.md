## Agent Skills vs. MCP

Youtube: [Agent Skills vs MCP: What’s the difference?](https://www.youtube.com/watch?v=6wdvSH61xGw)

Generally, AI is getting smarter and smarter, in not only [GPQA](https://github.com/idavidrein/gpqa), but in [SWE-bench](https://www.swebench.com/).

#### MCP (Model Context Protocol)

This is a universal way to give LLMs tools and context. "USB-C Port for AI Application"

The idea is to connect any AI app to any tools, like tools to manipulate notes on notion, etc.

Without MCP, service providers will provide an integration for every distinct AI apps.

It uses `client-server` architecture, where MCP client send requests to MCP server and get responses.

However, the action of MCP is `token-heavy`, because AI needs a large amount of context to let it know which tool is available and how t can manage those tools.

#### Agents Skills

###### Overview of Skills

Basically, it is a folder with instructions accessed by agent as needed.

```
skill-name/
┗ SKILL.md
```

A skill consists two parts:

- `frontmatter`: loaded at startup
  - `name`
  - `description`
- `Body`: Loaded if agent calls skill

###### Progressive Disclosure

Claude API Docs: [Progressive disclosure patterns](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/best-practices#progressive-disclosure-patterns)

|         | Content                               | Enters Context Window...     | Tokens   |
| ------- | ------------------------------------- | ---------------------------- | -------- |
| Level 1 | SKILL.md and metadata                 | On start up                  | ~100     |
| Level 2 | SKILL.md body                         | When agent invokes the skill | <5k      |
| Level 3 | Files and folders in skills directory | As needed by agent           | No limit |

## OpenCode vs. Claude Code

#### References

OpenCode Tutorial for Beginners: [Learn 90% Of OpenCode in Under 25 Minutes](https://www.youtube.com/watch?v=QzqaZshQcJI)

[Open Code](https://opencode.ai/)

#### Comparison

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
