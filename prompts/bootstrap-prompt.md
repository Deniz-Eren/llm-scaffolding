# Scaffolding Bootstrap Prompt

## Project Overview (configure these before running)

| Attribute | Value |
| --- | --- |
| Project Name | [Insert Project Name] |
| Description | [Insert high-level project description and purpose] |
| Project Type | Software \| Documentation \| Mixed |
| Primary Language(s) | [e.g. Python, TypeScript, C++, Rust, None, Multiple: Python+TypeScript] |
| Language Standard/Version | [e.g. Python 3.12, C++20, None] |
| Target Platforms | [e.g. Linux, cross-platform, Web, None] |

---

## Project Operational Settings (configure these before running)

These settings determine which scaffolding files and skills are generated.

| Tunable | Value |
| --- | --- |
| Commit Mode | Autonomous \| HITL |
| Build System | CMake \| Make \| None \| Poetry \| npm \| Cargo \| Gradle \| ... |
| Testing Framework | Google Test \| pytest \| Jest \| None |
| Static Analysis / Linter | Clang-Tidy \| pylint \| eslint \| ruff \| None |
| Code Formatter | Clang-Format \| black \| prettier \| None |
| Build Convention | Out-of-source \| In-source \| None |
| Dev Environment | Native \| Containerized \| Auto (default) |

---

## Session Context (populated by the orchestrator — read by the agent)

> The orchestrator (user or system) fills this section before handing the prompt to the agent.
> The agent reads these fields to populate commit footers and identify itself.
> **Do NOT fill these in the Project Tunables table above — they are runtime identity, not project config.**

| Field | Value |
| --- | --- |
| Git Author Name | [Your Name] |
| Git Author Email | [your.commit@email.com] |
| Copyright Email | [your.copyright@email.com] — Email used in all copyright headers. Defaults to Git Author Email if blank. |
| Git Commit Flag | `--no-gpg-sign` |
| Agent Name | [e.g. pi-agent, opencode, claude] — Your own agent identity |
| Model Version | [e.g. 4.1, 3.7-sonnet] — The model running this session |
| Additional Tools | [e.g. Cursor, Windsurf] — Other tools used in this session, if any |

---

## Agent Scripts (pre-configured paths)

| Tunable | Value |
| --- | --- |
| Build Agent Script | `scripts/build-agent.sh` |
| Formatter Agent Script | `scripts/formatter-agent.sh` |

---

## Pre-Existing Documents

The following documents already exist in the project and must be included in the scaffolding.

For each pre-existing document:
1. Copy the file content into the destination path during Step 1. Copy the file **first**, then apply any relative link fixes only to the copy — **never edit the source file**. You must copy the content **verbatim**, with ONE strict exception: **If the destination path changes the directory depth of the document, you MUST update any relative markdown links within it so they resolve correctly.**
2. Add the document to the project chronicle with category `[DOC]`.
3. Reference it from the knowledge base or architecture document.
4. Do **NOT** add a `## License` section to pre-existing documents.
5. **CRITICAL:** Obey the ongoing modification permissions defined in the "Notes" column for all future interactions.

### How to Specify Pre-Existing Documents

Add entries to the table below before running the bootstrap. Each row declares one document to preserve. Leave the table empty if there are none.

| Document Label | Source Path | Destination Path | Notes |
| --- | --- | --- | --- |
| *Example: License* | `<path-to-your-license>/LICENSE.md` | `LICENSE.md` | Copy verbatim; IMMUTABLE (never modify) |
| *Example: Skills Spec* | `<path-to-llm-scaffolding-repo>/SKILLS.mdx` | `docs/skills/create-skill/references/SKILLS.mdx` | Copy verbatim; IMMUTABLE; use as strict blueprint for generating skills |
| *Example: Commit Rules* | `<path-to-llm-scaffolding-repo>/COMMITS.md` | `docs/skills/git/references/COMMITS.md` | Copy verbatim; fix relative links; IMMUTABLE; apply rules immediately |
| *Example: Semantic Versioning* | `<path-to-llm-scaffolding-repo>/semver.md` | `docs/skills/git/references/semver.md` | Copy verbatim; fix relative links; APPEND-ONLY during future development |
| *Example: 3rd Party* | `<path-to-llm-scaffolding-repo>/THIRD-PARTY-NOTICES.md` | `docs/THIRD-PARTY-NOTICES.md` | Copy verbatim; fix relative links; APPEND-ONLY during future development |

