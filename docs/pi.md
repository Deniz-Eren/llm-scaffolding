# Pi Coding Agent

## Purpose

Install and configure the `pi-subagents` extension so the project can use Pi's subagent system for delegation, orchestration, and agent-driven workflows.

## Structure

Agent definitions live in `docs/agents/` — a directory that is **agent-agnostic** and belongs in version control. Integration with any specific coding agent is handled via a symbolic link, so the definitions themselves never need to change:

| Agent | Symlink Command | Purpose |
|---|---|---|
| **Pi** | `ln -sfn docs/agents .pi/agents` | Inject agents into Pi's project discovery |
| **GitHub Copilot** | `ln -sfn docs/agents .github/agents/` | Inject agents into Copilot's workspace |

Creating the symlink is a one-time setup step per agent platform.

## Formatting Rules

- Agent files use YAML frontmatter for metadata and Markdown for the system prompt body.
- Filenames use lowercase kebab-case (e.g., `reviewer.md`, `deploy-helper.md`).
- Each file must include at least: `name`, `description`, and `tools`.

---

## Setup

Install the subagents extension:

```bash
pi install npm:pi-subagents
```

Then create the symlink for your chosen agent platform. For Pi:

```bash
ln -sfn docs/agents .pi/agents
```

After creating the symlink, restart the Pi session to pick up the new agents.

---

## Agent File Format

Every agent file consists of YAML frontmatter followed by a Markdown system prompt:

```markdown
---
name: my-agent
description: What this agent does
model: openai-codex/gpt-5.4
tools: read, grep, find, ls, bash
systemPromptMode: replace
inheritProjectContext: true
inheritSkills: false
---

Your system prompt here.
```

### Frontmatter Fields

| Field | Required | Description |
|---|---|---|
| `name` | Yes | Runtime identifier — used when launching the agent via `subagent(...)` or slash commands |
| `description` | Yes | Brief summary of what the agent does |
| `tools` | Yes | Comma-separated list of tools the agent is allowed to use |
| `model` | No | Override the default model for this agent |
| `systemPromptMode` | No | How to merge with existing prompts. Use `replace` to fully override |
| `inheritProjectContext` | No | Whether the agent inherits the project's session context (default: `true`) |
| `inheritSkills` | No | Whether the agent inherits project skills (default: `false`) |

### Example

```markdown
---
name: code-reviewer
description: Review diffs for correctness and regressions
tools: read, grep, find, ls, bash
systemPromptMode: replace
---

You are a code review agent. Inspect the current diff and report findings.

## Instructions

1. Inspect the staged diff
2. Check for correctness issues, regressions, and edge cases
3. Report findings with file paths and line numbers
4. Do not modify project files
```

---

## Discovery

Pi discovers agents recursively in `.pi/agents/`. The symlink from `docs/agents/` makes this work without duplicating files.

To verify agents are visible:

```bash
pi subagents list
```
