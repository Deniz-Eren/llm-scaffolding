## Purpose

Document the architectural decisions and structural organization of the AI Scaffolding Bootstrap project.

## Structure

Architecture is organized by: project overview, directory structure rationale, key design patterns, and integration points.

## Formatting Rules

- Use code blocks for path examples.
- Keep architectural descriptions concise and reference skill files for procedural details.

---

## Project Overview

This is a documentation-only project. The primary artifact is `prompts/bootstrap-prompt.md` — a single, self-contained prompt that configures an AI agent to scaffold complete project structures.

There is no build system, no source code, and no dev environment. The project structure is designed to support the bootstrap prompt's own development through a self-improvement loop.

## Directory Structure Rationale

```
/
├── AGENTS.md          ← Supreme authority for agent behavior (not in docs/)
├── README.md          ← Entry point with overview and quick-start
├── LICENSE.md         ← Project license (immutable)
├── prompts/           ← All prompt templates (bootstrap, retro, rubric)
├── docs/
│   ├── *.md           ← UPPERCASE-named documentation (TASKS, HISTORY, VISION, DECISIONS, STANDARDS)
│   ├── SKILLS.mdx     ← Source skills specification (immutable)
│   ├── COMMITS.md     ← Source commits specification (immutable)
│   ├── semver.md      ← Source semver specification (immutable)
│   ├── THIRD-PARTY-NOTICES.md ← Third-party attribution
│   └── skills/        ← Agent skill implementations (lowercase dirs)
└── .gitignore         ← Build, IDE, and environment exclusions
```

### Why `docs/` is UPPERCASE

Non-skill documentation files under `docs/` use UPPERCASE names (e.g., `TASKS.md`, `DECISIONS.md`) to distinguish them from skill files and to follow the project's naming convention.

### Why `prompts/` is lowercase

Prompt templates are implementation artifacts, not documentation. They use lowercase to differentiate from the formal documentation layer.

### Why `skills/` uses lowercase

Skills follow the bare lowercase tool folder convention (`create-skill/`, `dev-environment/`) with `SKILL.md` as the entry point.

## Key Design Patterns

### Self-Improvement Loop

The project implements a closed-loop refinement process:

1. **Create** → Design bootstrap prompt and assessment rubric
2. **Generate** → Run prompt against 6 independent project types
3. **Retrospect** → Same AI critiques the prompt
4. **Assess** → Fresh AI evaluates all 6 scaffoldings with the rubric
5. **Refine** → Feed insights back, iterate

This loop is documented in `README.md` and orchestrated through the prompts in `prompts/`.

### Skill-Based Governance

All operational procedures live in `docs/skills/`. This ensures:
- **DRY**: No duplicated instructions across files.
- **Modularity**: Each skill owns a distinct concern.
- **Discoverability**: Skills are organized in a flat directory structure.

Key skills:
- `create-skill/` — Meta-skill for creating new skills
- `dev-environment/` — Environment setup (documents that no env is needed)
- `git/` — Git conventions, commit rules, and Assisted-by footer
- `state-management/` — TASKS/HISTORY/DECISIONS update procedures

### Immutable Source Documents

Specification documents (SKILLS.mdx, COMMITS.md, semver.md) exist in two places:
1. **Source** (`docs/`) — Original, immutable, canonical versions
2. **Copies** (`docs/skills/*/references/`) — Referenced by skill files

Copies have relative links fixed to their new locations but content is verbatim.

## Integration Points

| Component | References | Referenced By |
|---|---|---|
| `prompts/bootstrap-prompt.md` | All skills, AGENTS.md | README.md |
| `prompts/retro-prompt.md` | bootstrap-prompt.md | README.md |
| `prompts/rubric-prompt.md` | bootstrap-prompt.md | README.md |
| `docs/skills/create-skill/references/SKILLS.mdx` | SKILL.md in create-skill/ | STANDARDS.md |
| `docs/skills/git/references/COMMITS.md` | SKILL.md in git/ | STANDARDS.md |
| `docs/skills/git/references/semver.md` | SKILL.md in git/ | STANDARDS.md |
| `docs/THIRD-PARTY-NOTICES.md` | README.md, all skill references | docs/skills/*/references/*.md |
| `docs/DECISIONS.md` | ADRs for all major decisions | HISTORY.md |

## Non-Architectural Decisions

Per `docs/DECISIONS.md`:
- **ADR-1**: Documentation-only project type (no build system, no tests, no formatter)
- **ADR-4**: Skills philosophy (non-overlapping domains, mandatory create-skill and state-management)
- **ADR-6**: No development environment (documented in dev-environment skill for completeness)