> **If this table is empty, proceed with bootstrap generation only.**
> **If rows are present, include and analyze those documents in Step 1 before creating any commits.**

---

You are an expert Software Architect and AI Operations Manager. Your task is to design a comprehensive, high-quality project scaffolding and documentation system optimized for autonomous CLI-based AI development (e.g. Pi Agent, Opencode).

**Project-Type Awareness (CRITICAL)**: Fully respect all values in the Overview and Tunables tables, especially `Project Type`, `Primary Language(s)`, `Build System`, and `Commit Mode`.

**Isolated Development Environment (CRITICAL)**: Every project must ship with a reproducible, isolated development environment. The environment type is determined by the `Dev Environment` tunable (default: `Auto`).

* **Environment type resolution** (applied when `Auto` or when the tunable is not set):
  * **Native** — Python only:
    * Python → `.venv/` (via `python -m venv .venv`). Generate `.python-version` for version pinning and `requirements.txt` for dependency specification.
  * **Containerized (Podman Compose)** — all other languages and stacks:
    * `docker-compose.yml` at project root with a `dev` service
    * `Dockerfile` with all build tools, compilers, linters, formatters, and test frameworks installed
    * `scripts/enter-dev.sh` (executable) to enter the dev container
    * Base image appropriate for the project's language(s)
  * **Multi-language stacks**: Always containerized regardless of individual language capabilities.

* **Generated files by environment type:**
  | Environment | Files Generated |
  |---|---|
  | Native (Python) | `.venv/` (gitignored), `requirements.txt`, `.python-version` |
  | Containerized | `docker-compose.yml`, `Dockerfile`, `scripts/enter-dev.sh` |

* **`.gitignore`** must include the isolation directory for the chosen environment type. For containerized environments, exclude build outputs and tool caches per the project's language conventions.
* **Build and test commands** in the Build Agent script must activate/use the environment (e.g., `source .venv/bin/activate && pytest` for Python native, `podman compose run dev <command>` for containerized).
* **Document the environment** in `README.md` under a `## Development Environment` section (quick-start exception: include the single command to set up the environment).
* **SKILL:** Generate `docs/skills/dev-environment/SKILL.md` documenting environment setup, activation, dependency installation, and troubleshooting.

**Hard Rules (only these are enforced):**

* **Single Source of Truth (DRY)**: Never repeat **operational** instructions (detailed commands, flags, execution sequences, procedural steps). Build steps, testing commands, git rules, formatting, etc. must live **only** in the relevant skill file under `docs/skills/`. **Navigational references** (file paths, relative links, skill indexes) are permitted and encouraged in README.md, ARCHITECTURE.md, AGENTS.md, and other documents. All non-skill files must use relative markdown links to the SSOT.
  - **README.md Quick-Start Exception:** `README.md` is permitted to contain **single-invocation** copy-pasteable commands sufficient to build, test, and run the project. A *single-invocation* command is one atomic operation: `cmake --build build`, `pytest`, or `cargo test`. Compound commands like `cmake -B build -S . && cmake --build build` count as two invocations and must be placed in skill files. Multi-step procedures, detailed flags, and troubleshooting sequences must remain in skill files. The DRY prohibition applies to all other non-skill files (including `ARCHITECTURE.md` and `AGENTS.md`).
  - **Permitted in non-skill files:** High-level protocols (e.g., "run the build agent before committing"), navigational references (e.g., `see docs/skills/build-system/SKILL.md`), governance rules (e.g., failure modes table, CLI boundaries). Single-line quick-start commands in README.md (per the exception above).
  - **Prohibited in non-skill files (except README.md quick-start):** Detailed copy-pasteable multi-step commands, tool-specific invocation flags, troubleshooting sequences.
  - **Test:** If a reader could execute the procedure directly from the document without looking up a skill file, it belongs in a skill file. (The README.md quick-start exception is the only allowed bypass.)

  - **DRY Permitted Content by File Type:**

    | Element | README.md | AGENTS.md | ARCHITECTURE.md | Other docs/\*.md |
    | --- | --- | --- | --- | --- |
    | Single-invocation build/run commands | ✓ | ✗ | ✗ | ✗ |
    | Skill file references (relative links) | ✓ | ✓ | ✓ | ✓ |
    | Governance/CLI boundary tables | ✗ | ✓ | ✗ | ✗ |
    | Failure modes table | ✗ | ✓ | ✗ | ✗ |
    | One-sentence procedure summaries | ✓ | ✓ | ✓ | ✗ |
    | Multi-step command sequences | ✗ | ✗ | ✗ | ✗ |
    | Flag-by-flag command explanations | ✗ | ✗ | ✗ | ✗ |

  - **What is a single-invocation command?** One atomic command such as `cmake --build build`, `pytest`, or `cargo test` — not a sequence of commands that requires understanding intermediate steps.

  - **Note on bootstrap prompts:** This prompt is not subject to DRY — it must contain operational commands to teach the agent. Generated skill files must not copy these commands verbatim. Instead, include context-specific examples appropriate for the skill's scope.
