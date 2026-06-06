## Purpose

Define project-wide standards for file naming, copyright headers, and document formatting.

## Structure

Standards are organized by category: file naming, copyright headers, document formatting, and skill conventions.

## Formatting Rules

- Standards are mandatory unless explicitly noted as "recommended."
- Deviations must be documented in DECISIONS.md.

---

## File Naming

### Documentation Files (`docs/` non-skill)

The **scaffolding-enforcing** documentation files — those that maintain and enforce the project scaffolding:

- Must use **UPPERCASE** names.
- Prefer single words or hyphenated compounds.
- No spaces.
- Examples: `TASKS.md`, `HISTORY.md`, `VISION.md`, `DECISIONS.md`, `STANDARDS.md`, `ARCHITECTURE.md`, `THIRD-PARTY-NOTICES.md`

Other documentation files (e.g., user guides, API references) are not bound by this rule and may use any sensible naming convention.

### Skill Files

- **Bare lowercase** directory names.
- Each directory contains exactly one `SKILL.md` file.
- Directory name must match the `name` field in SKILL.md frontmatter.
- Examples: `docs/skills/create-skill/SKILL.md`, `docs/skills/git/SKILL.md`, `docs/skills/dev-environment/SKILL.md`

### Prompt Files (`prompts/`)

- **lowercase-hyphenated** names.
- Examples: `bootstrap-prompt.md`, `retro-prompt.md`, `rubric-prompt.md`

### Root Files

- **TitleCase** or specific names: `README.md`, `AGENTS.md`, `LICENSE.md`, `.gitignore`

---

## Copyright Headers

The project license is **MIT License**.
**Copyright (c) 2026 Deniz Eren <deniz.eren@outlook.com>**

Every file that supports comment blocks must include the copyright header at the top. Markdown documents are excluded.

### Source Files

| Extension | Header |
|---|---|
| `*.cpp`, `*.hpp`, `*.h`, `*.c` | `// Copyright (c) 2026 Deniz Eren <deniz.eren@outlook.com>` |
| `*.rs` | `// Copyright (c) 2026 Deniz Eren <deniz.eren@outlook.com>` |
| `*.py` | `# Copyright (c) 2026 Deniz Eren <deniz.eren@outlook.com>` |
| `*.js`, `*.ts` | `// Copyright (c) 2026 Deniz Eren <deniz.eren@outlook.com>` |
| `*.go` | `// Copyright (c) 2026 Deniz Eren <deniz.eren@outlook.com>` |

### Build Files

| File | Header |
|---|---|
| `Dockerfile` | `# Copyright (c) 2026 Deniz Eren <deniz.eren@outlook.com>` |
| `CMakeLists.txt` | `# Copyright (c) 2026 Deniz Eren <deniz.eren@outlook.com>` |
| `package.json` | Not applicable (JSON format does not support comments) |
| `Cargo.toml` | Not applicable (TOML format does not support comments) |
| `Makefile` | `# Copyright (c) 2026 Deniz Eren <deniz.eren@outlook.com>` |

### Shell Scripts

| Extension | Header |
|---|---|
| `*.sh`, `*.bash` | `# Copyright (c) 2026 Deniz Eren <deniz.eren@outlook.com>` |

### Configuration Files

| Extension | Header |
|---|---|
| `*.yaml`, `*.yml` | `# Copyright (c) 2026 Deniz Eren <deniz.eren@outlook.com>` |
| `*.toml` | `# Copyright (c) 2026 Deniz Eren <deniz.eren@outlook.com>` |
| `.clang-format` | `# Copyright (c) 2026 Deniz Eren <deniz.eren@outlook.com>` |
| `.clang-tidy` | `# Copyright (c) 2026 Deniz Eren <deniz.eren@outlook.com>` |

### Exclusions

- Markdown files (`.md`) — do not include copyright headers.
- `.gitignore` — do not include copyright headers (clutters the file).
- `LICENSE.md` — do not include copyright headers (is the license itself).
- Pre-existing/IMMUTABLE documents — do not modify.
- `package.json`, `Cargo.toml` — formats do not support comments.

---

## Document Headers

All generated markdown files under `docs/` must begin with these three headings in order:

1. `## Purpose`
2. `## Structure`
3. `## Formatting Rules`

**Exceptions:**
- Pre-existing/IMMUTABLE documents (retain original content).
- `VISION.md` — rename its internal purpose section to `## Mission` to avoid duplicate headings; the three required headings still appear at the top.

---

## Skill Conventions

### SKILL.md Frontmatter

Follow the specification in `[references/SKILLS.mdx](docs/skills/create-skill/references/SKILLS.mdx)`.

### SKILL.md Content

- Keep SKILL.md under 500 lines.
- Use `## Purpose`, `## Structure`, `## Formatting Rules` as the first three headings.
- Reference files using relative paths from the skill root.
- Keep file references one level deep.

### Domain Overlap

If two skills would share more than 30% of their instructions, merge them into a single skill.

---

## Reference

- Conventional Commits: `[docs/skills/git/references/COMMITS.md](docs/skills/git/references/COMMITS.md)`
- Semantic Versioning: `[docs/skills/git/references/semver.md](docs/skills/git/references/semver.md)`
- Skills Specification: `[docs/skills/create-skill/references/SKILLS.mdx](docs/skills/create-skill/references/SKILLS.mdx)`
