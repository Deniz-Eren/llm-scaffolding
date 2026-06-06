---
name: create-skill
description: Create new agent skills following the project skills specification. Use when adding new tools, workflows, or operational concerns to the skills directory.
license: MIT
metadata:
  author: llm-scaffolding
  version: "1.0"
---

# Create Skill

## Purpose

Provide step-by-step instructions for creating new agent skills in this project, following the established specification.

## Structure

Skill creation follows a structured process: plan, create, validate, and integrate.

## Formatting Rules

- Follow the SKILLS.mdx specification from `references/SKILLS.mdx`.
- Use lowercase directory names matching the skill `name` field.
- Keep SKILL.md under 500 lines.

---

## Prerequisites

1. Ensure no existing skill covers the same domain (check `docs/skills/` for overlap).
2. If two skills would share more than 30% of their instructions, merge them instead.
3. Confirm the skill is not already covered by an existing skill.

## Steps

### 1. Plan the Skill

- Determine the skill name: lowercase, alphanumeric + hyphens, 1–64 chars, no leading/trailing/consecutive hyphens.
- The name must match the directory name.
- Write a clear description (1–1024 chars) that explains what the skill does and when to use it.
- Decide which reference files, scripts, or assets are needed.

### 2. Create the Directory and SKILL.md

```bash
mkdir -p docs/skills/<skill-name>/
```

Create `docs/skills/<skill-name>/SKILL.md` with YAML frontmatter:

```markdown
---
name: <skill-name>
description: <what it does and when to use it>
license: MIT
---

# <Skill Name>

## Purpose
<One sentence describing the skill's purpose>

## Structure
<How the skill is organized>

## Formatting Rules
<Rules for using this skill>

---

<Main skill content>
```

### 3. Add Reference Files (if needed)

Create any reference, script, or asset files under the skill directory:

```
docs/skills/<skill-name>/
├── SKILL.md
├── scripts/          # Optional: executable code
├── references/       # Optional: documentation
└── assets/           # Optional: templates, resources
```

Reference files using relative paths from the skill root:

```markdown
See [the reference guide](references/REFERENCE.md) for details.
```

### 4. Validate

- Verify the skill name matches the directory name.
- Ensure the YAML frontmatter is valid.
- Check that the description is between 1–1024 characters.
- Ensure no overlap with existing skills (>30% content overlap = merge).
- If using the skills-ref validator: `skills-ref validate ./docs/skills/<skill-name>`

### 5. Integrate

- Update `docs/ARCHITECTURE.md` with the new skill in the integration points table.
- Update `docs/TASKS.md` if the skill creation was a tracked task.
- Update `docs/HISTORY.md` with the skill creation event.

### 6. Commit

```bash
git -c user.name="Deniz Eren" -c user.email="deniz.eren@outlook.com" add docs/skills/<skill-name>/
git -c user.name="Deniz Eren" -c user.email="deniz.eren@outlook.com" commit -m "scaffold: add <skill-name> skill" --no-gpg-sign
```

## Reference

- Full specification: `[references/SKILLS.mdx](references/SKILLS.mdx)`
- Copyright standards: `[STANDARDS.md](../../STANDARDS.md)`