* **`AGENTS.md`** at root is the supreme authority. Must include all of the following:
  - [ ] Mode toggle (AUTONOMOUS / HITL)
  - [ ] Predict → Act → Verify workflow
  - [ ] Failure modes table
  - [ ] CLI execution boundaries
  - [ ] Token & context management guidelines
  - [ ] Git protocol (inline config, identity, signing rules)
  - [ ] HITL text: `WAITING FOR GPG SIGNATURE`
  - [ ] Pre-Commit Checklist with documentation maintenance requirements
    - Documentation maintenance requirements: Update `TASKS.md` (mark completed tasks with `[x] COMPLETE YYYY-MM-DD`), update `HISTORY.md` (add event entry), update `DECISIONS.md` (add ADR if new decisions made), verify copyright headers on all new/modified source files.
    - **Note:** Detailed documentation update procedures belong in `docs/skills/state-management/SKILL.md`. The Pre-Commit Checklist should reference that skill for full instructions rather than embedding the procedures here.
* **Git Protocol (STRICT)**:
  - Always use **inline** `-c user.name="..." -c user.email="..."` for every commit. Never modify local git config.
  - The committer identity (name + email) is **the same for both modes**. The Commit Mode affects only:
    - **Commit behavior**: Autonomous = proceed without pausing; HITL = pause for human confirmation before committing.
    - **Signing flag**: `--no-gpg-sign` for Autonomous; default signing behavior for HITL.
  - Every commit message must end with a blank line followed by an `Assisted-by:` footer:
    ```
    {commit message body}

    Assisted-by: {AgentName}:{ModelVersion}
    ```
    If additional tools were used, append them with ` + `:
    ```
    Assisted-by: {AgentName}:{ModelVersion} + {Tool1} + {Tool2}
    ```
    **Example (no extra tools):**
    ```
    scaffold: initial project structure

    Assisted-by: pi-agent:4.1
    ```
    **Example (with extra tools):**
    ```
    scaffold: add clang-tidy configuration

    Assisted-by: pi-agent:4.1 + Cursor
    ```
    Replace placeholders with actual values; never include literal brackets. Always end with a blank line before the footer.
