---
name: git
description: Git conventions and commit rules for this project. Use when making commits, writing commit messages, managing branches, or handling Git operations.
metadata:
  author: llm-scaffolding
  version: "1.0"
---

# Git Conventions

## Purpose

Document Git usage rules, commit message format, and branching strategy for this project.

## Structure

Covers commit format, git protocol, branch strategy, and Assisted-by footer convention.

## Formatting Rules

- All commits use inline identity flags.
- Every commit ends with an Assisted-by footer.
- Follow Conventional Commits types.

---

## Commit Mode

This project operates in **AUTONOMOUS** mode.

| Mode | Signing Flag | Behavior |
|---|---|---|
| AUTONOMOUS | `--no-gpg-sign` | Proceed without pausing |
| HITL | (default signing) | Pause for human confirmation |

## Git Protocol

Always use inline identity flags. Never modify local git config:

```bash
git -c user.name="Deniz Eren" -c user.email="deniz.eren@outlook.com" <command>
```

## Commit Message Format

Every commit message must follow this structure:

```
<type>[optional scope]: <description>

[optional body]

Assisted-by: {AgentName}:{ModelVersion}
```

### Components

1. **Type**: Required. One of: `feat`, `fix`, `docs`, `scaffold`, `refactor`, `style`, `test`, `chore`, `ci`, `build`, `perf`.
2. **Scope**: Optional. In parentheses after the type.
3. **Description**: Short summary of changes.
4. **Body**: Optional. Detailed explanation, one blank line after description.
5. **Assisted-by Footer**: Required. Always present, after a blank line.

### Assisted-by Footer

The footer identifies the AI agent and model version that assisted with the commit:

```
Assisted-by: pi-agent:Qwen3.6-35B-A3B-UD-Q4_K_XL
```

If additional tools were used:

```
Assisted-by: pi-agent:Qwen3.6-35B-A3B-UD-Q4_K_XL + Cursor + Claude
```

### Examples

```
scaffold: add state management skill

Created docs/skills/state-management/SKILL.md with procedures
for updating TASKS.md, HISTORY.md, and DECISIONS.md.

Assisted-by: pi-agent:Qwen3.6-35B-A3B-UD-Q4_K_XL
```

```
docs: update README with governance links

Added references to AGENTS.md and ARCHITECTURE.md in the
governance section of README.md.

Assisted-by: pi-agent:Qwen3.6-35B-A3B-UD-Q4_K_XL
```

## Conventional Commits Reference

Full Conventional Commits specification is available at:
[references/COMMITS.md](references/COMMITS.md)

## Semantic Versioning Reference

Semantic Versioning 2.0.0 is available at:
[references/semver.md](references/semver.md)

## Branch Strategy

- `main` is the protected production branch.
- Create feature branches from `main` for changes.
- Squash and merge feature branches into `main`.
- Commit messages on `main` should follow Conventional Commits.

## Committing Workflow

1. **Stage changes**: `git add <files>`
2. **Verify changes**: `git diff --staged`
3. **Commit**: Use the commit format above with the `Assisted-by:` footer
4. **Verify**: Check `git log --oneline` to confirm the commit message

## Pre-Commit Checklist

- [ ] Commit type follows Conventional Commits
- [ ] `Assisted-by:` footer is present
- [ ] Commit message is concise but descriptive
- [ ] No IMMUTABLE documents are modified
- [ ] State documents are updated (TASKS.md, HISTORY.md, DECISIONS.md)
- [ ] Build and tests pass (if applicable)

> For detailed state document update procedures, see [state-management/SKILL.md](state-management/SKILL.md).
