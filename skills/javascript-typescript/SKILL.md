---
name: "javascript-typescript"
description: "Use when building, refactoring, debugging, scaffolding, or testing modern JavaScript or TypeScript projects, including async patterns, advanced typing, Node.js backend architecture, and JS or TS testing practices."
---

# JavaScript TypeScript

Use this skill for modern JavaScript and TypeScript work derived from the `wshobson/agents` `plugins/javascript-typescript` plugin. It packages the upstream material as one installable skill with targeted reference files.

## Use This Skill When

- Writing or refactoring modern JavaScript
- Designing advanced TypeScript types or utility types
- Building Node.js backends in JavaScript or TypeScript
- Setting up or improving Jest or Vitest test suites
- Scaffolding a new TypeScript project
- Debugging async behavior, promise handling, or event loop issues

## Default Approach

1. Decide whether the task is primarily JavaScript, TypeScript, backend, testing, or scaffolding.
2. Read only the matching reference file from `references/`.
3. Prefer modern syntax and strict typing where the codebase supports it.
4. Preserve existing framework and tooling choices unless the user asks for a migration.
5. Keep implementations practical: clear modules, explicit error handling, and tests when behavior changes.

## Fast Rules

- Prefer `async` and `await` over promise chains unless stream-style composition is clearer.
- Favor `const`, pure helpers, and immutable updates by default.
- In TypeScript, prefer inference when readable and explicit types when contracts matter.
- Use `unknown` instead of `any` when input must be narrowed.
- Model backend code with thin handlers, explicit validation, and isolated business logic.
- Add or update tests when changing behavior, especially around async flows and type-sensitive utilities.

## Reference Map

Load only what you need:

- `references/javascript-pro.md` -> high-level JavaScript expert guidance, async patterns, browser and Node.js compatibility.
- `references/typescript-pro.md` -> high-level TypeScript expert guidance, strict typing, compiler strategy, and enterprise-grade patterns.
- `references/modern-javascript-patterns.md` -> ES6+, async and await, modules, iterators, generators, modern operators, and performance patterns.
- `references/typescript-advanced-types.md` -> generics, conditional types, mapped types, template literal types, inference, type guards, and type testing.
- `references/javascript-testing-patterns.md` -> Jest, Vitest, Testing Library, unit tests, integration tests, E2E patterns, mocking, and TDD workflows.
- `references/nodejs-backend-patterns.md` -> Express, Fastify, middleware, architecture, auth, database integration, and production backend patterns.
- `references/typescript-scaffold.md` -> TypeScript project scaffolding guidance for Next.js, Vite, Node.js APIs, libraries, and CLIs.

## Suggested Routing

- If the user asks for async JavaScript cleanup, load `references/javascript-pro.md` and `references/modern-javascript-patterns.md`.
- If the task is advanced typing, load `references/typescript-pro.md` and `references/typescript-advanced-types.md`.
- If the task is backend API architecture, load `references/nodejs-backend-patterns.md`.
- If the task is testing or test setup, load `references/javascript-testing-patterns.md`.
- If the user wants a new project scaffold, load `references/typescript-scaffold.md` and whichever runtime-specific reference also matches.

## Notes

- The bundled references are adapted from the upstream plugin source and kept as separate files for progressive disclosure.
- Prefer the existing repository conventions over the reference defaults when they conflict.
