# AI Scaffolding Bootstrap

## Quick Start — Using the Bootstrap Prompt

The deliverable of this project is [prompts/bootstrap-prompt.md](prompts/bootstrap-prompt.md) — a single prompt you give to your AI agent to generate a complete, production-ready project scaffold.

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

---

## How This Prompt Was Built

> **Disclaimer:** This prompt was built and iteratively refined using only C/C++, CMake, and Podman Compose configurations during the self-improvement loop. However, explicit focus and care were taken to ensure the result is not limited to these selections — every rule and instruction is designed to be language- and tool-agnostic, so it works just as well for Python, Rust, TypeScript, or any other stack.

This bootstrap prompt was not hand-written — it was iteratively developed, stress-tested, and refined by the author (with AI assistance) through a structured feedback loop using the prompts in this repository.

The process generates 6 independent scaffolding projects (alpha, beta, gamma, delta, epsilon, and zeta) from the current version of the prompt, then asks the AI to critique the prompt itself. The AI identifies what worked, what failed, and suggests concrete improvements. The prompt is refined, assessed by a fresh session using an assessment rubric, and the cycle repeats until the output is consistently reliable.

---

## How the Prompt Was Built (Manual Process)

> **Important:** The 6-project stress test and feedback loops described below were **manual steps performed by the author** to iteratively refine [prompts/bootstrap-prompt.md](prompts/bootstrap-prompt.md). This scaffolding has **no mechanism** to automatically generate, test, or assess other projects. The prompts in `prompts/` are standalone templates you can use (or not use) at your discretion.

```text
 ┌───────────────────────────────────────────────────────────────┐
 │          Manual Process — Author-Driven                       │
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

The author performed these manual steps:

1. **Prompt & Rubric Creation**
   - The author designed the initial **Scaffolding Bootstrap Prompt** and **Assessment Rubric**.

2. **Scaffolding Generation (Manual)**
   - The author ran the prompt 6 independent times, producing separate scaffolding projects: `alpha/`, `beta/`, `gamma/`, `delta/`, `epsilon/`, and `zeta/`.

3. **Retrospective Analysis (Manual)**
   - The author asked an AI to critically analyze the prompt using [prompts/retro-prompt.md](prompts/retro-prompt.md), identifying what worked, what failed, and suggesting improvements.
   - The author refined the prompt based on the analysis.

4. **Independent Assessment (Manual)**
   - The author asked a fresh AI session to evaluate all 6 scaffoldings using the rubric via [prompts/rubric-prompt.md](prompts/rubric-prompt.md).

5. **Feedback & Iteration (Manual)**
   - The author fed the assessment report and retrospective insights back into the prompt, iterating until the bootstrap consistently produced high-quality results.

**You are free to repeat this process** with the prompts in `prompts/`, adapting them to your own workflow and project types. There is no automation — the prompts are your tools, and how you use them is entirely up to you.

---

## Governance

- **Agent rules**: [AGENTS.md](AGENTS.md) — mode toggle, CLI boundaries, git protocol, pre-commit checklist.
- **Architecture**: [docs/ARCHITECTURE.md](docs/ARCHITECTURE.md) — system overview, directory structure, component descriptions, and integration points.
- **Standards**: [docs/STANDARDS.md](docs/STANDARDS.md) — copyright headers, file naming, formatting.
- **Pi setup**: [docs/pi.md](docs/pi.md) — pi configuration and usage notes.
- **Skills**: All operational procedures live in [docs/skills/](docs/skills/). Each skill covers a distinct tool or concern.

---

## License

This project is licensed under the MIT License. See [LICENSE.md](LICENSE.md) for full terms.

**Copyright (c) 2026 Deniz Eren <deniz.eren@outlook.com>**

Third-party components (COMMITS.md, SKILLS.mdx, semver.md) are included under their original licenses. See [docs/THIRD-PARTY-NOTICES.md](docs/THIRD-PARTY-NOTICES.md) for attribution details.