* **Root Files Requirement**: `README.md` **MUST** exist at the project root. It must contain a high-level project overview, quick-start guidance, a `## Development Environment` section (with the single command to set up the environment), and relative links to `AGENTS.md`, `ARCHITECTURE.md`, and key skills. Follow DRY principles.
* **Skills Philosophy**: Generate one skill per distinct tool or operational concern. Each gets its own bare lowercase tool folder containing `SKILL.md`. **Avoid domain overlap**: each skill should own a distinct tool invocation or workflow step. If two skills share more than 30% of their instructions, merge them. **Always create these skills** (in addition to tool-specific skills): `create-skill/` (meta-skill, always required) and `state-management/` (owns TASKS.md, HISTORY.md, DECISIONS.md update procedures — always required). Create a skill for every configured tool. Do not create skills for concerns with no associated tooling (e.g., "deploy" if no deployment tool is configured). Integrate established standards wherever applicable. Strictly follow any provided `SKILLS.mdx` blueprint.
* **Tool Configuration Files**: Generate configuration files for configured tools. Use widely-adopted defaults as a starting point. If a tool has a recognized "recommended" or "default" configuration, use it. Document any deviations from defaults in `DECISIONS.md`.
* **Tool Version Compatibility (STRICT)**: Before generating any tool configuration file, the agent MUST check the installed version of each configured tool by running its `--version` (or `--help` for tools without version flags) command. Every setting in the generated config must be verified against that version. If a feature or option is unavailable, replace it with the closest compatible alternative and record the deviation in `DECISIONS.md`.
  - Map tunables to version commands: `Clang-Format` → `clang-format --version`, `Clang-Tidy` → `clang-tidy --version`, `CMake` → `cmake --version`, `black` → `black --version`, `prettier` → `prettier --version`, `eslint` → `eslint --version`, `rustfmt` → `rustfmt --version`, `cargo` → `cargo --version`, `pytest` → `pytest --version`, `poetry` → `poetry --version`, `npm` → `npm --version`. Add more as needed.
  - **Tool Not Installed:** If `--version` returns "command not found" (exit code 127), do NOT create the tool's configuration file. Create a SKILL.md documenting the tool and noting that it must be installed before use. Record the absence in `DECISIONS.md`.
  - If no version command is available, use best available defaults and note the uncertainty in `DECISIONS.md`.
  - **Config Testing Loop:** `--version` alone is insufficient for config-file-based tools (e.g., `.clang-format`, `.eslintrc`, `black.toml`). After generating a config, you MUST test it by running the tool on a sample file. If the tool rejects the config, remove options one at a time until the tool accepts it, then add them back incrementally, testing after each addition. Record all removed or modified options in `DECISIONS.md`. If the tool has no `--version`, generate a zero-option config (just comments) and note the uncertainty.
  - **Minimal Config First:** Generate the smallest valid config for each tool (zero or one option, or a single style preset like `BasedOnStyle: LLVM`). Only add advanced options after confirming they are accepted by the installed tool. A config that the tool rejects entirely is a scaffolding failure and must be treated as such.
  - **Config Complexity Target:** A minimal valid config should contain at most **3–5 options** beyond the base style. **Counting rules:** `BasedOnStyle: <preset>` = 1 option; a scalar value (e.g., `ColumnLimit: 100`) = 1 option; a check list (e.g., `checks=llvm*,modernize-*`) = 1 option regardless of how many individual checks it contains. For tools with a recognized default style (e.g., `BasedOnStyle: LLVM`), start there and add at most 1–2 project-specific options (e.g., `ColumnLimit: 100`). Do not add more options unless there is a clear justification.
* **Documentation headers**: Every **generated** markdown file under the `docs/` folder must begin with these three sections in order:
  1. `## Purpose`
  2. `## Structure`
  3. `## Formatting Rules`
  **Applies to:** ALL generated `.md` files under `docs/`, including `TASKS.md`, `HISTORY.md`, `VISION.md`, `DECISIONS.md`, `STANDARDS.md`, `ARCHITECTURE.md`, and any other generated files.
  **Excludes:** Pre-existing/IMMUTABLE documents copied verbatim (they retain their original content).
  - **Adaptation clause:** If the standard section names don't fit a document's natural structure, use the exact strings `## Purpose`, `## Structure`, `## Formatting Rules` as the first-level headings.

    **VISION.md specifically:** VISION.md naturally contains a purpose/mission section in its content body. Rename that content section to `## Mission` (not `## Purpose`) to avoid duplicate headings. The required three headers must still appear as the first content in the file.

    **General adaptation:** If any other document's intrinsic content would use one of the exact strings `## Purpose`, `## Structure`, or `## Formatting Rules` as a section name, rename the content section (e.g., `## Purpose` → `## Goals`) and keep the required header string.

    **Placement rule:** These three headings must appear **only at the top** of the file as the first content. If you need to document the format itself (e.g., in STANDARDS.md), use a fenced code block — not live headings.

    **Verification:** Each document must have exactly one of each required heading. The self-verification script checks for exact heading strings `^## Purpose`, `^## Structure`, `^## Formatting Rules` (excluding lines inside fenced code blocks).

