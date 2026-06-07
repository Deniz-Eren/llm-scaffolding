## Purpose

Define the long-term vision and guiding principles for this project.

## Structure

Vision statements are organized by theme, each with a brief description.

## Formatting Rules

- Use concise, actionable language.
- Avoid jargon where possible.
- Review and update vision periodically as the project evolves.

## Mission

Produce a single, reliable bootstrap prompt that, when given to an AI agent, generates a complete production-ready project scaffold. The prompt was iteratively refined through manual stress-testing (6 independent project scaffoldings), retrospective analysis, and structured assessment — but the prompt itself is a static template, not an automated system.

## Guiding Principles

- **User-Driven Iteration**: The prompt can be stress-tested, critiqued, and refined by the user through structured feedback loops. The prompts (`retro-prompt.md`, `rubric-prompt.md`) are provided as tools — the user decides when and how to apply them.
- **Measurable Progress**: When users run the feedback loops, they score results using the objective rubric in `rubric-prompt.md`.
- **Repeatable & Transparent**: Every version is version-controlled with clear changelogs.
- **Robust**: The prompt is stress-tested across multiple independent scaffoldings before each refinement cycle, using the prompts in `prompts/` at the user's discretion.
- **Language-Agnostic**: Rules and instructions are designed to work with any programming language or tool stack.
- **DRY First**: Operational instructions live in skill files; navigational references in all other documents.
- **Zero Complexity**: The end goal is a single, reliable prompt — nothing more.

## Target Outcome

A single `bootstrap-prompt.md` file that, when given to an AI agent, produces a complete, production-ready project scaffold tailored to any configured project type, language, build system, and operational settings.
