# Engineering Agent Skill

Use this skill pack whenever writing, reviewing, refactoring, or approving code. It combines baseline programming rules with quality gates so the agent can enforce both code quality and release readiness.

---

# Part 1: Base Programming Rules

## Objective

Produce code that is:

* Easy to read
* Easy to test
* Easy to reuse
* Safe to change
* Small in scope

Prefer boring, predictable solutions over clever ones.

## Core Rules

### 1. Keep complexity low

* Keep each function focused on one job.
* Target cyclomatic complexity below **10** per function.
* Prefer complexity below **5** when practical.
* Split large condition trees into helper functions.
* Replace nested conditionals with guard clauses when it improves clarity.
* Do not combine parsing, validation, business logic, and formatting in one function.

### 2. Prefer reusable utilities

* If logic is useful in more than one place, extract it.
* Put reusable pure logic into a `utils`, `helpers`, or shared domain module.
* Export utility functions with stable, descriptive names.
* Do not duplicate string formatting, validation, mapping, date handling, or transformation logic across files.
* Before adding a new helper, check whether an equivalent utility already exists.

### 3. Write small functions

* Prefer functions under **30 lines**.
* Reconsider any function above **50 lines**.
* Pass explicit inputs instead of depending on hidden globals.
* Return explicit outputs.

### 4. Use clear names

* Use names that describe intent, not implementation details.
* Prefer `calculateInvoiceTotal` over `handleData`.
* Avoid abbreviations unless they are standard in the codebase.
* Boolean names should read like facts, such as `isReady`, `hasAccess`, `canRetry`.

### 5. Separate responsibilities

* Keep business logic separate from I/O.
* Keep UI rendering separate from data transformation.
* Keep database access separate from decision logic.
* Keep framework glue thin.

### 6. Prefer pure functions

* Prefer functions that do not mutate inputs.
* Prefer deterministic behavior for the same inputs.
* Isolate side effects like network calls, file writes, and database access.

### 7. Avoid duplication

* Follow DRY, but do not over-abstract too early.
* Extract duplication when:

  * the same logic appears more than once,
  * the behavior must stay consistent everywhere,
  * a bug fix would otherwise require multiple edits.
* Do not create abstractions that hide simple code without a clear benefit.

### 8. Validate at boundaries

* Validate external input at the edges of the system.
* Fail fast with clear errors.
* Do not let malformed input flow deep into the code.

### 9. Make errors useful

* Raise or return errors with actionable context.
* Do not swallow exceptions silently.
* Log enough detail for debugging without leaking secrets.

### 10. Keep interfaces simple

* Prefer fewer parameters.
* Group related parameters into a typed object when it improves readability.
* Avoid long positional argument lists.

## Code Organization Rules

### File structure

* One file should have one clear responsibility.
* Avoid mixing unrelated utilities, domain logic, and UI concerns in the same file.
* Keep shared helpers in a dedicated reusable location.

### Utility extraction guidance

Extract code to a utility module when it is:

* Pure or mostly pure
* Reused or likely to be reused
* Easy to test independently
* Not tightly coupled to a single component or endpoint

Do **not** extract to a utility if the logic is:

* Hyper-local and only used once
* More readable inline
* Dependent on too much local context

### Import rules

* Prefer importing from stable public modules instead of deep internal paths.
* Avoid circular dependencies.
* Keep dependency direction clean: app layers may depend downward, not upward.

## Review Gates for Code Quality

Before finalizing code, check these questions:

1. Is every function doing one thing?
2. Is any function likely above complexity 10?
3. Can repeated logic be moved to a reusable utility?
4. Are names obvious to a new engineer?
5. Are side effects isolated?
6. Is input validated at the boundary?
7. Is the code easy to test?
8. Is there duplication that will create future drift?
9. Are errors clear and actionable?
10. Is this the simplest solution that works?

## Preferred Refactoring Patterns

### Reduce branching

* Use guard clauses
* Extract predicate helpers
* Replace repeated switch or if chains with maps where appropriate
* Split workflows into named steps

### Improve reuse

* Extract formatting logic
* Extract validation logic
* Extract transformation and mapping logic
* Extract shared constants and enums
* Extract repeated API response normalization

### Improve readability

* Replace magic values with named constants
* Inline overly trivial wrappers
* Break complex expressions into named intermediate variables
* Remove dead code and commented-out code

## Testing Rules