**Copyright & STANDARDS (CRITICAL)**:
- If `LICENSE.md` is provided, extract the exact copyright notice during Step 1 and state it.
- Create `docs/STANDARDS.md` defining exact copyright header formats.
- **Every file that supports comment blocks** must include the project copyright header at the top:
  - Source files (`*.cpp`, `*.hpp`, `*.h`, `*.c`, `*.rs`, `*.py`, `*.js`, `*.ts`, etc.): use language-appropriate comment syntax.
  - Build files (`CMakeLists.txt`, `Makefile`, `package.json`, `Cargo.toml`, `build.gradle`, `Dockerfile`, etc.): use the appropriate comment syntax for that tool.
  - Shell scripts (`*.sh`, `*.bash`): `# Copyright ...`
  - Configuration files (`.clang-format`, `.clang-tidy`, `*.yaml`, `*.yml`, `*.toml`, etc.): if the format supports comments, add the copyright header. **Excludes `.gitignore`** (where it clutters the file without adding value).
  - Excludes markdown documents.
- Add a `## License` section to `README.md`.

**File Naming (strict)**:
- **Scaffolding-enforcing** non-skill files under `docs/` (TASKS, HISTORY, VISION, DECISIONS, STANDARDS, ARCHITECTURE, THIRD-PARTY-NOTICES): UPPERCASE names. Prefer single words or hyphenated compounds. Do not use spaces.
- Other `docs/` files (user guides, references, etc.): no UPPERCASE requirement.
- Skills: bare lowercase tool folders + `SKILL.md` exactly.

**Project Name Collision Check**:
- Before generating source files, check whether the configured `Project Name` shadows or conflicts with common library symbols in the target language(s). If the name conflicts with a widely-used symbol (e.g., `json`, `uuid`, `yaml`, `async`, `result`, `gamma` in C/C++), append a language-appropriate suffix (`_lib`, `_core`, `lib.`, etc.) to the internal namespace/module name while keeping the project name unchanged in build files and `README.md`. Record the decision in `DECISIONS.md`.

**Build Integrity (STRICT)**:
- The project must always be in a buildable state. Never stage or commit scaffolding that doesn't compile and pass all tests. If the build or test run fails, diagnose the root cause, fix it, and re-run. Do not proceed to the next step or make a commit until the build succeeds. If the failure is caused by the scaffolding itself (e.g., incorrect config, wrong feature flags), fix the scaffolding — not the boilerplate.
- **Invalid tool configs are build failures:** A configuration file (e.g., `.clang-format`) that causes the tool to crash or refuse operation must be fixed before proceeding. This is treated the same as a build failure.
- **Atomic commit in failure scenarios:** An "atomic commit" includes all files necessary for the step to be in a complete, buildable state. If a build failure requires an intermediate fix commit, that fix may be committed separately — but the scaffolding is not considered "complete" until the fix is integrated and verified.

**Formatter/Build Script Scope (STRICT)**:
- The **Formatter Agent script** (`formatter-agent.sh`) handles **formatting only** — it runs the code formatter tool. It must NOT include static analysis/lint checks; those belong in the Build Agent script.
- The **Build Agent script** (`build-agent.sh`) handles **build, test, and static analysis** — it runs the build system, tests, and optional static analysis tools (e.g., clang-tidy, pylint).
- When creating the Build Agent and Formatter Agent scripts, they MUST:
  - Only scan project source directories. Use the community-standard source layout for the configured language (e.g., `src/`, `tests/`, and language-specific standard directories like `include/` for C/C++ or `internal/` for Go). Do not invent non-standard directory names. For any language, follow the conventions documented in the build-system SKILL.md.
  - Explicitly exclude `build/`, `.git/`, `node_modules/`, `__pycache__/`, `target/`, `vendor/`, and any other common build/cache directories
  - Exit 0 on success, non-zero on failure (build failure, test failure, or formatting violations)
  - **`find` command note:** When using `find` with `-o` operators, always group name clauses in parentheses for correct precedence: `find "$dir" \( -name '*.cpp' -o -name '*.h' -o -name '*.hpp' \) -print0`

---

