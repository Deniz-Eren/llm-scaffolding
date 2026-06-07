## Purpose

Record significant events, milestones, and changes in the project's history.

## Structure

Each entry includes a date, category, and description. Entries are listed in reverse chronological order (newest first).

## Formatting Rules

- Each entry starts with `## YYYY-MM-DD — [Category] Title`
- Categories use `[CAT]` tags
- Keep descriptions concise (1–3 sentences)
- Add entries for major decisions, releases, milestones, and notable events

<!-- [CAT] Documentation -->

## 2026-06-06 — [Docs] Separated Architecture from Decisions; Updated Bootstrap Prompt

Rewrote `ARCHITECTURE.md` to describe the current system architecture (files, structure, components) instead of recording decisions. Fixed the root cause in `bootstrap-prompt.md` — the instruction "Create architectural documentation under `docs/`" was replaced with specific instructions defining what ARCHITECTURE.md should contain. Added ADR-8 documenting this decision. Updated `STANDARDS.md` with a reference table clarifying each `docs/` file's purpose.

<!-- [CAT] Documentation -->

## 2026-06-06 — [Docs] Fixed Backtick-Wrapped Links and Added ADR-7

Fixed all markdown links that were broken by being wrapped in backticks (e.g., `` `[text](url)` `` → `[text](url)`). Added ADR-7 to STANDARDS.md and the bootstrap prompt to prevent this mistake from recurring. Broken links were found in SKILL.md files across `docs/skills/`, STANDARDS.md, and bootstrap prompt.

<!-- [CAT] Documentation -->

## 2026-06-06 — [Docs] Clarified Manual Nature of 6-Project Stress Test

Updated README.md, ARCHITECTURE.md, and VISION.md to explicitly state that the 6-project stress test and feedback loops were manual steps performed by the author, not an automated feature of the scaffolding. The prompts in `prompts/` are standalone templates for the user to apply at their discretion.

<!-- [CAT] Scaffolding -->

## 2026-06-06 — [Scaffold] Initial Project Structure

Created the initial project scaffold with governance documents, skills directory, and pre-existing document integration. The project is a documentation-based AI scaffolding bootstrap system.

<!-- [CAT] Documentation -->

## 2026-06-06 — [Docs] Pre-Existing Documents Integrated

Integrated five pre-existing specification documents: LICENSE.md, SKILLS.mdx, COMMITS.md, semver.md, and THIRD-PARTY-NOTICES.md. All relative links were adjusted for new file locations.

<!-- [CAT] Governance -->

## 2026-06-06 — [Governance] Agent Governance Established

Created AGENTS.md with autonomous mode governance, Pre-Commit Checklist, and CLI execution boundaries. Git protocol with Assisted-by footer convention documented.

<!-- [CAT] Development -->

## 2026-06-06 — [Dev-Env] Development Environment Configuration

Documented development environment setup procedures in docs/skills/dev-environment/SKILL.md. For this documentation-only project, environment setup is not required.

<!-- [CAT] Skills -->

## 2026-06-06 — [Skills] Skills Directory Established

Created skills for git conventions, skill creation, and state management. Each skill owns a distinct operational concern with no domain overlap. Standards document defines copyright headers and file naming conventions.

<!-- [CAT] Finalization -->

## 2026-06-06 — [Bootstrap] Scaffolding Complete

All bootstrap steps completed. Project structure established with governance, documentation, skills, and state management. Self-verification passed.
