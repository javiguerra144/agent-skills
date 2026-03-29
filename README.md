# agent-skills

Installable Codex skills packaged as standalone folders under `skills/`.

Each skill is structured so it can be installed directly from this repository with a GitHub repo path such as `skills/documentation-generation`.

## Repository Layout

```text
skills/
  <skill-name>/
    SKILL.md
    agents/
      openai.yaml
    references/        # optional
      *.md
```

## Available Skills

- `app-docs`: README writing, docstrings, and implementation-grounded documentation.
- `backend-development`: Backend architecture, APIs, GraphQL, microservices, CQRS, event sourcing, security, performance, and workflow orchestration guidance.
- `bem-styling`: BEM-based UI styling and CSS class naming guidance.
- `cicd-automation`: CI/CD pipeline design, workflow automation, secrets handling, Kubernetes delivery, and DevOps troubleshooting.
- `cli-developer`: CLI design and implementation guidance for Node.js, Python, and Go, including UX, flags, prompts, and shell completions.
- `conventional-commits`: Conventional Commit message drafting and review.
- `django-expert`: Django and DRF guidance for models, serializers, viewsets, authentication, testing, and ORM query optimization.
- `documentation-generation`: Technical docs, ADRs, changelogs, OpenAPI specs, tutorials, references, Mermaid diagrams, and documentation workflow guidance.
- `developer-essentials`: Cross-cutting engineering workflow guidance for auth, debugging, code review, E2E, errors, git, monorepos, builds, and SQL optimization.
- `engineering`: General engineering standards for code quality and release readiness.
- `flutter-expert`: Flutter and Dart guidance for widgets, Riverpod or Bloc state management, GoRouter navigation, project structure, and performance optimization.
- `golang-pro`: Idiomatic Go guidance for concurrency, interfaces, generics, project structure, testing, and production-grade microservices.
- `html-css-refactor`: Refactor existing HTML into semantic markup or React, Vue, or Angular output with CSS or SASS, CSS variables, responsive layout improvements, and UI polish guided by the `ui-design` skill.
- `javascript-typescript`: Modern JavaScript and TypeScript guidance, testing, backend patterns, and scaffolding references.
- `kotlin-specialist`: Idiomatic Kotlin guidance for coroutines, Flow, Jetpack Compose, Ktor, DSL design, and Kotlin Multiplatform architecture.
- `nextjs-developer`: Next.js App Router guidance for server components, server actions, data fetching, SEO metadata, deployment, and server-first rendering patterns.
- `pandas-pro`: Pandas guidance for DataFrame manipulation, data cleaning, aggregation, merging, and performance optimization on large datasets.
- `playwright-expert`: Playwright end-to-end testing guidance for selectors, page objects, API mocking, configuration, and flaky-test debugging.
- `python-development`: Modern Python development guidance for Django, FastAPI, async patterns, testing, typing, packaging, observability, resilience, and project scaffolding.
- `react-expert`: Modern React and Next.js guidance for React 19, Server Components, hooks, state management, performance, testing, and class migrations.
- `react-native-expert`: React Native and Expo guidance for navigation, platform-specific handling, list optimization, storage hooks, and project structure.
- `rust-engineer`: Idiomatic Rust guidance for ownership, borrowing, traits, async Tokio code, error handling, testing, and systems programming.
- `skill-selector`: Meta-skill routing that recommends the best matching skill or skill combination from this repository.
- `sql-pro`: SQL guidance for query tuning, schema design, window functions, execution-plan analysis, indexing, and dialect-specific query migration.
- `using-git-worktrees`: Safe git worktree setup for isolated feature work, including directory selection, ignore verification, setup, and baseline checks.
- `ui-design`: UI and UX design guidance for design systems, accessibility, responsive layouts, web and mobile patterns, interaction design, and review workflows.
- `vue-expert-js`: Vue 3 JavaScript-only guidance using Composition API plus JSDoc typing, composables, state management, and testing patterns.
- `fullstack-stacks`: Opinionated stack selection for web and backend projects.

## Install a Skill

From Codex's built-in installer:

```bash
python3 ~/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py \
  --repo javiguerra144/agent-skills \
  --path skills/documentation-generation
```

You can replace `skills/documentation-generation` with any skill path from this repository.

After installing a skill, restart Codex so it picks up the new skill.

## Install as a Git Submodule

If you want to make the whole library available as project-local skills, you can add this repository as a git submodule at `.codex`:

```bash
git submodule add https://github.com/javiguerra144/agent-skills.git .codex
git submodule update --init --recursive
```

That produces a layout like this:

```text
.codex/
  README.md
  skills/
    documentation-generation/
    react-expert/
    ...
```

Codex can then discover the skills from `.codex/skills`.

If your project already has files under `.codex`, do not replace that directory with this submodule. In that case, prefer the built-in installer above, or vendor the repository somewhere else and copy or link only the skill folders you need into `.codex/skills`.

## Add or Update Skills

When adding a new skill:

1. Create `skills/<skill-name>/SKILL.md`.
2. Add YAML frontmatter with `name` and `description`.
3. Create `skills/<skill-name>/agents/openai.yaml`.
4. Keep the folder name, frontmatter `name`, and `$skill-name` references aligned.
5. If the skill needs bundled files, use `scripts/`, `references/`, or `assets/` as needed.

This repository intentionally stores skills as installable directories, not as flat root-level markdown files.