**IMMEDIATE EXECUTION PROTOCOL (CRITICAL)**

Operate according to the configured **Commit Mode**.
- If `Autonomous`: run without pausing for human input.
- If `HITL`: pause and wait for human confirmation where appropriate.

Follow the steps strictly in order.

**Step 1: Initialization & Pre-Existing Documents**
* Initialize the Git repository.
* Create a comprehensive `.gitignore` tailored to the project. **Generated `.gitignore` must include:**
  - Build output: `build/`, `CMakeCache.txt`, `CMakeFiles/`, `cmake_install.cmake`
  - Language artifacts: `*.o`, `*.a`, `*.so`, `*.pyc`, `__pycache__/`, `node_modules/`, `target/`, `bin/`, `obj/`
  - Development environment: `.venv/`
  - IDE files: `.idea/`, `.vscode/`, `*.swp`, `*.suo`
  - OS files: `.DS_Store`, `Thumbs.db`
  - **Do NOT use broad glob patterns** like `build-*` that may match project directories. **Do NOT exclude `include/`, `src/`, `tests/`, or source code files.**
* Copy and process all Pre-Existing Documents (fix relative links if needed). To fix relative links: calculate the path depth delta between source and destination directories. If a file moves from depth A to depth B, prepend `(B - A)` copies of `../` to each relative reference. If moving to a shallower path, strip that many leading `../` segments.
* If LICENSE.md was provided, explicitly state the extracted copyright string.
* Make an atomic commit using the configured git identity and the appropriate signing flag for the Commit Mode.
* Proceed to Step 2.

**Step 2: Planning & State Management**
* Create state tracking documents under `docs/`: `TASKS.md`, `HISTORY.md`, `VISION.md`, `DECISIONS.md`.
* Record initial decisions.
* Make an atomic commit.
* Proceed to Step 3.

**Step 3: Governance & Core Architecture**
* Create `AGENTS.md` at root with all required governance content and Pre-Commit Checklist.
* Create `README.md` at root with high-level overview, quick-start guidance, relative links, and a `## License` section.
* If Build System is specified, create root build file(s) and relevant tool config files (e.g. `.clang-format`, `.clang-tidy`).
* **Dev Environment Setup (always run):** Determine the environment type per the rules above. Generate all required dev environment setup files:
  - **Native (Python):** Create `.python-version` and `requirements.txt` for dependency specification.
  - **Containerized (all other languages and stacks):** Generate `docker-compose.yml` with a `dev` service, `Dockerfile` that installs all tools declared in the tunables (build system, compilers, linters, formatters, test frameworks), and `scripts/enter-dev.sh` (executable) to interactively enter the container. The `Dockerfile` should use a base image appropriate for the project's language(s) (e.g., `ubuntu:24.04` with compilers and toolchains installed for C/C++, or the relevant distro image for other languages).
  - **Mixed stacks:** Always containerized — generate a single `docker-compose.yml` / `Dockerfile` that handles all languages.
  - **Record the decision** in `DECISIONS.md` under an entry explaining why the chosen environment type was selected.
* If Build System is specified, tool config files (e.g. `.clang-format`, `.clang-tidy`): Generate a minimal valid config first (zero or one option, or a single style preset). Test the config against the installed tool. Only add advanced options after verifying they are accepted. If a config is rejected, strip options until accepted, then add back incrementally.
  - **Config Testing Timing for Step 3:** Since no project source files exist in Step 3, test configs against temporary inline samples. For clang-format: `echo 'int x;' | clang-format -style=file`. For clang-tidy: `echo 'int x;' > /tmp/test.cpp && clang-tidy /tmp/test.cpp --checks=llvm*`. Full integration testing occurs in Step 5.
* Create architectural documentation under `docs/`.
* Make an atomic commit.
* Proceed to Step 4.

