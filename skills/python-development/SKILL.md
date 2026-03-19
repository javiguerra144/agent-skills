---
name: "python-development"
description: "Use when building, refactoring, debugging, testing, or optimizing modern Python applications, including Django, FastAPI, asyncio, typing, packaging, observability, resilience, configuration, and project scaffolding."
---

# Python Development

Use this skill for modern Python engineering work derived from the `wshobson/agents` `plugins/python-development` plugin. It packages the upstream material as one installable skill with targeted references.

## Use This Skill When

- Building or refactoring Python applications or libraries
- Working on Django or FastAPI services
- Designing async flows, background jobs, or task processing
- Improving Python tests, type safety, or code quality tooling
- Setting up project structure, configuration, packaging, or scaffolding
- Debugging performance, observability, resilience, or resource-management issues

## Default Approach

1. Identify whether the task is general Python, Django, FastAPI, async, testing, typing, packaging, configuration, architecture, performance, or operational hardening.
2. Load only the matching reference files from `references/`.
3. Prefer modern Python project conventions such as `pyproject.toml`, type hints, automated linting, and practical test coverage when they fit the existing codebase.
4. Preserve the repository's current framework and tooling choices unless the user asks for migration or standardization.
5. When behavior changes, include validation, tests, and operational considerations proportional to the risk.

## Fast Rules

- Prefer readable modules, explicit interfaces, and focused responsibilities over clever abstractions.
- Use async patterns for I/O concurrency, not as a default for CPU-bound work.
- Keep configuration externalized and validated at startup.
- Add type annotations to public interfaces when the codebase supports them.
- Treat retries, timeouts, logging, and metrics as design concerns, not post-release cleanup.
- Profile before making performance-driven rewrites.

## Reference Map

Load only what you need:

- `references/python-pro.md` -> broad modern Python guidance, tooling, language features, and production practices.
- `references/django-pro.md` -> Django application architecture, ORM usage, async Django, DRF, Channels, Celery, and deployment guidance.
- `references/fastapi-pro.md` -> FastAPI architecture, async API design, SQLAlchemy, Pydantic, and production API patterns.
- `references/async-python-patterns.md` -> `asyncio`, concurrency decisions, async/await patterns, and non-blocking design.
- `references/python-testing-patterns.md` -> `pytest`, fixtures, mocking, async tests, and broader testing strategy.
- `references/python-type-safety.md` -> type annotations, generics, protocols, narrowing, and strict type-checking practices.
- `references/python-code-style.md` -> formatting, linting, naming, docstrings, and project style baselines.
- `references/python-project-structure.md` -> module layout, public API design, and project organization.
- `references/python-design-patterns.md` -> KISS, separation of concerns, composition, and architecture-level design choices.
- `references/python-anti-patterns.md` -> review checklist for common Python mistakes and maintainability risks.
- `references/python-configuration.md` -> environment variables, typed settings, secret handling, and startup validation.
- `references/python-error-handling.md` -> input validation, exception design, and graceful handling of partial failures.
- `references/python-resource-management.md` -> context managers, cleanup guarantees, streaming, and connection lifecycle patterns.
- `references/python-background-jobs.md` -> queues, workers, idempotency, and long-running task processing.
- `references/python-resilience.md` -> retries, backoff, timeouts, and fault-tolerant service interactions.
- `references/python-observability.md` -> structured logging, metrics, tracing, and production diagnostics.
- `references/python-performance-optimization.md` -> profiling, bottleneck analysis, memory usage, and performance tuning.
- `references/python-packaging.md` -> packaging libraries or CLIs, `pyproject.toml`, build backends, and publishing workflows.
- `references/uv-package-manager.md` -> `uv` workflows for environments, dependencies, lockfiles, and faster installs.
- `references/python-scaffold.md` -> new-project scaffolding for FastAPI, Django, libraries, CLIs, and generic Python apps.

## Suggested Routing

- If the task is broad Python work, load `references/python-pro.md` first, then the narrower reference that matches the framework or concern.
- If the task is framework-specific, load `references/django-pro.md` or `references/fastapi-pro.md`.
- If the task is architecture or maintainability focused, load `references/python-project-structure.md`, `references/python-design-patterns.md`, and optionally `references/python-anti-patterns.md`.
- If the task is reliability or production-hardening focused, load `references/python-error-handling.md`, `references/python-resilience.md`, `references/python-resource-management.md`, and `references/python-observability.md` as needed.
- If the task is tooling or project setup, load `references/python-code-style.md`, `references/python-configuration.md`, `references/uv-package-manager.md`, `references/python-packaging.md`, or `references/python-scaffold.md`.
- If the task is performance or concurrency related, load `references/async-python-patterns.md` and/or `references/python-performance-optimization.md`.

## Notes

- The bundled references are adapted from the upstream plugin source and kept separate for progressive disclosure.
- This skill overlaps with broader repo skills such as `backend-development` and narrower ones such as `cli-developer`; use the more focused skill when the task is narrow, and this bundle when Python-specific implementation detail matters most.
- Prefer the repository's existing runtime version, framework choices, and deployment model over generic examples when they conflict.
