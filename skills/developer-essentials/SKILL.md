---
name: "developer-essentials"
description: "Use when solving common engineering workflow problems such as authentication, debugging, code review, E2E testing, error handling, advanced git usage, monorepo management, build optimization, SQL performance, and developer tooling architecture."
---

# Developer Essentials

Use this skill for cross-cutting engineering workflow tasks derived from the `wshobson/agents` `plugins/developer-essentials` plugin. It packages the upstream material as one installable skill with targeted references.

## Use This Skill When

- Implementing or reviewing authentication patterns
- Debugging complex application or infrastructure issues
- Performing or improving code review quality
- Designing E2E testing strategies
- Improving application error handling
- Working on advanced git workflows
- Managing monorepos, Nx workspaces, or Turborepo caching
- Optimizing Bazel builds or SQL query performance

## Default Approach

1. Identify whether the task is auth, code review, debugging, testing, error handling, git workflow, monorepo tooling, build optimization, or SQL optimization.
2. Load only the matching reference files from `references/`.
3. Prefer reproducible workflows, explicit validation, and maintainable conventions.
4. Keep the solution proportional to the real operational or development pain point.
5. When changing shared developer workflows, optimize for clarity, adoption, and low surprise.

## Fast Rules

- Prefer stable workflows and explicit guardrails over clever shortcuts.
- Treat debugging as hypothesis-driven, evidence-based work.
- Keep review guidance actionable and specific to impact.
- Make authentication and error handling secure by default.
- Avoid monorepo or build-tool complexity unless it materially improves the developer experience.
- Optimize SQL and build performance from actual bottlenecks, not guesses.

## Reference Map

Load only what you need:

- `references/auth-implementation-patterns.md` -> authentication flows, implementation patterns, and auth-specific tradeoffs.
- `references/code-review-excellence.md` -> effective review strategy, issue identification, and review quality patterns.
- `references/debugging-strategies.md` -> debugging workflows, diagnosis patterns, and evidence-driven troubleshooting.
- `references/e2e-testing-patterns.md` -> end-to-end testing design, structure, reliability, and tooling patterns.
- `references/error-handling-patterns.md` -> error boundaries, classification, propagation, and recovery patterns.
- `references/git-advanced-workflows.md` -> advanced branching, history management, and collaborative git workflows.
- `references/monorepo-management.md` -> monorepo structure, coordination, dependency boundaries, and developer workflow management.
- `references/monorepo-architect.md` -> higher-level monorepo architecture guidance and tradeoff framing.
- `references/nx-workspace-patterns.md` -> Nx workspace organization and tooling patterns.
- `references/turborepo-caching.md` -> Turborepo caching strategy and performance guidance.
- `references/bazel-build-optimization.md` -> Bazel performance and build optimization patterns.
- `references/sql-optimization-patterns.md` -> SQL performance, query tuning, and database-side optimization patterns.

## Suggested Routing

- If the task is security- or identity-related, load `references/auth-implementation-patterns.md`.
- If the task is debugging, load `references/debugging-strategies.md`.
- If the task is about review quality, load `references/code-review-excellence.md`.
- If the task is about E2E reliability, load `references/e2e-testing-patterns.md`.
- If the task is about errors, retries, or user-facing failures, load `references/error-handling-patterns.md`.
- If the task is git process or history management, load `references/git-advanced-workflows.md`.
- If the task is monorepo-wide, load `references/monorepo-management.md` and `references/monorepo-architect.md`; add Nx or Turborepo references when relevant.
- If the task is Bazel-specific, load `references/bazel-build-optimization.md`.
- If the task is query or database performance, load `references/sql-optimization-patterns.md`.

## Notes

- The bundled references are adapted from the upstream plugin source and kept separate for progressive disclosure.
- This skill overlaps with narrower repo skills like `using-git-worktrees`, `engineering`, `cli-developer`, and `cicd-automation`; use the focused skill when the task is narrow, and this bundle when the workflow concern is broader.
- Prefer the repository's existing stack, tooling, and team conventions over generic examples when they conflict.