**Step 4: Knowledge Base & Skills Directory**
* Create `docs/skills/` with comprehensive relevant tool folders and `SKILL.md` files (including meta-skill in `create-skill/`).
* **Always create `docs/skills/dev-environment/SKILL.md`** documenting: how to set up the development environment, how to activate it, how to install project dependencies, how to use the build/test/formatter tools within the environment, and troubleshooting steps. For containerized environments, document how to enter the container and how to build/update the image.
* Create `STANDARDS.md` with full copyright and file creation rules.
* Ensure the git skill documents the `Commit Mode` and `Assisted-by:` footer convention.
* If Build System specified: create the Build Agent script (executable, exits non-zero on failure). The script must:
  - Activate the development environment before running any tool commands (e.g., `source .venv/bin/activate` for Python native, `podman compose run dev` for all containerized environments).
  - Scan only source directories and exclude build/cache dirs (`build/`, `.git/`, `node_modules/`, `__pycache__/`, `target/`, `vendor/`).
* If Code Formatter specified: create the Formatter Agent script (executable, exits non-zero on failure). The script must activate the development environment before running the formatter and scan only source directories and exclude build/cache dirs.
* Make an atomic commit.
* Proceed to Step 5.

**Step 5: Boilerplate & Finalization**

**Development Environment Setup** (always run):
- Ensure the dev environment is fully set up and functional:
  - **Native (Python):** Create the virtual environment (`python -m venv .venv && source .venv/bin/activate`). Install project dependencies from `requirements.txt` (`pip install -r requirements.txt`). Verify with a smoke test (e.g., `python -c "import <project_name>"`).
  - **Containerized:** Build the image (`podman compose build dev`) and verify the dev service starts (`podman compose run dev <language-specific-smoke-test>`). Confirm all declared tools (compilers, linters, formatters, test frameworks) are present.
  - **Mixed stacks:** Always containerized — build the image and verify.
- Update `README.md` with a `## Development Environment` section (quick-start exception: include the single command to set up the environment).

**Boilerplate Requirements** (if Project Type includes software development):
- **Version source of truth**: The project version (e.g., `0.1.0`) is defined **only** in the Build System configuration file(s). It must never be duplicated in source code, headers, or documentation.
- **Version injection**: Pass the version to the software using the build system's native best-practice mechanism:
  - CMake: configure a header template (`<name>_config.h.in` → `<name>_config.h`) via `configure_file()`; place it in the `include/` path. Use `@PROJECT_VERSION@` (NOT `<name>_VERSION_STRING`, which does not exist in CMake). Available variables include: `@PROJECT_VERSION@`, `@PROJECT_NAME@`, `@PROJECT_VERSION_MAJOR@`, `@PROJECT_VERSION_MINOR@`, `@PROJECT_VERSION_PATCH@`.
  - **Version Injection by Build System:**
    | Build System | Version Source | Injection Mechanism | Notes |
    |---|---|---|---|
    | CMake | `project(... VERSION ...)` | `configure_file()` → `<name>_config.h` | Use `@PROJECT_VERSION@`, NOT `<name>_VERSION_STRING` |
    | Cargo | `[package] version` | `env!("CARGO_PKG_VERSION")` at compile time | No config header needed |
    | npm | `package.json "version"` | Runtime `require('./package.json').version` or build script | |
    | Poetry/Python | `pyproject.toml version` | `importlib.metadata.version()` or generated `__version__.py` | |
  - Other build systems: use the equivalent native mechanism (e.g., define flags via `add_definitions()`, set environment variables, generate source files)
- **Binary interface**: The main executable must respond to `-h` (or `--help`) with version information
- **Minimal structure**: At minimum, create:
  - One library target with at least one exported class/function
  - One executable target
  - At least one passing test per exported API surface (cover initialization, a core feature, and shutdown/cleanup)
  - **Idiomatic patterns for the language:**
    - C/C++: header/source split with namespace; public API in `include/`, implementation in `src/`
    - Python: flat `src/` package with `__init__.py` exports; or src-layout with `src/<package>/`
    - JavaScript/TypeScript: `src/` with barrel exports; use ES modules
    - Rust: `src/` with `lib.rs` (library) and `main.rs` (binary)
    - Go: `cmd/`, `pkg/`, `internal/` directory structure
- **include/ directory**: Only create if the project has a public API surface. Place public headers (and version-injected config headers) there.

**Build & Test Verification**:
- Run the Build Agent script
- If it fails: diagnose the cause, fix the source of the failure, and re-run. **Do not make a final commit until the build succeeds and all tests pass**
- Run the Formatter Agent and verify no formatting changes are needed

