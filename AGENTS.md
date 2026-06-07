# AI Agent Governance

## Purpose

Establish the rules, boundaries, and operational protocols for AI agents operating in this project.

## Structure

Governance content is organized into: agent identity, mode toggle, workflow, failure modes, CLI boundaries, token management, git protocol, and pre-commit checklist.

## Formatting Rules

- Use tables for structured comparisons (failure modes, CLI boundaries).
- Use checkboxes for actionable items (pre-commit checklist).
- Keep each section concise and reference skill files for detailed procedures.

---

## Agent Identity

The agent and model used for AI-assisted commits are configured here so the `Assisted-by:` footer always references the correct values.

| Setting | Value |
|---|---|
| **Agent Name** | `pi-agent` |
| **Model** | `Qwen3.6-35B-A3B-UD-Q4_K_XL` |

The `Assisted-by:` footer in every commit uses the format: `pi-agent:Qwen3.6-35B-A3B-UD-Q4_K_XL`.

---

## Mode Toggle

| Mode | Behavior | Use Case |
|---|---|---|
| **AUTONOMOUS** | Agent proceeds without pausing. Commits are made automatically with `--no-gpg-sign`. | Routine maintenance, scaffolding generation, documentation updates. |
| **HITL** | Agent pauses for human confirmation before committing. Waits for `GPG SIGNATURE` before signing. | High-impact changes, security-sensitive operations, releases. |

**Default:** AUTONOMOUS

---

## Predict → Act → Verify

All agent actions follow this three-phase workflow:

1. **Predict**: Analyze the request, identify required steps, and check for potential failures before acting.
2. **Act**: Execute the planned steps, making atomic commits after each logical phase.
3. **Verify**: Run self-verification checks (build, test, format, lint) and confirm success before proceeding.

If verification fails in Phase 3, **Act** again with the fix, then **Verify** once more. Do not proceed to the next phase until the current phase passes.

---

## Failure Modes

| Failure | Response | Escalation |
|---|---|---|
| Build fails | Diagnose root cause, fix scaffolding (not boilerplate), re-run build | If unable to fix after 3 attempts, switch to HITL mode |
| Test fails | Investigate test failures, fix source of failure, re-run | If unable to fix after 3 attempts, switch to HITL mode |
| Formatter rejects config | Strip invalid options one at a time, re-test, document in DECISIONS.md | If config cannot be validated, create zero-option config and note uncertainty |
| Tool not installed | Create SKILL.md documenting the tool and noting it must be installed. Record absence in DECISIONS.md | None — documented for future use |
| Git conflict | Abort, update from remote, resolve conflicts, re-attempt | Switch to HITL mode for conflict resolution |
| Token limit approaching | Prioritize critical content, compress documentation, avoid redundant info | None — adjust output length |
| Context overflow | Summarize earlier context, reference files instead of embedding content | None — rely on skill file references |

---

## CLI Execution Boundaries

| Action | Allowed | Requires HITL |
|---|---|---|
| Read files | ✓ | — |
| Run version checks (`--version`) | ✓ | — |
| Execute build/test scripts | ✓ | — |
| Execute formatter scripts | ✓ | — |
| Make git commits (Autonomous mode) | ✓ | — |
| Make git commits (HITL mode) | ✗ | `WAITING FOR GPG SIGNATURE` |
| Modify IMMUTABLE documents | ✗ | ✗ (never) |
| Delete project files | ✗ | ✗ (never) |
| Install system packages | ✓ | — |
| Modify .gitignore | ✓ | — |
| Push to remote | ✗ | ✓ |

---

## Token & Context Management

- **Load skills progressively**: Load SKILL.md only when relevant; don't preload all skills.
- **Reference, don't embed**: Point to skill files and documentation instead of repeating instructions.
- **Keep SKILL.md under 500 lines**: Split detailed reference material into separate files under `references/`.
- **Summarize, don't repeat**: When referencing earlier context, use concise summaries.
- **Batch reads**: Read multiple files in a single call when they're related.
- **Use find efficiently**: When scanning for files, use `find` with `-print0` and appropriate name groups.

---

## Git Protocol

### Identity

All commits use the configured identity inline — never modify local git config:

```bash
git -c user.name="Deniz Eren" -c user.email="deniz.eren@outlook.com" commit -m "message" --no-gpg-sign
```

### Commit Message Format

Every commit ends with a blank line followed by an `Assisted-by:` footer:

```
{commit message body}

Assisted-by: {AgentName}:{ModelVersion}
```

If additional tools were used, append with ` + `:

```
Assisted-by: {AgentName}:{ModelVersion} + {Tool1} + {Tool2}
```

### Commit Mode Rules

| Mode | Signing Flag | Behavior |
|---|---|---|
| AUTONOMOUS | `--no-gpg-sign` | Proceed without pausing |
| HITL | (default signing) | Pause for human confirmation; WAITING FOR GPG SIGNATURE |

### Conventional Commits

Use types from [docs/skills/git/references/COMMITS.md](docs/skills/git/references/COMMITS.md). Reference: [docs/skills/git/SKILL.md](docs/skills/git/SKILL.md).

### Branch Strategy

- `main` is the protected production branch.
- Create feature branches from `main` for changes.
- Squash and merge feature branches into `main`.

---

## Pre-Commit Checklist

Before every commit, verify:

- [ ] Commit message follows Conventional Commits format
- [ ] `Assisted-by:` footer is present
- [ ] Build and tests pass (if applicable)
- [ ] Formatter finds no violations (if applicable)
- [ ] `TASKS.md` updated with `[x] COMPLETE YYYY-MM-DD` for completed tasks
- [ ] `HISTORY.md` updated with event entry
- [ ] `DECISIONS.md` updated with ADR if new decisions made
- [ ] `THIRD-PARTY-NOTICES.md` updated with attribution for new third-party components or dependencies
- [ ] Copyright headers verified on all new/modified source files
- [ ] No IMMUTABLE documents modified

> **Detailed update procedures**: See [docs/skills/state-management/SKILL.md](docs/skills/state-management/SKILL.md) for full instructions on updating state documents.

---

## HITL Text

When HITL mode is active and waiting for human confirmation:

```
WAITING FOR GPG SIGNATURE
```

Do not proceed until the human confirms or provides the GPG signature.
