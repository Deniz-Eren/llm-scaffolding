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

There is no build system, no source code, and no dev environment. The prompts in `prompts/` are standalone templates — the user decides whether and how to use them in their own iterative refinement process.

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

### Iterative Prompt Refinement (Manual Process)

The 6-project stress test and self-improvement loop described in `README.md` was a **manual methodology** used by the author to develop and refine `prompts/bootstrap-prompt.md`. It is **not** a feature of the generated scaffolding, nor is it built into the prompt itself.

The loop was performed as follows:

1. **Create** → Design bootstrap prompt and assessment rubric
2. **Generate** → Run the prompt 6 independent times (alpha→zeta) by the author
3. **Retrospect** → Author asks an AI to critique the prompt using `retro-prompt.md`
4. **Assess** → Author asks a fresh AI session to evaluate all 6 scaffoldings using `rubric-prompt.md`
5. **Refine** → Feed insights back into the prompt, iterate

The prompts in `prompts/` are standalone templates. The user decides whether and how to use them in their own verification loop. The scaffolding itself has no mechanism to generate, test, or assess other projects.

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
