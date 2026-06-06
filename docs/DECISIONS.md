## Purpose

Record architectural and strategic decisions made during the project, with context, alternatives considered, and consequences.

## Structure

Each decision is a self-contained block with Context, Decision, Alternatives, and Consequences sections.

## Formatting Rules

- Each decision gets its own `## ADR-N: Title` heading (where N is the next sequential number).
- Follow with `### Context`, `### Decision`, `### Alternatives`, and `### Consequences` subsections.
- Date decisions in the heading: `ADR-1 (2026-06-06)`.
- Keep decisions concise; reference detailed discussions in HISTORY.md.

<!-- [CAT] Architecture -->

## ADR-1 (2026-06-06): Project Type and Scope

### Context

The project is a meta-project: a scaffolding bootstrap prompt that generates other project scaffolds. It produces documentation artifacts, not executable software.

### Decision

The project type is **Documentation**. No build system, no testing framework, no static analysis, no code formatter, and no dev environment is configured. The deliverable is `prompts/bootstrap-prompt.md` — a single prompt file.

### Alternatives

- Software project with C++/CMake and full toolchain
- Python project with Poetry and pytest
- Node.js project with npm and eslint/prettier

### Consequences

- No build or test automation is needed.
- Skill files focus on documentation standards, git conventions, and prompt engineering.
- The project structure is simpler: no `src/`, no `tests/`, no CI configuration.
- All tool-specific skills are omitted. Only operational skills (create-skill, state-management, dev-environment, git) are required.

<!-- [CAT] Governance -->

## ADR-2 (2026-06-06): Git Commit Protocol

### Context

Multiple AI agents may contribute to this project, each with different identity and signing configurations. A consistent, safe commit protocol is required.

### Decision

All commits use inline `-c` identity flags (or equivalent environment variables). Every commit ends with an `Assisted-by: {Agent}:{Model}` footer. The Commit Mode is Autonomous, using `--no-gpg-sign` for all commits.

### Alternatives

- Modify local git config globally
- Use GPG signing for all commits
- Use separate committer identities per tool

### Consequences

- Commits are portable and don't depend on local config state.
- AI contributions are always traceable via the `Assisted-by:` footer.
- No GPG key management overhead for autonomous commits.

<!-- [CAT] Documentation -->

## ADR-3 (2026-06-06): Documentation Header Standard

### Context

All generated markdown files under `docs/` need a consistent structure to be machine-parseable and human-readable.

### Decision

Every generated `.md` file under `docs/` begins with exactly three required headings in order: `## Purpose`, `## Structure`, `## Formatting Rules`. Pre-existing/IMMUTABLE documents are excluded.

### Alternatives

- Use YAML frontmatter for structure metadata
- Adopt a different heading convention (e.g., Markdown attributes)
- No enforced structure

### Consequences

- A self-verification script can validate document structure.
- Human readers can quickly scan any doc for its purpose and format.
- The verification script uses `grep` patterns, requiring exact heading strings.

<!-- [CAT] Tooling -->

## ADR-4 (2026-06-06): Skills Philosophy

### Context

Skill files drive AI agent behavior. Overlapping skills create confusion and redundant instructions.

### Decision

Each skill owns a distinct tool or operational concern. Skills are merged if they share more than 30% of instructions. Two mandatory skills always exist: `create-skill/` (meta-skill) and `state-management/` (docs update procedures). Skills are created per configured tool only.

### Alternatives

- One monolithic skills file
- Create a skill for every possible concern
- No mandatory skills

### Consequences

- Skills remain focused and under 500 lines.
- New tool integrations are unambiguous.
- Documentation update procedures are always available via state-management skill.

<!-- [CAT] Licensing -->

## ADR-5 (2026-06-06): License and Copyright

### Context

The project uses MIT License with copyright held by Deniz Eren. Third-party documents (COMMITS.md, SKILLS.mdx, semver.md, THIRD-PARTY-NOTICES.md) carry their own licenses.

### Decision

- The project root LICENSE.md is MIT License, Copyright (c) 2026 Deniz Eren <deniz.eren@outlook.com>. IMMUTABLE.
- Third-party notices document the licenses of included specification documents.
- STANDARDS.md defines copyright header format for any future source files.

### Alternatives

- Use Apache 2.0
- Use BSD-3-Clause
- Use a custom license

### Consequences

- Permissive MIT license allows broad reuse of the scaffolding prompt.
- Third-party licenses are properly attributed in THIRD-PARTY-NOTICES.md.
- Copyright headers in future source files follow the format defined in STANDARDS.md.

<!-- [CAT] Development Environment -->

## ADR-6 (2026-06-06): No Development Environment

### Context

The project type is Documentation with no primary language, no build system, and no dev environment configured. The bootstrap prompt requires a DEV-ENV SKILL to exist.

### Decision

No dev environment files are generated. The `docs/skills/dev-environment/SKILL.md` exists but documents that no dev environment setup is required for this documentation-only project.

### Alternatives

- Create a containerized dev environment
- Create a native Python venv

### Consequences

- No build or container infrastructure to maintain.
- The dev-environment skill serves as a template for future software projects.
- The README.md Development Environment section notes no setup is needed.
