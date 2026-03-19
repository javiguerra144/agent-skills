---
name: "using-git-worktrees"
description: "Use when starting feature work that needs isolation from the current workspace or before executing implementation plans. Creates isolated git worktrees with smart directory selection and safety verification."
---

# Using Git Worktrees

## Overview

Git worktrees create isolated workspaces sharing the same repository, allowing work on multiple branches simultaneously without switching.

Core principle: systematic directory selection plus safety verification equals reliable isolation.

Announce at start: "I'm using the using-git-worktrees skill to set up an isolated workspace."

## Directory Selection Process

Follow this priority order:

### 1. Check Existing Directories

```bash
# Check in priority order
ls -d .worktrees 2>/dev/null
ls -d worktrees 2>/dev/null
```

If found: use that directory. If both exist, `.worktrees` wins.

### 2. Check CLAUDE.md

```bash
grep -i "worktree.*director" CLAUDE.md 2>/dev/null
```

If a preference is specified, use it without asking.

### 3. Ask User

If no directory exists and no `CLAUDE.md` preference:

```text
No worktree directory found. Where should I create worktrees?

1. .worktrees/ (project-local, hidden)
2. ~/.config/superpowers/worktrees/<project-name>/ (global location)

Which would you prefer?
```

## Safety Verification

### For Project-Local Directories (`.worktrees` or `worktrees`)

Verify the directory is ignored before creating the worktree:

```bash
git check-ignore -q .worktrees 2>/dev/null || git check-ignore -q worktrees 2>/dev/null
```

If the directory is not ignored:

1. Add the appropriate line to `.gitignore`
2. Commit the change
3. Proceed with worktree creation

Why this matters: it prevents accidentally committing worktree contents into the repository.

### For Global Directory (`~/.config/superpowers/worktrees`)

No `.gitignore` verification is needed because the directory is outside the project.

## Creation Steps

### 1. Detect Project Name

```bash
project=$(basename "$(git rev-parse --show-toplevel)")
```

### 2. Create Worktree

```bash
case $LOCATION in
  .worktrees|worktrees)
    path="$LOCATION/$BRANCH_NAME"
    ;;
  ~/.config/superpowers/worktrees/*)
    path="~/.config/superpowers/worktrees/$project/$BRANCH_NAME"
    ;;
esac

git worktree add "$path" -b "$BRANCH_NAME"
cd "$path"
```

### 3. Run Project Setup

Auto-detect and run the appropriate setup:

```bash
if [ -f package.json ]; then npm install; fi
if [ -f Cargo.toml ]; then cargo build; fi
if [ -f requirements.txt ]; then pip install -r requirements.txt; fi
if [ -f pyproject.toml ]; then poetry install; fi
if [ -f go.mod ]; then go mod download; fi
```

### 4. Verify Clean Baseline

Run tests to ensure the worktree starts clean:

```bash
npm test
cargo test
pytest
go test ./...
```

If tests fail, report the failures and ask whether to proceed or investigate.

If tests pass, report that the worktree is ready.

### 5. Report Location

```text
Worktree ready at <full-path>
Tests passing (<N> tests, 0 failures)
Ready to implement <feature-name>
```

## Quick Reference

| Situation | Action |
|-----------|--------|
| `.worktrees/` exists | Use it and verify ignored |
| `worktrees/` exists | Use it and verify ignored |
| Both exist | Use `.worktrees/` |
| Neither exists | Check `CLAUDE.md`, then ask user |
| Directory not ignored | Add to `.gitignore` and commit |
| Tests fail during baseline | Report failures and ask |
| No package manifest found | Skip dependency install |

## Common Mistakes

### Skipping Ignore Verification

- Problem: worktree contents get tracked and pollute git status
- Fix: always use `git check-ignore` before creating a project-local worktree

### Assuming Directory Location

- Problem: creates inconsistency and ignores project conventions
- Fix: follow priority order of existing directory, then `CLAUDE.md`, then ask

### Proceeding with Failing Tests

- Problem: it becomes unclear whether later failures are pre-existing
- Fix: report failures and get explicit permission to proceed

### Hardcoding Setup Commands

- Problem: breaks on projects using different tools
- Fix: auto-detect from project files

## Example Workflow

```text
You: I'm using the using-git-worktrees skill to set up an isolated workspace.

[Check .worktrees/ - exists]
[Verify ignored - git check-ignore confirms .worktrees/ is ignored]
[Create worktree: git worktree add .worktrees/auth -b feature/auth]
[Run npm install]
[Run npm test - 47 passing]

Worktree ready at /Users/jesse/myproject/.worktrees/auth
Tests passing (47 tests, 0 failures)
Ready to implement auth feature
```

## Red Flags

Never:

- Create a worktree without verifying it is ignored for project-local directories
- Skip baseline test verification
- Proceed with failing tests without asking
- Assume directory location when ambiguous
- Skip `CLAUDE.md` checks

Always:

- Follow directory priority: existing, then `CLAUDE.md`, then ask
- Verify ignore status for project-local locations
- Auto-detect and run project setup
- Verify a clean test baseline

## Integration

Called by:

- `brainstorming` when design is approved and implementation follows
- `subagent-driven-development` before executing tasks
- `executing-plans` before executing tasks
- Any skill needing an isolated workspace

Pairs with:

- `finishing-a-development-branch` for cleanup after work completes
