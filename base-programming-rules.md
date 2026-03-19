# Base Programming Rules Skill

Use this skill whenever writing, reviewing, or refactoring code. The goal is to keep code simple, reusable, testable, and easy to maintain.

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

## Review Gates

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

## Agent Behavior

When generating or reviewing code, the agent should:

1. Prefer the simplest correct implementation.
2. Flag functions that appear too large or too complex.
3. Suggest extraction when logic is duplicated or reusable.
4. Recommend moving shared logic into a utility folder or shared module.
5. Preserve existing architecture unless there is a clear improvement.
6. Avoid unnecessary rewrites.
7. Explain refactors in terms of readability, reuse, testing, and maintenance.

## Example Enforcement Notes

* "This function should be split because it mixes validation, transformation, and persistence."
* "The date formatting logic appears in multiple files and should be exported to a shared utility."
* "This branch structure is too nested; use guard clauses or extract decision helpers."
* "This helper is generic and should be renamed to reflect business intent."
* "This function likely exceeds the complexity target and should be broken into smaller steps."

## Output Style for Reviews

When reviewing code, use this structure:

### Summary

* State whether the code meets the baseline rules.

### Issues

* List concrete violations.
* Mention complexity, duplication, naming, coupling, or testing gaps.

### Suggested changes

* Give targeted refactors.
* Prefer small, incremental improvements.

### Example rewrite

* Include a minimal example only when it helps clarify the suggestion.

## Default Standard

If no project-specific convention overrides these rules, default to:

* Functions with complexity < 10
* Small focused modules
* Reusable utility extraction for shared logic
* Clear names
* Pure functions where possible
* Boundary validation
* Testable design
* Minimal but sufficient documentation
