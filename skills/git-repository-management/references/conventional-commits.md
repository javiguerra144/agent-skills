---
name: conventional-commits
description: Draft and review Git commit messages using Conventional Commits so history stays clear, searchable, and automation-friendly.
---

# Conventional Commits

Use this reference when writing or reviewing commit messages.

## Goal

Produce commit history that is:

- Accurate to the actual diff
- Easy to scan in logs and PRs
- Consistent across contributors
- Useful for changelogs and release automation

## Core Format

```text
<type>(<scope>): <subject>

<body>

<footer>
```

- `type` is required
- `scope` is optional but recommended when it adds clarity
- `subject` is required
- `body` is recommended for non-trivial changes
- `footer` is for breaking changes, issue references, or metadata

## Default Types

- `feat`: new user-visible behavior
- `fix`: bug fix
- `refactor`: structural change without behavior change
- `perf`: measurable performance improvement
- `test`: adding or updating tests
- `docs`: documentation-only changes
- `style`: formatting or non-functional style-only changes
- `build`: build system or dependency tooling changes
- `ci`: CI/CD workflow changes
- `chore`: maintenance that does not change product behavior
- `revert`: reverting a previous commit

Do not hide meaningful product work behind `chore`.

## Scope Rules

- Keep scope short and lowercase
- Prefer one scope
- Match project terminology when it exists
- Omit scope if it adds no signal

Examples:

- `feat(auth): add email magic link login`
- `fix(api): handle empty filter params`
- `docs: update local setup instructions`

## Subject Rules

- Use imperative mood
- Keep it specific
- Start with a lowercase word after the colon
- Avoid trailing punctuation
- Prefer under 72 characters

Good:

- `add invoice status filter`
- `prevent duplicate webhook processing`
- `extract shared date formatter`

Avoid:

- `fix bug`
- `misc changes`
- `WIP`
- `final commit`

## Body Rules

Add a body when the subject alone is not enough.

Explain:

- Why the change was needed
- What approach was chosen
- Any important tradeoffs or behavior changes

Keep it factual and concise. Favor intent and impact over diff narration.

## Breaking Changes

Mark breaking changes with either:

```text
feat(api)!: replace legacy order summary response
```

or:

```text
refactor(auth): replace session payload structure

BREAKING CHANGE: session.user.id is now session.user.userId
```

Use both when the migration impact needs explanation.

## Selection Workflow

Before drafting the message:

1. Identify the dominant purpose of the change.
2. Choose the narrowest accurate type.
3. Add scope only if it improves scanning.
4. Keep the subject action-oriented.
5. Add a body for non-trivial or risky changes.
6. Mark breaking changes explicitly.

Priority hints:

- Prefer `feat` for new behavior
- Prefer `fix` for incorrect behavior
- Prefer `refactor` for internal cleanup
- Prefer `docs` for documentation-only changes
- Prefer `test` for test-only changes

## Quick Examples

```text
feat(checkout): add saved card selection
fix(search): handle empty query without 500 response
refactor(ui): extract reusable modal footer actions
perf(api): cache product detail responses for 60 seconds
test(auth): add regression coverage for expired reset tokens
build(deps): upgrade prisma to 6.2.0
ci: run typecheck before docker build
```

## Review Checklist

1. Is the type accurate?
2. Is the scope useful and concise?
3. Does the subject describe the actual change?
4. Is the subject imperative and specific?
5. Does the body explain why for non-trivial changes?
6. Is any breaking change clearly marked?
7. Will the message still make sense months later?
