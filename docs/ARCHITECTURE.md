## Purpose

Document the architecture of the AI Scaffolding Bootstrap project — what files exist, how they are structured, and what each component does.

## Structure

Architecture is organized by: system overview, directory structure, component descriptions, and integration points.

## Formatting Rules

- Use code blocks for path examples.
- Keep descriptions concise and reference skill files for procedural details.
- Do NOT record decisions here — use `docs/DECISIONS.md` for that.

---

## System Overview

This is a documentation-only project. The primary artifact is `prompts/bootstrap-prompt.md` — a single prompt file that configures an AI agent to scaffold complete project structures.

There is no build system, no source code, and no dev environment. The prompts in `prompts/` are standalone templates — the user decides whether and how to use them.

---

## Directory Structure

```
/
├── AGENTS.md          ← AI agent governance (mode toggle, git protocol, checklist)
├── README.md          ← Entry point: overview, quick-start, how-to-use
├── LICENSE.md         ← Project license (MIT, immutable)
├── .gitignore         ← Build, IDE, and environment exclusions
├── prompts/
│   ├── bootstrap-prompt.md ← Scaffolding bootstrap prompt (the deliverable)
│   ├── retro-prompt.md     ← Retrospective analysis template
│   └── rubric-prompt.md    ← Assessment rubric template
├── docs/
│   ├── TASKS.md            ← Task tracking with completion dates
│   ├── HISTORY.md          ← Project chronicle
│   ├── VISION.md           ← Mission and guiding principles
│   ├── DECISIONS.md        ← Architectural Decision Records (ADRs)
│   ├── STANDARDS.md        ← Copyright and file creation standards
│   ├── THIRD-PARTY-NOTICES.md ← Third-party dependency attribution
│   ├── SKILLS.mdx          ← Original skills spec (immutable source)
│   ├── COMMITS.md          ← Original commits spec (immutable source)
│   ├── semver.md           ← Original semver spec (immutable source)
│   └── skills/             ← Agent skill implementations
│       ├── create-skill/   ← Meta-skill: how to create new skills
│       │   └── references/ ← SKILLS.mdx copy (immutable)
│       ├── dev-environment/← Dev environment setup docs
│       ├── git/            ← Git conventions
│       │   └── references/ ← COMMITS.md, semver.md copies
│       └── state-management/ ← TASKS/HISTORY/DECISIONS update procedures
```

---

## Component Descriptions

### Root Files

| File | Purpose |
|---|---|
| `AGENTS.md` | Supreme authority for AI agent behavior: mode toggle, CLI boundaries, git protocol, pre-commit checklist. |
| `README.md` | Entry point: project overview, how to use the bootstrap prompt, development environment notes, repository structure. |
| `LICENSE.md` | MIT License (immutable). |
| `.gitignore` | Excludes build outputs, IDE files, language artifacts, and dev environment directories. |

### Prompt Files (`prompts/`)

| File | Purpose |
|---|---|
| `bootstrap-prompt.md` | The main deliverable: a single prompt that configures an AI agent to scaffold a complete project structure with governance, skills, and boilerplate. |
| `retro-prompt.md` | Template for retrospective analysis: critiques the bootstrap prompt after use. |
| `rubric-prompt.md` | Assessment rubric: evaluates generated scaffoldings against criteria. |

### Documentation Files (`docs/`)

| File | Purpose |
|---|---|
| `TASKS.md` | Tracks project tasks with `[x] COMPLETE YYYY-MM-DD` format. |
| `HISTORY.md` | Chronological record of significant events (reverse chronological). |
| `VISION.md` | Mission statement and guiding principles for the project. |
| `DECISIONS.md` | Architectural Decision Records (ADRs): context, decision, alternatives, consequences. |
| `STANDARDS.md` | Copyright headers, file naming, document formatting rules. |
| `THIRD-PARTY-NOTICES.md` | Attribution for third-party dependencies and copied files. |
| `SKILLS.mdx` | Original skills specification (immutable source). |
| `COMMITS.md` | Conventional Commits specification (immutable source). |
| `semver.md` | Semantic Versioning 2.0.0 specification (immutable source). |

### Skills Directory (`docs/skills/`)

| Skill | Purpose |
|---|---|
| `create-skill/` | Meta-skill: step-by-step instructions for creating new agent skills. |
| `dev-environment/` | Documents development environment setup (for this project: no env needed; for software projects: template for venv or container). |
| `git/` | Git conventions: commit format, Assisted-by footer, branch strategy, Conventional Commits reference. |
| `state-management/` | Procedures for updating TASKS.md, HISTORY.md, DECISIONS.md, and THIRD-PARTY-NOTICES.md. |

### Reference Files (`docs/skills/*/references/`)

Copies of immutable source documents, with relative links adjusted for their new locations:

| Skill | Reference File | Purpose |
|---|---|---|
| `create-skill/` | `SKILLS.mdx` | Skills specification blueprint for skill creation. |
| `git/` | `COMMITS.md` | Conventional Commits format reference. |
| `git/` | `semver.md` | Semantic Versioning reference. |

---

## Integration Points

| Component | References | Referenced By |
|---|---|---|
| `prompts/bootstrap-prompt.md` | All skills, AGENTS.md | README.md |
| `prompts/retro-prompt.md` | bootstrap-prompt.md | README.md |
| `prompts/rubric-prompt.md` | bootstrap-prompt.md | README.md |
| `docs/skills/create-skill/references/SKILLS.mdx` | SKILL.md in create-skill/ | STANDARDS.md |
| `docs/skills/git/references/COMMITS.md` | SKILL.md in git/ | STANDARDS.md |
| `docs/skills/git/references/semver.md` | SKILL.md in git/ | STANDARDS.md |
| `docs/THIRD-PARTY-NOTICES.md` | (standalone — no cross-references) | (standalone — referenced by Pre-Commit Checklist in AGENTS.md) |
| `docs/DECISIONS.md` | (standalone — contains ADRs) | (referenced by Pre-Commit Checklist in AGENTS.md and state-management SKILL.md) |
