# AGENT.md

This repository stores installable Codex skills. Treat `skills/<skill-name>/` as the source of truth.

## Required Structure

Every skill directory must contain:

- `SKILL.md`
- `agents/openai.yaml`

Optional bundled resources may live under:

- `scripts/`
- `references/`
- `assets/`

Do not reintroduce flat `*-agent-skill.md` files at the repository root.

## Editing Rules

- Keep the folder name, `SKILL.md` frontmatter `name`, and `$skill-name` prompt references consistent.
- `SKILL.md` must include valid YAML frontmatter with `name` and `description`.
- `agents/openai.yaml` should provide at least `interface.display_name`, `interface.short_description`, and `interface.default_prompt`.
- Keep skills directly installable by GitHub path, for example `skills/api-design`.
- Preserve existing skill content unless the task requires rewriting it.
- Fix malformed copied text instead of carrying broken links or truncated sentences forward.
- Avoid adding extra documentation files inside skill folders unless the skill genuinely needs `references/`.

## Root Docs

If you add, remove, or rename a skill, update:

- `README.md`
- this file if the repository workflow or constraints changed

## Validation Checklist

Before finishing:

1. Confirm every skill folder has `SKILL.md`.
2. Confirm every skill folder has `agents/openai.yaml`.
3. Validate `SKILL.md` frontmatter parses cleanly.
4. Check install paths still map cleanly to `skills/<skill-name>`.