**Finalize**:
- Update all state documents (mark bootstrap tasks as `[x] COMPLETE` with today's date)
- Make a final atomic commit
- Report readiness

---

**SELF-VERIFICATION (Mandatory — run these commands and report results)**

```bash
# Check three-section headers in all generated docs
# Exclude lines inside fenced code blocks (grep -v '^```') to avoid false positives
for f in docs/DECISIONS.md docs/HISTORY.md docs/STANDARDS.md docs/TASKS.md docs/VISION.md docs/ARCHITECTURE.md; do
  if [ -f "$f" ]; then
    purposes=$(grep -v '^```' "$f" | grep -c '^## Purpose' 2>/dev/null || echo 0)
    structures=$(grep -v '^```' "$f" | grep -c '^## Structure' 2>/dev/null || echo 0)
    formatting=$(grep -v '^```' "$f" | grep -c '^## Formatting Rules' 2>/dev/null || echo 0)
    echo "$f: $purposes purpose, $structures structure, $formatting formatting"
    if [ "$purposes" -ne 1 ] || [ "$structures" -ne 1 ] || [ "$formatting" -ne 1 ]; then
      echo "  ERROR: Expected exactly 1 of each heading in $f"
    fi
  else
    echo "$f: MISSING"
  fi
done

# Check build + tests (only if Build System is configured)
if [ "$BUILD_SYSTEM" != "None" ] && [ -n "$BUILD_SYSTEM" ]; then
  ./scripts/build-agent.sh && echo "BUILD: PASS" || { echo "BUILD: FAIL"; exit 1; }
else
  echo "BUILD: SKIP (no build system configured)"
fi

# Check formatting (only if Code Formatter is configured)
if [ "$CODE_FORMATTER" != "None" ] && [ -n "$CODE_FORMATTER" ]; then
  ./scripts/formatter-agent.sh && echo "FORMAT: PASS" || { echo "FORMAT: FAIL"; exit 1; }
else
  echo "FORMAT: SKIP (no formatter configured)"
fi

# Check git status (should be 0 = clean)
echo "UNTRACKED/MODIFIED: $(git status --short | wc -l)"

# Check Assisted-by footers
echo "Assisted-by footers: $(git log --format='%B' | grep -c 'Assisted-by')"

# Check commit count
echo "Total commits: $(git log --oneline | wc -l)"

# Check for duplicate ADR blocks in DECISIONS.md
if [ -f "docs/DECISIONS.md" ]; then
  duplicates=$(grep -c '^## Context' docs/DECISIONS.md 2>/dev/null || echo 0)
  echo "ADR context blocks in DECISIONS.md: $duplicates"
fi

# Check dev environment skill and README section
if [ -f "docs/skills/dev-environment/SKILL.md" ]; then
  echo "DEV-ENV SKILL: PRESENT"
else
  echo "DEV-ENV SKILL: MISSING"
fi
if grep -q '## Development Environment' README.md 2>/dev/null; then
  echo "DEV-ENV README SECTION: PRESENT"
else
  echo "DEV-ENV README SECTION: MISSING"
fi
```

Then verify manually:
* Commit Mode correctly respected during bootstrap and used for all commits
* Strict Git Protocol followed (inline -c, correct committer per Commit Mode, `Assisted-by:` footer)
* DRY principle upheld (no duplicated commands outside skill files)
* Comprehensive relevant skills created (non-overlapping domains)
* `docs/skills/dev-environment/SKILL.md` exists and documents the environment setup
* Tool configuration files generated where applicable (tools that are installed)
* `README.md` exists at root with a `## Development Environment` section
* All `docs/` markdown files have the three required header sections (verified by the for-loop above)
* Nomenclature is correct (scaffolding-enforcing docs use UPPERCASE, single words or hyphenated compounds preferred)
* STANDARDS.md exists with exact copyright rules from LICENSE (if provided)
* Git skill documents Commit Mode and Assisted-by convention
* Project structure matches declared Project Type and Tunables
* Development environment is fully functional (native env activated or container image built)
* Clean git status and successful build (if applicable) and formatting (if applicable)

**End your response with a clear summary of the scaffolding created and recommended next steps for the user.**
