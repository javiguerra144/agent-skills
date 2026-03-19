---
name: "conventional-commits"
description: "Use when writing or reviewing commit messages that should follow Conventional Commits with clear type, scope, subject, optional body, breaking-change notes, and release-friendly history."
---

# Conventional Commits Skill

Use this skill whenever writing commit messages. The goal is to produce clear, consistent, searchable commit history that works well for changelogs, release automation, and code review.

## Objective

Write commit messages that are:

* Conventional Commits compliant
* Specific and easy to scan
* Accurate to the actual change
* Small in scope
* Useful for future maintainers

Do not write vague commit messages.

## Core Format

Use this format:

```text
<type>(<scope>): <subject>

<body>

<footer>
```

Parts:

* `type` is required
* `scope` is recommended when it adds clarity
* `subject` is required
* `body` is optional but should be added for non-trivial changes
* `footer` is optional and used for breaking changes, issue references, or metadata

## Allowed Types

Use these default types unless the project defines others:

* `feat`: a new feature
* `fix`: a bug fix
* `refactor`: code change that neither fixes a bug nor adds a feature
* `perf`: performance improvement
* `test`: adding or updating tests
* `docs`: documentation only changes
* `style`: formatting or non-functional style-only changes
* `build`: build system or dependency/build tooling changes
* `ci`: CI/CD pipeline or automation changes
* `chore`: maintenance work that does not affect product behavior
* `revert`: reverts a previous commit

Do not misuse `chore` for meaningful product changes.

## Scope Rules

Use a scope when it helps identify the affected area.

Good scopes:

* `auth`
* `api`
* `checkout`
* `ui`
* `db`
* `payments`
* `search`
* `config`
* `deps`

Rules:

* Keep scope short
* Use lowercase
* Prefer one scope
* Match project naming if conventions already exist
* Omit scope if it does not add value

Examples:

* `feat(auth): add email magic link login`
* `fix(api): handle empty filter params`
* `refactor(db): extract order repository`
* `docs: update local setup instructions`

## Subject Rules

The subject line must:

* Be concise
* Describe what changed
* Use imperative mood
* Start with a lowercase word after the colon
* Avoid ending punctuation
* Prefer under 72 characters

Write subjects like:

* `add invoice status filter`
* `prevent duplicate webhook processing`
* `extract shared date formatter`

Do not write subjects like:

* `fixed stuff`
* `changes`
* `WIP`
* `misc updates`
* `final commit`

## Body Rules

Add a body when the change is not obvious from the subject alone.

The body should explain:

* Why the change was needed
* What approach was taken
* Any important tradeoffs or behavior changes

Rules:

* Wrap lines around 72 characters when practical
* Keep it factual and concise
* Focus on intent and impact, not low-level diff narration
* Use bullet points only when they improve clarity

Example:

```text
fix(webhooks): prevent duplicate order processing

Add idempotency checks before creating fulfillment records.
This avoids duplicate processing when the provider retries the
same webhook event after a timeout.
```

## Footer Rules

Use footers for:

* Breaking changes
* Issue references
* Ticket references
* Co-authors if required by workflow

Examples:

```text
BREAKING CHANGE: rename /v1/orders endpoint to /v2/orders
Refs: PROJ-142
Closes: #58
```

## Breaking Changes

Mark breaking changes in one of these ways:

### Option 1: `!` in the header

```text
feat(api)!: rename order status enum values
```

### Option 2: `BREAKING CHANGE:` footer

```text
refactor(auth): replace session payload structure

BREAKING CHANGE: session.user.id is now session.user.userId
```

Use both header and footer when the migration impact needs explanation.

## Commit Selection Rules

Before writing the commit message:

* Identify the primary purpose of the change
* Choose the most accurate type
* Avoid combining unrelated changes in one commit message
* Prefer one logical change per commit
* If the diff mixes concerns, describe the dominant one or split the commit

Priority guidance:

* If it adds user-visible behavior, prefer `feat`
* If it fixes incorrect behavior, prefer `fix`
* If it restructures code without behavior change, prefer `refactor`
* If it only updates docs, prefer `docs`
* If it only updates tests, prefer `test`

## Agent Behavior

When asked to write a commit, the agent should:

1. Infer the dominant change from the diff or description.
2. Choose the narrowest accurate commit type.
3. Add scope when it improves clarity.
4. Keep the subject concise and action-oriented.
5. Add a body for non-trivial changes.
6. Mark breaking changes explicitly.
7. Avoid vague, inflated, or misleading wording.
8. Avoid mentioning unrelated files or side effects not central to the commit.
9. Prefer one strong commit message over multiple weak variants unless alternatives are requested.

## Review Checklist

Before finalizing the commit message, check:

1. Is the type correct?
2. Is the scope useful and concise?
3. Does the subject describe the actual change?
4. Is the subject imperative and specific?
5. Is the commit free of vague words like `stuff`, `misc`, or `updates`?
6. Does the body explain why for non-trivial changes?
7. Is any breaking change clearly marked?
8. Would this message still make sense six months from now?

## Examples

### Feature

```text
feat(checkout): add saved card selection
```

### Bug fix

```text
fix(search): handle empty query without 500 response
```

### Refactor

```text
refactor(ui): extract reusable modal footer actions
```

### Performance

```text
perf(api): cache product detail responses for 60 seconds
```

### Tests

```text
test(auth): add regression coverage for expired reset tokens
```

### Docs

```text
docs: add environment setup steps for local postgres
```

### Build

```text
build(deps): upgrade prisma to 6.2.0
```

### CI

```text
ci: run typecheck before docker build
```

### Breaking change

```text
feat(api)!: replace legacy order summary response

BREAKING CHANGE: remove totalPrice field in favor of totals.grandTotal
```

## Anti-Patterns to Avoid

* `update code`
* `fix bug`
* `misc changes`
* `WIP`
* `final`
* `small fixes`
* `cleanup`
* `more changes`
* Overstuffed subjects listing many unrelated changes
* Mislabeling features as chores
* Omitting breaking change notes when migration is required

## Output Format

When asked to produce a commit message, return:

### Commit message

```text
<full conventional commit message>
```

### Rationale

* Briefly explain the selected type and scope when useful

## Default Standard

If no project-specific commit convention overrides this skill, default to:

* Conventional Commits format
* Lowercase type and scope
* Imperative subject
* Scope when helpful
* Subject under 72 characters
* Body for non-trivial changes
* Explicit breaking change notation when applicable
