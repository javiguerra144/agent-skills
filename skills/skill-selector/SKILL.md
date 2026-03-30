---
name: "skill-selector"
description: "Use when the user asks which skill to use, wants help routing a task to one or more skills in this repository, or provides a task description and needs the best matching skill or skill combination."
---

# Skill Selector

Use this skill when the task is meta-level skill routing rather than direct implementation. The goal is to map a user request to the smallest effective set of skills from this repository.

## Core Workflow

1. Identify the primary outcome the user wants.
2. Pick the most specific matching skill first.
3. Add at most one or two supporting skills when the task clearly spans multiple domains.
4. Prefer focused skills over broad bundles when both could apply.
5. Explain the recommendation in plain language with a short reason for each skill.

## Selection Rules

- Recommend one skill by default.
- Recommend multiple skills only when the request has distinct concerns, such as framework plus design, or implementation plus docs.
- Prefer `git-repository-management` for repository hygiene, branch workflow, history edits, recovery, or commit-process questions that span more than one Git concern.
- Prefer `developer-essentials` for broad engineering workflow problems when no narrower skill is a better fit.
- Prefer `engineering` for general quality, maintainability, and release-readiness guidance.
- Prefer `documentation-generation` for formal technical docs and `app-docs` for README and code documentation.
- If the request is mostly stack choice, prefer `fullstack-stacks` instead of a framework-specific skill.
- If the request already names a framework or language, prefer the corresponding specialist skill.

## Routing Map

- `app-docs` -> README writing, docstrings, code comments, and implementation-grounded app documentation.
- `backend-development` -> backend architecture, APIs, GraphQL, microservices, CQRS, security, and performance.
- `bem-styling` -> BEM naming, CSS architecture, and class refactors.
- `cicd-automation` -> CI/CD pipelines, workflow automation, deployments, and secrets handling.
- `cli-developer` -> CLI design, flags, prompts, shell UX, and command architecture.
- `developer-essentials` -> auth, debugging, git, code review, E2E, errors, monorepos, builds, and SQL optimization.
- `django-expert` -> Django, DRF, models, serializers, viewsets, auth, and ORM tuning.
- `documentation-generation` -> ADRs, changelogs, OpenAPI docs, tutorials, references, and Mermaid diagrams.
- `engineering` -> general engineering quality, architecture sanity, code review standards, and release readiness.
- `flutter-expert` -> Flutter, Dart, widgets, Riverpod or Bloc, GoRouter, and app structure.
- `fullstack-stacks` -> selecting pragmatic modern stacks across web and backend ecosystems.
- `git-repository-management` -> worktrees, branch hygiene, rebasing, recovery, release cleanup, and commit-process guidance across the full Git workflow.
- `golang-pro` -> idiomatic Go, concurrency, interfaces, testing, and production services.
- `javascript-typescript` -> modern JavaScript and TypeScript implementation and testing guidance.
- `kotlin-specialist` -> Kotlin, coroutines, Flow, Compose, Ktor, DSLs, and multiplatform architecture.
- `nextjs-developer` -> Next.js App Router, data fetching, metadata, server actions, and server-first patterns.
- `pandas-pro` -> pandas data cleaning, joins, aggregations, reshaping, and performance work.
- `playwright-expert` -> Playwright test design, selectors, page objects, mocks, and flaky-test debugging.
- `python-development` -> modern Python development, FastAPI, async patterns, testing, typing, packaging, and observability.
- `react-expert` -> React, hooks, component architecture, Next.js UI work, testing, and modern patterns.
- `react-native-expert` -> React Native, Expo, navigation, platform differences, list performance, and storage patterns.
- `rust-engineer` -> Rust ownership, traits, async Tokio code, error handling, and systems programming.
- `sql-pro` -> SQL query tuning, schema design, indexing, execution-plan analysis, and dialect migrations.
- `ui-design` -> UI and UX design, design systems, accessibility, responsive layout, and interaction review.
- `vue-expert-js` -> Vue 3 with Composition API in JavaScript, composables, state management, and testing.

## Common Combinations

- React UI implementation -> `react-expert` + `ui-design`
- Next.js product feature -> `nextjs-developer` + `react-expert`
- HTML or CSS cleanup with visual polish -> `html-css-refactor` + `ui-design`
- Release or PR cleanup with commit and history work -> `git-repository-management`
- Backend API with Python -> `python-development` + `backend-development`
- Django backend feature -> `django-expert` + `backend-development`
- Architecture review before release -> `engineering` + `developer-essentials`
- Docs for an implemented feature -> `app-docs` or `documentation-generation`, depending on whether the output is lightweight app docs or formal technical documentation

## Response Shape

When using this skill, answer with:

1. The recommended skill or skills.
2. A one-line reason for each.
3. Any close alternative when the match is ambiguous.

Keep recommendations concrete. Do not list the entire catalog unless the user explicitly asks for all available options.
