---
name: state-management
description: Procedures for updating project state documents: TASKS.md, HISTORY.md, DECISIONS.md, and THIRD-PARTY-NOTICES.md. Use when completing tasks, recording events, making architectural decisions, or adding third-party components.
metadata:
  author: llm-scaffolding
  version: "1.0"
---

# State Management

## Purpose

Define procedures for maintaining project state documents: TASKS.md, HISTORY.md, DECISIONS.md, and THIRD-PARTY-NOTICES.md.

## Structure

Covers update procedures for each state document, including formatting rules, trigger conditions, and examples.

## Formatting Rules

- Follow the exact formatting rules defined in each document.
- Never delete existing entries.
- Always use today's date in ISO format (YYYY-MM-DD).

---

## TASKS.md Update Procedure

TASKS.md tracks project tasks with completion status and dates.

### When to Update

- After completing any task listed in TASKS.md.
- When creating new tasks during planning.
- When re-prioritizing existing tasks.

### How to Update

1. **Mark completed tasks**: Change `[ ]` to `[x]` and append ` COMPLETE YYYY-MM-DD`
   ```markdown
   - [x] COMPLETE 2026-06-06 scaffold: create initial project structure
   ```

2. **Add new tasks**: Add under the appropriate category section
   ```markdown
   - [ ] COMPLETE scaffold: add new feature
   ```

3. **Group by category**: Use comments like `<!-- [CAT] Category Name -->` to group tasks.

### Example

**Before:**
```markdown
- [ ] COMPLETE scaffold: update documentation
```

**After:**
```markdown
- [x] COMPLETE 2026-06-06 scaffold: update documentation
```

---

## HISTORY.md Update Procedure

HISTORY.md records significant events in the project's chronicle.

### When to Update

- After major decisions are made.
- After significant changes to project structure.
- When milestones are reached.
- At the end of each bootstrap generation cycle.

### How to Update

1. **Add entry at top** (newest first):
   ```markdown
   ## YYYY-MM-DD — [Category] Title
   ```

2. **Write a concise description** (1–3 sentences):
   ```markdown
   Description of the event and its impact on the project.
   ```

3. **Use category tags**: `[Scaffold]`, `[Docs]`, `[Governance]`, `[Dev-Env]`, `[Release]`, etc.

### Example

```markdown
## 2026-06-06 — [Scaffold] Initial Project Structure

Created the initial project scaffold with governance documents, skills directory,
and pre-existing document integration. The project is a documentation-based AI
scaffolding bootstrap system.
```

---

## DECISIONS.md Update Procedure

DECISIONS.md contains Architectural Decision Records (ADRs) for significant decisions.

### When to Update

- When making a new architectural or strategic decision.
- When reversing or modifying an existing decision.
- When the rationale for an existing decision changes.

### How to Update

1. **Determine the next ADR number** (check existing ADRs for the highest number).
2. **Create a new ADR entry**:
   ```markdown
   ## ADR-N (YYYY-MM-DD): Title
   ```

3. **Fill in the four required subsections**:
   - `### Context` — Why was this decision being considered?
   - `### Decision` — What was decided?
   - `### Alternatives` — What other options were considered?
   - `### Consequences` — What are the results of this decision?

4. **Group under a category comment**: `<!-- [CAT] Category -->`

### Example

```markdown
<!-- [CAT] Tooling -->

## ADR-7 (2026-06-06): Linter Configuration

### Context
The project needs a static analysis tool to catch common issues.

### Decision
Use ruff for Python projects and eslint for JavaScript projects.

### Alternatives
- pylint for Python, clang-tidy for C++
- No linter
- flake8 for Python

### Consequences
- Tool configuration files must be generated in Step 3.
- Build Agent script must run the linter as part of the check phase.
```

---

## THIRD-PARTY-NOTICES.md Update Procedure

THIRD-PARTY-NOTICES.md tracks third-party open-source software, files, snippets, and libraries used in the project, with license attribution.

### When to Update

- When adding a new third-party dependency (via package manager or direct inclusion).
- When copying a file or snippet from an external source into the project.
- During initial scaffolding when pre-existing documents are integrated.

### How to Update

1. **Determine which template to use**:
   - **Template A (Copied Files or Snippets)** — Use when directly copying a file or code snippet from an external repository.
   - **Template B (Software Libraries / Dependencies)** — Use when importing an external library via a package manager or linking an external compiled library.

2. **Create the entry** with these fields:

   **Template A (copied files/snippets):**
   ```markdown
   ### [Original Project or Author Name]
   * **Source:** [URL to original source]
   * **Component(s) Used:** [Relative path in our project]
   * **Original License:** [e.g., MIT, Apache 2.0]

   #### License Notice
   Copyright (c) [Year] [Original Copyright Holder]

   [Paste the exact text of the license from the original source]
   ```

   **Template B (libraries/dependencies):**
   ```markdown
   ### [Library Name]
   * **Source:** [URL to library documentation or repository]
   * **Version:** [e.g., v1.4.2]
   * **License:** [e.g., Apache 2.0, MIT]

   #### License Notice
   Copyright (c) [Year] [Original Copyright Holder]

   [Paste the exact text of the library's license]
   ```

3. **Place the entry** under the appropriate section:
   - **Section 1** — Copied Files and Snippets (Template A entries)
   - **Section 2** — Software Libraries and Dependencies (Template B entries)

4. **Verify** that the license text is complete and the source URL is accessible.

### Example

```markdown
### conventionalcommits.org
* **Source:** [github.com/conventional-commits/conventionalcommits.org/content/v1.0.0/index.md](https://github.com/conventional-commits/conventionalcommits.org/blob/master/content/v1.0.0/index.md)
* **Component(s) Used:** [COMMITS.md](./docs/skills/git/references/COMMITS.md)
* **Original License:** MIT License

#### License Notice
Copyright (c) 2018 Conventional Changelog

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights to
use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies
of the Software, and to permit persons to whom the Software is furnished to
do so, subject to the following conditions:...
```

---

## Pre-Commit Integration

The Pre-Commit Checklist in `[AGENTS.md](../../../AGENTS.md)` requires updating all four state documents and verifying copyright headers before every commit:

1. **TASKS.md**: Mark completed tasks with `[x] COMPLETE YYYY-MM-DD`
2. **HISTORY.md**: Add event entry for the commit
3. **DECISIONS.md**: Add ADR if any new decisions were made
4. **THIRD-PARTY-NOTICES.md**: Add attribution for new third-party components or dependencies
5. **Copyright headers**: Verify on all new/modified source files

---

## Reference

- TASKS.md: `[docs/TASKS.md](../TASKS.md)`
- HISTORY.md: `[docs/HISTORY.md](../HISTORY.md)`
- DECISIONS.md: `[docs/DECISIONS.md](../DECISIONS.md)`
- AGENTS.md Pre-Commit Checklist: `[AGENTS.md](../../AGENTS.md)`
