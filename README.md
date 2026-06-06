# AI Scaffolding Bootstrap

## Quick Start — Using the Bootstrap Prompt

The deliverable of this project is `prompts/bootstrap-prompt.md` — a single prompt you give to your AI agent to generate a complete, production-ready project scaffold.

### How to Use It

1. **Configure the tunable sections.** The tables at the top of the prompt (`Project Overview` and `Project Operational Settings`) let you define your project name, languages, build system, testing framework, and more. Fill these in with your desired settings before running the prompt.

2. **Configure pre-existing documents.** If you have files that need to be preserved and integrated into the scaffold (licenses, skill blueprints, commit rules, etc.), add entries to the `Pre-Existing Documents` table with their `Source Path` and `Destination Path`. The agent will copy them verbatim and apply any needed relative link fixes.

3. **Recommended: wire up the example documents.** The `Pre-Existing Documents` table ships with sample entries prefixed with `*Example: *`. Delete the `Example: ` prefix from any of these rows and set their `Source Path` to point to the matching documents in this repository. This repository already includes several specification documents that govern how the scaffold is built:

- `docs/COMMITS.md` — Defines commit message rules (Conventional Commits specification).
- `docs/SKILLS.mdx` — Specifies how skill files should be structured (headers, formatting rules).
- `docs/semver.md` — Defines the semantic versioning scheme to follow.
- `docs/THIRD-PARTY-NOTICES.md` — Template for tracking third-party dependencies and licenses; also contains the above specification documents.

The prompt endorses specification-based working — even for specifying how skills are created. Point these example rows to the matching documents, and the prompt will follow your specifications when generating the scaffold, producing skill files, commit history, versioning, and dependency tracking that all conform to your rules.

That's all. Run the prompt, and your AI agent will produce a full project structure with governance, skills, tool configs, dev environment, and boilerplate — all tailored to your configuration.

---

## Development Environment

This project is **Documentation-only** — no build system, no source code, and no development environment setup is required.

No commands are needed to set up a development environment for this project.

> For software projects with a build system, see `[docs/skills/dev-environment/SKILL.md](docs/skills/dev-environment/SKILL.md)` for environment setup procedures.

---

## How This Prompt Was Built

> **Disclaimer:** This prompt was built and iteratively refined using only C/C++, CMake, and Podman Compose configurations during the self-improvement loop. However, explicit focus and care were taken to ensure the result is not limited to these selections — every rule and instruction is designed to be language- and tool-agnostic, so it works just as well for Python, Rust, TypeScript, or any other stack.

This bootstrap prompt was not hand-written — it was iteratively developed, stress-tested, and refined entirely by a local AI using a structured self-improvement loop.

The process generates 6 independent scaffolding projects (alpha, beta, gamma, delta, epsilon, and zeta) from the current version of the prompt, then asks the AI to critique the prompt itself. The AI identifies what worked, what failed, and suggests concrete improvements. The prompt is refined, assessed by a fresh session using an assessment rubric, and the cycle repeats until the output is consistently reliable.

---

## Development Process

```text
 ┌───────────────────────────────────────────────────────────────┐
 │                Local AI — All Phases                          │
 │                                                               │
 │  ┌──────────────┐    ┌───────────────┐    ┌────────────────┐  │
 │  │  Create &    │───▶│  Generate 6   │───▶│  Retrospective │  │
 │  │  Refine      │    │  Scaffoldings │    │  Analysis      │  │
 │  │  Prompt &    │    │  (alpha→zeta) │    │  (critique     │  │
 │  │  Rubric      │    │               │    │   prompt)      │  │
 │  └──────────────┘    └───────────────┘    └────────┬───────┘  │
 │         ▲                                          │          │
 │         │                                         Refine      │
 │         │                                          │          │
 │         │                                          ▼          │
 │         │                            ┌──────────────────┐     │
 │         │                            │  Fresh Assessment│     │
 │         │                            │  (blindly score  │     │
 │         │                            │   all 6 with     │     │
 │         │                            │   the rubric)    │     │
 │         │                            └────────┬─────────┘     │
 │         │                                     │               │
 │         └─────────────────────────────────────┘               │
 │                                                               │
 └───────────────────────────────────────────────────────────────┘
```

### Process Steps

1. **Prompt & Rubric Creation**
   - The local AI designs the initial **Scaffolding Bootstrap Prompt** and **Assessment Rubric** — no human co-authoring.

2. **Scaffolding Generation**
   - The current prompt is run 6 independent times to create separate scaffolding projects: `alpha/`, `beta/`, `gamma/`, `delta/`, `epsilon/`, and `zeta/`.

3. **Retrospective Analysis**
   - The same AI is asked to critically analyze the prompt it was given — identifying what worked, what failed, and suggesting improvements (using the prompt `./prompts/retro-prompt.md`).
   - The AI refines the prompt based on this self-critique.

4. **Independent Assessment**
   - A fresh session of the local AI evaluates all 6 scaffoldings using the Assessment Rubric and produces a detailed report (using the prompt `./prompts/rubric-prompt.md`).

5. **Feedback & Iteration Loop**
   - The assessment report and retrospective insights are fed back. The AI reviews results, identifies remaining weaknesses, and further refines the prompt and/or rubric.
   - The cycle repeats until the bootstrap consistently produces high-quality, production-ready scaffoldings.

---

## Repository Structure

```
/
├── .gitignore
├── README.md
├── AGENTS.md              ← AI agent governance (mode toggle, git protocol, checklist)
├── prompts/
│   ├── bootstrap-prompt.md ← The scaffolding bootstrap prompt (use this)
│   ├── retro-prompt.md     ← Retrospective analysis template
│   └── rubric-prompt.md    ← Assessment rubric template
├── docs/
│   ├── THIRD-PARTY-NOTICES.md
│   ├── TASKS.md            ← Task tracking with completion dates
│   ├── HISTORY.md          ← Project chronicle
│   ├── VISION.md           ← Mission and guiding principles
│   ├── DECISIONS.md        ← Architectural Decision Records (ADRs)
│   ├── STANDARDS.md        ← Copyright and file creation standards
│   ├── SKILLS.mdx          ← Original skills spec (source, immutable)
│   ├── COMMITS.md          ← Original commits spec (source, immutable)
│   ├── semver.md           ← Original semver spec (source, immutable)
│   └── skills/
│       ├── create-skill/   ← Meta-skill for creating new skills
│       │   └── references/ ← Reference materials
│       ├── dev-environment/← Development environment setup
│       ├── git/            ← Git conventions and references
│       │   └── references/ ← Reference materials
│       └── state-management/ ← TASKS, HISTORY, DECISIONS update procedures
```

---

## Governance

- **Agent rules**: `[AGENTS.md](AGENTS.md)` — mode toggle, CLI boundaries, git protocol, pre-commit checklist.
- **Architecture**: `[docs/ARCHITECTURE.md](docs/ARCHITECTURE.md)` — project structure and design rationale.
- **Standards**: `[docs/STANDARDS.md](docs/STANDARDS.md)` — copyright headers, file naming, formatting.
- **Skills**: All operational procedures live in `[docs/skills/](docs/skills/)`. Each skill covers a distinct tool or concern.

---

## License

This project is licensed under the MIT License. See `LICENSE.md` for full terms.

**Copyright (c) 2026 Deniz Eren <deniz.eren@outlook.com>**

Third-party components (COMMITS.md, SKILLS.mdx, semver.md) are included under their original licenses. See [docs/THIRD-PARTY-NOTICES.md](docs/THIRD-PARTY-NOTICES.md) for attribution details.