* Add tests for business logic and extracted utilities.
* Prefer unit tests for pure helpers.
* Test edge cases, invalid input, and failure paths.
* When fixing a bug, add or update a test that would have caught it.

## Performance Rules

* Do not optimize prematurely.
* First prefer readable code.
* Optimize only when there is a known bottleneck, measurable cost, or clear scale concern.
* When optimizing, preserve readability and add comments only where needed.

## Documentation Rules

* Add comments only when the code itself cannot make the intent obvious.
* Document why, not what.
* For shared utilities, include a short docstring when behavior or constraints are not obvious.

## Anti-Patterns to Avoid

* God functions
* Deeply nested conditionals
* Hidden side effects
* Copy-paste reuse
* Generic helper names like `process`, `handleThing`, `doStuff`
* Premature abstraction
* Mixed business logic and framework code
* Silent catch blocks
* Mutating input objects unless clearly intended

---

# Part 2: Quality Gates

## Objective

Only allow changes to pass when they meet a minimum bar for:

* Correctness
* Readability
* Test coverage
* Reliability
* Security
* Performance
* Operability
* Maintainability

Do not approve code just because it works locally.

## Core Principle

A change passes only when it is:

1. Correct
2. Verified
3. Safe to operate
4. Easy to understand
5. Low enough risk for the scope

If a gate fails, stop and report the failure clearly.

## Required Quality Gates

### 1. Build gate

The change must:

* Compile or build successfully
* Not introduce broken imports or unresolved references
* Not leave dead code paths caused by partial refactors

Fail if:

* The project does not build
* Any required generated artifacts are missing
* The change depends on manual hidden steps not documented in the workflow

### 2. Lint and formatting gate

The change must:

* Pass project lint rules
* Pass formatting checks
* Follow existing style conventions

Fail if:

* New warnings are introduced in enforced lint paths
* Formatting is inconsistent with the codebase standard
* The change adds suppressions without justification

### 3. Type and schema gate

The change must:

* Pass type checks where applicable
* Keep public types accurate
* Keep schemas, contracts, and interfaces aligned

Fail if:

* Type errors exist
* Runtime shape and declared type diverge
* API contracts changed without corresponding updates

### 4. Correctness gate

The change must:

* Solve the stated problem
* Handle expected edge cases
* Preserve existing required behavior

Fail if:

* The implementation only covers the happy path
* Existing flows regress
* Input validation is missing at boundaries
* Error handling is incomplete or misleading

### 5. Test gate

The change must:

* Include tests for new business logic
* Update tests for changed behavior
* Add regression tests for bug fixes
* Keep existing tests passing

Minimum expectations:

* Unit tests for pure logic
* Integration tests for changed boundaries where relevant
* Regression coverage for known failures

Fail if:

* New logic has no meaningful test coverage
* A bug fix ships without a regression test
* Tests are brittle, misleading, or do not assert behavior clearly

### 6. Complexity gate

The change must:

* Keep function cyclomatic complexity below **10**
* Avoid deeply nested control flow
* Keep modules focused and understandable

Fail if:

* A function becomes too large or too branch-heavy
* One unit mixes validation, orchestration, business logic, and I/O unnecessarily
* Duplication increases future maintenance risk

### 7. Reuse and duplication gate

The change must:

* Reuse existing shared helpers when appropriate
* Extract repeated logic when it appears in more than one place
* Keep shared behavior consistent through utility modules

Fail if:

* Similar logic is copied across files
* New helper logic duplicates an existing utility
* Shared business rules are implemented differently in different paths

### 8. Security gate

The change must:

* Validate and sanitize untrusted input where needed
* Avoid leaking secrets, tokens, or sensitive data
* Respect authorization and access control boundaries
* Use safe defaults

Fail if:

* Sensitive data is logged
* Auth checks are missing or bypassable
* User input reaches risky sinks without validation
* Dependencies or patterns introduce obvious security issues

### 9. Performance gate

The change must:

* Avoid unnecessary repeated work
* Avoid clearly inefficient queries, loops, or rendering patterns
* Consider scale when touching hot paths

Fail if:

* The change adds avoidable N+1 queries, repeated scans, or wasteful recomputation
* It increases latency or memory cost in a known critical path without reason
* It adds caching, batching, or concurrency in a way that harms correctness

### 10. Observability and operability gate

The change must:

* Produce useful logs, metrics, or traces where operationally relevant
* Fail with actionable errors
* Support debugging of likely failure modes

Fail if:

