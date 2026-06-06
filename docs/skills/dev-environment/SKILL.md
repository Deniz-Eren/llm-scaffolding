---
name: dev-environment
description: Document development environment setup procedures for this project. Includes activation, dependency installation, build/test/formatter tool usage, and troubleshooting.
---

# Development Environment

## Purpose

Document how to set up, activate, and use the development environment for this project.

## Structure

This skill covers environment setup, activation, dependency installation, tool usage within the environment, and troubleshooting steps.

## Formatting Rules

- Follow the steps in order.
- Reference specific files and directories by path.
- Include troubleshooting steps for common failures.

---

## Environment Type

**This project is Documentation-only.** No build system, no primary language, and no dev environment is configured.

No development environment setup is required.

## What This Means

- No virtual environment to activate.
- No dependencies to install.
- No build or test commands to run.
- No container to enter.

## Related Skills

- `[state-management/SKILL.md](scripts/state-management/SKILL.md)` — For updating project state documents (TASKS, HISTORY, DECISIONS).
- `[git/SKILL.md](scripts/git/SKILL.md)` — For git conventions and commit rules.

## Troubleshooting

**Q: The bootstrap prompt expects a dev-environment skill to exist.**
A: This skill exists as a template. For documentation-only projects, no actual environment setup is needed. For software projects with a build system, follow the corresponding skill (CMake, Poetry, npm, etc.).

**Q: How do I set up a dev environment for a software project?**
A: The bootstrap prompt generates environment setup based on the `Dev Environment` and `Build System` tunables:
- **Python + Native**: `python -m venv .venv && source .venv/bin/activate && pip install -r requirements.txt`
- **Containerized**: `podman compose build dev && podman compose run dev`
- **See**: `docs/skills/build-system/SKILL.md` for build-specific environment details.
