# agent-skills

Installable Codex skills packaged as standalone folders under `skills/`.

Each skill is structured so it can be installed directly from this repository with a GitHub repo path such as `skills/api-design`.

## Repository Layout

```text
skills/
  <skill-name>/
    SKILL.md
    agents/
      openai.yaml
```

## Available Skills

- `api-design`: REST and GraphQL API design, review, and consistency guidance.
- `app-docs`: README writing, docstrings, and implementation-grounded documentation.
- `bem-styling`: BEM-based UI styling and CSS class naming guidance.
- `conventional-commits`: Conventional Commit message drafting and review.
- `engineering`: General engineering standards for code quality and release readiness.
- `fullstack-developer`: End-to-end full-stack web application guidance.
- `fullstack-stacks`: Opinionated stack selection for web and backend projects.

## Install a Skill

From Codex's built-in installer:

```bash
python3 ~/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py \
  --repo javiguerra144/agent-skills \
  --path skills/api-design
```

You can replace `skills/api-design` with any skill path from this repository.

After installing a skill, restart Codex so it picks up the new skill.

## Add or Update Skills

When adding a new skill:

1. Create `skills/<skill-name>/SKILL.md`.
2. Add YAML frontmatter with `name` and `description`.
3. Create `skills/<skill-name>/agents/openai.yaml`.
4. Keep the folder name, frontmatter `name`, and `$skill-name` references aligned.
5. If the skill needs bundled files, use `scripts/`, `references/`, or `assets/`.

This repository intentionally stores skills as installable directories, not as flat root-level markdown files.