* Failures become harder to diagnose
* Critical background or async workflows have no visibility
* Operational impact cannot be detected or investigated

### 11. Documentation gate

The change must:

* Update docs when behavior, configuration, or workflows change
* Keep README, runbooks, or API docs aligned when relevant
* Explain non-obvious decisions briefly in code or docs

Fail if:

* Setup or usage changed but docs did not
* New env vars, feature flags, or migrations are undocumented
* Important constraints exist only in someone’s head

### 12. Deployment and rollback gate

The change must:

* Be safe to deploy for its risk level
* Avoid breaking migrations or irreversible steps without a plan
* Support rollback or safe mitigation where practical

Fail if:

* The rollout depends on fragile sequencing without documentation
* The change introduces irreversible behavior with no mitigation
* Backward compatibility is broken without explicit coordination

## Risk-Based Expectations

### Low-risk changes

Examples:

* Copy updates
* Styling-only changes
* Small refactors with no behavior change

Expected gates:

* Build
* Lint/format
* Correctness review
* Existing tests pass

### Medium-risk changes

Examples:

* Business logic updates
* New endpoint behavior
* Validation changes
* Shared utility refactors

Expected gates:

* All low-risk gates
* New or updated tests
* Type checks
* Complexity and reuse review
* Basic operational review

### High-risk changes

Examples:

* Auth changes
* Billing logic
* Data migrations
* Concurrency changes
* Infrastructure or deployment changes
* Performance-critical path updates

Expected gates:

* All medium-risk gates
* Security review
* Rollout plan
* Rollback or mitigation plan
* Strong observability review
* Explicit edge-case review

## Review Questions

Before approving, answer:

1. Does this change clearly solve the intended problem?
2. What could break because of this change?
3. Are new behaviors covered by tests?
4. Is the code understandable to someone new to the area?
5. Are shared rules implemented in one reusable place?
6. Are edge cases and failure paths handled?
7. Could this expose data, bypass auth, or weaken validation?
8. Could this cause avoidable performance regressions?
9. Can we detect and debug failures in production?
10. Can we roll this back or mitigate quickly if needed?

---

# Part 3: Agent Behavior

When writing, reviewing, or refactoring code, the agent should:

1. Prefer the simplest correct implementation.
2. Flag functions that appear too large or too complex.
3. Suggest extraction when logic is duplicated or reusable.
4. Recommend moving shared logic into a utility folder or shared module.
5. Preserve existing architecture unless there is a clear improvement.
6. Avoid unnecessary rewrites.
7. Explain refactors in terms of readability, reuse, testing, and maintenance.
8. Treat quality gates as blocking checks, not optional advice.
9. Call out failures explicitly by gate name.
10. Distinguish between must-fix issues and nice-to-have improvements.
11. Suggest the smallest change that would make the gate pass.
12. Escalate scrutiny when the change touches security, data integrity, billing, auth, or production operations.
13. Refuse to mark a change production-ready if required gates fail.

---

# Part 4: Review Output Format

Use this structure when reviewing code:

## Verdict

* Pass
* Pass with minor follow-ups
* Fails skill pack checks

## Failed gates

* List each failed gate by name
* Explain why it failed
* State impact and risk briefly

## Required fixes

* List blocking changes needed to pass

## Suggested improvements

* List non-blocking improvements separately

## Residual risk

* State any remaining risk even if the change passes

---

# Part 5: Example Enforcement Notes

* "This function should be split because it mixes validation, transformation, and persistence."
* "The date formatting logic appears in multiple files and should be exported to a shared utility."
* "This branch structure is too nested; use guard clauses or extract decision helpers."
* "This helper is generic and should be renamed to reflect business intent."
* "Fails Test Gate: new business logic was added without unit coverage."
* "Fails Security Gate: user-controlled input reaches a query builder without validation."
* "Fails Deployment Gate: this migration is not clearly backward compatible and has no rollback plan."

---

# Default Standard

If no project-specific convention overrides this skill pack, default to:

* Functions with complexity < 10
* Small focused modules
* Reusable utility extraction for shared logic
* Clear names
* Pure functions where possible
* Boundary validation
* Testable design
* Minimal but sufficient documentation
* Block on broken build, lint, types, or tests
* Block on missing tests for meaningful business logic changes
* Block on security, auth, and data integrity concerns
* Block on undocumented rollout risk for high-impact changes
* Separate must-fix items from non-blocking improvements
