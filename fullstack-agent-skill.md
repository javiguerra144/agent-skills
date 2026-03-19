# Full-Stack Agent Skill

Use this skill whenever building, reviewing, extending, or debugging full-stack web applications. It is optimized for modern TypeScript stacks wi([skills.sh](https://skills.sh/shubhamsaboo/awesome-llm-apps/fullstack-developer)), Node.js, PostgreSQL, Prisma, Redis, and production-grade deployment workflows.

This skill is based on the fullstack-developer skill from `shubhamsaboo/awesome-llm-apps`, expanded into a stricter agent-oriented version for end-to-end product delivery.

---

# 1. Mission

Build full-stack software that is:

* Correct
* Typed
* Secure by default
* Easy to maintain
* Easy to test
* Production-ready
* Clear to hand off

Prefer simple, conventional architecture over cleverness.

---

# 2. When to Apply

Use this skill when:

* Building complete web applications
* Developing REST or GraphQL APIs
* Creating React or Next.js frontends
* Designing backend services and data flows
* Setting up databases and data models
* Implementing authentication and authorization
* Integrating payments, email, storage, or third-party APIs
* Improving performance, reliability, or observability
* Preparing apps for deployment and scaling
* Reviewing full-stack pull requests or feature work

---

# 3. Default Stack

## Frontend

* React with TypeScript
* Next.js with App Router by default
* Tailwind CSS for styling
* React Hook Form for forms
* Zod for validation
* TanStack Query for server state
* Zustand only when shared client state is truly needed

## Backend

* Next.js route handlers or Node.js service layer
* TypeScript throughout
* Zod for request and config validation
* REST by default, GraphQL only when the domain clearly benefits
* Session or token auth depending on product needs

## Database and Infra

* PostgreSQL as the default primary database
* Prisma as the default ORM
* Redis for caching, sessions, queues, rate limiting, or background coordination
* Object storage for file uploads
* Vercel for Next.js deployment by default
* Docker when parity, portability, workers, or custom runtime control is needed
* GitHub Actions for CI/CD

## Use Alternatives Only When Justified

Choose MongoDB, GraphQL, custom state libraries, or microservices only when there is a clear technical reason.

---

# 4. Decision Defaults

Unless the project already defines another pattern, default to:

* Monorepo only if there are multiple deployable apps or shared packages
* Next.js full-stack app for small to medium products
* REST APIs with typed request and response shapes
* Server components where possible, client components where necessary
* Server-side data fetching for SEO and initial load performance
* TanStack Query for client-side async state
* Prisma schema as the source of truth for relational data
* Feature folders for product domains, shared folders for reusable primitives
* Utility extraction when logic is duplicated or independently testable

---

# 5. Architecture Rules

## Frontend Structure

Prefer a structure like:

```text
src/
  app/
  components/
    ui/
    features/
  hooks/
  lib/
  services/
  types/
  styles/
```

Guidelines:

* `app/` for routes, layouts, pages, server actions, and route handlers
* `components/ui/` for reusable presentational primitives
* `components/features/` for domain-specific UI
* `hooks/` for custom React hooks
* `lib/` for shared utilities, config, and helpers
* `services/` for API clients and external integrations
* `types/` for stable cross-layer types when needed

## Backend Structure

Prefer a structure like:

```text
src/
  routes/
  controllers/
  services/
  repositories/
  middleware/
  lib/
  utils/
  config/
```

Guidelines:

* Routes should stay thin
* Controllers coordinate request/response flow
* Services hold business logic
* Repositories isolate data access when complexity warrants it
* Middleware handles cross-cutting concerns
* Utils hold pure reusable helpers

## Layering Rules

* UI must not directly contain business rules that belong in services or domain helpers
* Route handlers must not become giant orchestration blocks
* Database access should be centralized, typed, and consistent
* Validation should happen at boundaries
* Side effects should be isolated from pure logic where practical

---

# 6. Coding Rules

## Complexity and Reuse

* Keep function cyclomatic complexity below 10
* Prefer functions under 30 lines when practical
* Split validation, transformation, persistence, and formatting into separate units
* Extract reusable logic to `lib/`, `utils/`, or shared domain modules
* Avoid duplicate mapping, formatting, validation, and normalization logic

## Naming

* Use names that reflect business intent
* Avoid vague names like `handleData`, `processThing`, or `doStuff`
* Boolean names should read like facts: `isEligible`, `hasPermission`, `canPublish`

## Purity and Side Effects

* Prefer pure functions for transformations and calculations
* Keep network calls, writes, logging, and framework coupling isolated
* Do not mutate inputs unless clearly intended and documented

## Error Handling

* Return or throw actionable errors
* Use consistent error shapes for APIs
* Do not swallow exceptions silently
* Avoid leaking internal stack traces or secrets to clients

---

# 7. Frontend Rules

## Component Design

* Keep components focused and composable
* Prefer composition over prop drilling
* Use server components by default in Next.js
* Use client components only for interactivity, browser APIs, or local stateful behavior
* Handle loading, empty, success, and error states explicitly

## State Management

* Server state belongs in TanStack Query or server fetching flows
* Form state belongs in React Hook Form
* Local UI state stays local unless truly shared
* Introduce Zustand only for shared client state that does not fit context cleanly
* Avoid global state for transient or feature-local concerns

## Forms

* Use schema-backed validation
* Keep field defaults explicit
* Show useful validation messages
* Prevent duplicate submissions
* Handle optimistic UI carefully

## Performance

* Use dynamic imports for heavy components
* Lazy load non-critical UI where useful
* Optimize images and large assets
* Minimize unnecessary re-renders
* Memoize only when there is a real rendering benefit

## Accessibility

* Use semantic HTML first
* Ensure keyboard access for interactive elements
* Provide labels, alt text, and sensible focus states
* Never rely on color alone to convey meaning

---

# 8. Backend Rules

## API Design

* Prefer REST unless GraphQL clearly improves the product
* Use resource-oriented naming
* Use proper HTTP methods and status codes
* Version APIs when compatibility matters
* Return consistent success and error shapes

## Validation

* Validate all external inputs at the boundary
* Parse request bodies, params, headers, env vars, and webhooks explicitly
* Fail fast on malformed input
* Never trust client input

## Auth and Authorization

* Separate authentication from authorization
* Check permissions at the correct boundary
* Never expose data based only on client-provided identifiers
* Default deny when authorization context is unclear

## Security

* Use parameterized queries or ORM protections correctly
* Sanitize user-controlled rich text where needed
* Protect secrets and tokens
* Add rate limiting for sensitive or abusable endpoints
* Enforce HTTPS in production
* Verify webhook signatures
* Protect against CSRF where cookie-based auth is used

## Service Design

* Keep business rules in service functions, not route handlers
* Make side effects explicit
* Use idempotency where retries are possible
* Use queues or background jobs for slow or retry-prone workflows

---

# 9. Database Rules

## Schema Design

* Model relational data clearly
* Use explicit constraints and indexes
* Add unique constraints where business rules require uniqueness
* Prefer normalized schema until denormalization is justified

## Query Design

* Avoid N+1 queries
* Select only needed fields
* Use pagination for list endpoints
* Use transactions for related writes
* Keep query intent readable

## Migrations

* Make migrations reversible when practical
* Avoid risky destructive changes without a rollout plan
* Backfill data in safe steps for large datasets
* Coordinate schema and app deployments when compatibility matters

## Caching

* Cache only when it solves a real latency or load issue
* Define cache keys clearly
* Set explicit invalidation or TTL behavior
* Never let stale cache create correctness problems for sensitive workflows

---

# 10. Integration Rules

When integrating third-party services:

* Isolate provider logic behind service modules
* Validate provider responses before trusting them
* Handle retries, timeouts, and partial failures explicitly
* Log provider failures with enough detail for debugging
* Never spread provider-specific code throughout the app

Examples:

* Payments
* Email providers
* File storage
* Search providers
* Analytics
* Feature flags
* OAuth providers

---

# 11. Testing Rules

## Minimum Expectations

* Unit tests for pure business logic and utilities
* Integration tests for important API, DB, or service boundaries
* Regression tests for bug fixes
* Smoke coverage for critical user journeys when relevant

## What to Test

* Happy paths
* Validation failures
* Authorization failures
* Empty states
* Error states
* Edge cases around null, missing, and malformed input
* Retry and idempotency behavior for external operations

## Test Design

* Keep tests behavior-focused
* Avoid overly brittle snapshot-heavy tests
* Mock external services at stable boundaries
* Prefer realistic integration tests for critical flows

---

# 12. Quality Gates

A change fails this skill if any of the following are true:

* The build does not pass
* Lint or formatting is broken
* Type checks fail
* New meaningful logic lacks tests appropriate to risk
* Function complexity exceeds acceptable limits
* Shared logic is duplicated instead of extracted
* Input validation is missing at boundaries
* Security or auth concerns remain unresolved
* Performance regressions are introduced in obvious hot paths
* Operational visibility is missing for critical workflows
* Deployment or rollback risk is ignored for high-impact changes

---

# 13. Output Requirements

When implementing a feature, provide:

1. File structure
2. Complete code
3. Dependencies
4. Environment variables
5. Migration or schema updates if needed
6. Setup instructions
7. Run commands
8. Test notes
9. Deployment notes when relevant

When reviewing code, provide:

1. Verdict
2. Failed gates
3. Required fixes
4. Suggested improvements
5. Residual risk

---

# 14. Delivery Style

When generating code:

* Prefer complete, working, typed examples
* Keep files small and purpose-driven
* Explain placement of each file
* Show only necessary abstractions
* Match the existing stack and conventions where known

When reviewing code:

* Be strict on correctness, auth, validation, and data integrity
* Distinguish must-fix issues from optional improvements
* Suggest the smallest safe refactor that resolves the problem

---

# 15. Default Response Patterns

## For feature requests

Respond with:

* brief approach
* file tree
* implementation
* required packages
* env vars
* how to run
* how to test

## For debugging requests

Respond with:

* likely root cause
* exact failing layer
* minimal fix
* prevention steps
* tests to add

## For code reviews

Respond with:

* verdict
* blocking issues by gate name
* concise rationale
* suggested patch direction

---

# 16. Anti-Patterns to Avoid

* Giant route handlers
* Business logic inside React components
* Unvalidated request bodies
* Client-trusting authorization checks
* Generic helper names
* Copy-pasted normalization or formatting logic
* Hidden side effects
* Overuse of global state
* Premature microservices
* Missing loading and error states
* ORM misuse that causes N+1 queries
* Unsafe migrations without rollout planning

---

# 17. Default Standard

If no project-specific convention overrides this skill, default to:

* Next.js + TypeScript + Tailwind
* Prisma + PostgreSQL
* Zod validation at boundaries
* TanStack Query for server state
* React Hook Form for forms
* REST APIs
* Utility extraction for reusable logic
* Function complexity below 10
* Tests for business logic and critical paths
* Security and auth treated as blocking quality gates
