---
name: "backend-development"
description: "Use when designing, building, reviewing, or debugging backend systems, including API design, architecture patterns, microservices, CQRS and event sourcing, GraphQL, performance, security, testing, and workflow orchestration."
---

# Backend Development

Use this skill for backend engineering work derived from the `wshobson/agents` `plugins/backend-development` plugin. It packages the upstream material as one installable skill with targeted references.

## Use This Skill When

- Designing or reviewing backend system architecture
- Building or refactoring APIs, service boundaries, or domain logic
- Working on GraphQL backends or contract design
- Implementing microservices, CQRS, event sourcing, or sagas
- Improving backend performance, reliability, or security
- Adding backend tests or driving development with tests
- Building workflow orchestration or Temporal-based systems

## Default Approach

1. Identify whether the task is general backend architecture, API design, GraphQL, microservices, CQRS, event sourcing, performance, security, testing, or workflow orchestration.
2. Load only the matching reference files from `references/`.
3. Prefer explicit contracts, isolated business logic, and observable failure modes.
4. Keep architecture choices proportional to the actual problem size.
5. When behavior changes, include validation, tests, and operational considerations.

## Fast Rules

- Keep APIs and service boundaries consistent and predictable.
- Separate transport, orchestration, domain logic, and persistence concerns.
- Treat performance and security as design concerns, not afterthoughts.
- Avoid distributed complexity unless the domain justifies it.
- Prefer testable components and explicit failure handling.
- Use workflows, sagas, CQRS, and event sourcing only where they improve correctness or operability enough to justify the added complexity.

## Reference Map

Load only what you need:

- `references/backend-architect.md` -> broad backend architecture guidance, service design, reliability, and system evolution.
- `references/api-design-principles.md` -> REST or HTTP API consistency, contracts, and client-facing design rules.
- `references/graphql-architect.md` -> GraphQL schema design, resolver patterns, performance, and API boundaries.
- `references/architecture-patterns.md` -> layered architecture, hexagonal patterns, service decomposition, and backend structuring approaches.
- `references/microservices-patterns.md` -> service boundaries, communication patterns, resilience, and operational microservice tradeoffs.
- `references/performance-engineer.md` -> backend profiling, bottleneck analysis, scaling, and performance tuning.
- `references/security-auditor.md` -> backend security review, attack surface reduction, and secure implementation guidance.
- `references/tdd-orchestrator.md` -> test-driven backend delivery and sequencing.
- `references/test-automator.md` -> automated test generation and backend test coverage support.
- `references/cqrs-implementation.md` -> CQRS command and query separation patterns.
- `references/event-sourcing-architect.md` -> event-sourced domain design and aggregate modeling.
- `references/event-store-design.md` -> event store structure, append patterns, consistency, and retention concerns.
- `references/projection-patterns.md` -> read models, projections, denormalization, and update flow.
- `references/saga-orchestration.md` -> distributed transaction coordination and long-running workflows.
- `references/workflow-orchestration-patterns.md` -> durable workflow patterns and orchestration design.
- `references/temporal-python-pro.md` -> Temporal Python implementation guidance.
- `references/temporal-python-testing.md` -> testing Temporal Python workflows and activities.
- `references/feature-development.md` -> large backend feature workflow from planning through implementation.

## Suggested Routing

- If the task is general backend design, load `references/backend-architect.md` and `references/architecture-patterns.md`.
- If the task is API-first, load `references/api-design-principles.md`; for GraphQL specifically also load `references/graphql-architect.md`.
- If the task is distributed systems or service decomposition, load `references/microservices-patterns.md`.
- If the task is CQRS, event sourcing, projections, or sagas, load the matching event-driven references together.
- If the task is performance- or security-focused, load `references/performance-engineer.md` or `references/security-auditor.md`.
- If the task is Temporal-based, load `references/temporal-python-pro.md` and `references/temporal-python-testing.md`.
- If the user wants an end-to-end backend delivery workflow, load `references/feature-development.md`.

## Notes

- The bundled references are adapted from the upstream plugin source and kept separate for progressive disclosure.
- Some topics overlap with narrower skills already present in this repo, such as `api-design`; use the more focused skill when the task is narrow and the backend bundle when broader backend context matters.
- Prefer the repository's existing stack, deployment model, and architecture conventions over generic examples when they conflict.
