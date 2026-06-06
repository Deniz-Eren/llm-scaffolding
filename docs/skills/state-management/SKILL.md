---
name: state-management
description: Procedures for updating project state documents: TASKS.md, HISTORY.md, and DECISIONS.md. Use when completing tasks, recording events, or making architectural decisions.
metadata:
  author: llm-scaffolding
  version: "1.0"
---

# State Management

## Purpose

Define procedures for maintaining project state documents: TASKS.md, HISTORY.md, and DECISIONS.md.

## Structure

Covers update procedures for each state document, including formatting rules and timing.

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

## Pre-Commit Integration

The Pre-Commit Checklist in `[AGENTS.md](../../AGENTS.md)` requires updating all three documents before every commit:

1. **TASKS.md**: Mark completed tasks with `[x] COMPLETE YYYY-MM-DD`
2. **HISTORY.md**: Add event entry for the commit
3. **DECISIONS.md**: Add ADR if any new decisions were made
4. **Copyright headers**: Verify on all new/modified source files

---

## Reference

- TASKS.md: `[docs/TASKS.md](../TASKS.md)`
- HISTORY.md: `[docs/HISTORY.md](../HISTORY.md)`
- DECISIONS.md: `[docs/DECISIONS.md](../DECISIONS.md)`
- AGENTS.md Pre-Commit Checklist: `[AGENTS.md](../../AGENTS.md)`
