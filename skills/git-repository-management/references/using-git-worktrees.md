---
name: using-git-worktrees
description: Use Git worktrees to create isolated workspaces safely, with directory selection, ignore verification, setup, and clean baseline checks.
---

# Using Git Worktrees

Use this reference when the task needs an isolated workspace instead of modifying the current checkout.

## When to Prefer a Worktree

- Starting feature work without disturbing the current branch
- Handling a hotfix while other work stays open
- Testing risky rebases or branch surgery in isolation
- Running parallel efforts on different branches

## Directory Selection Order

Follow this order:

1. Use `.worktrees/` if it already exists.
2. Otherwise use `worktrees/` if it already exists.
3. Otherwise check `CLAUDE.md` for a preferred worktree location.
4. If none exists, ask the user where to create worktrees.

If both `.worktrees/` and `worktrees/` exist, prefer `.worktrees/`.

## Ignore Verification

For project-local worktree directories, verify they are ignored before creation:

```bash
git check-ignore -q .worktrees || git check-ignore -q worktrees
```

If the chosen directory is not ignored:

1. Add it to `.gitignore`
2. Commit that change if the workflow requires repository hygiene first
3. Then create the worktree

Why it matters: it prevents the worktree contents from polluting repository status.

Global worktree directories do not need `.gitignore` checks.

## Creation Flow

Detect project name:

```bash
project=$(basename "$(git rev-parse --show-toplevel)")
```

Create a worktree for an existing branch:

```bash
git worktree add <path> <branch>
```

Create a worktree and branch in one step:

```bash
git worktree add -b <branch> <path> <start-point>
```

## Baseline Setup

After creating the worktree:

1. Change into the new directory
2. Install dependencies based on the project manifests present
3. Run the relevant test or validation command
4. Confirm the baseline is clean before implementation starts

Examples:

```bash
npm install
pytest
cargo test
go test ./...
```

If baseline validation fails, report that before doing feature work.

## Report Back

When setup succeeds, report:

- full worktree path
- branch name
- whether setup completed
- whether baseline validation passed

## Red Flags

Never:

- create a project-local worktree without verifying ignore rules
- assume a directory when project conventions already exist
- skip baseline verification on active development repos
- proceed silently when setup or tests fail
