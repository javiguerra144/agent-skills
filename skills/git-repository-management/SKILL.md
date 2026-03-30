---
name: "git-repository-management"
description: "Use when managing Git repositories end to end, including safe worktree setup, branch hygiene, rebasing, cherry-picking, bisect, reflog recovery, PR cleanup, and Conventional Commit messages."
---

# Git Repository Management

Use this skill for repository work that spans more than one Git concern. It combines isolated workspace setup, history management, recovery workflows, and commit-message standards in one installable skill.

## Use This Skill When

- Setting up isolated feature or hotfix work with worktrees
- Cleaning up a branch before review or merge
- Rebasing, autosquashing, splitting, or cherry-picking commits
- Recovering lost commits or branches with reflog
- Tracking down regressions with `git bisect`
- Standardizing commit history with Conventional Commits
- Managing feature, release, and hotfix flows without polluting the main workspace

## Default Approach

1. Decide whether the work needs isolation. If the change is risky, parallel, or long-running, start with a worktree.
2. Inspect branch state before history edits: current branch, upstream, uncommitted changes, and whether commits are already shared.
3. Prefer reversible operations. Create a backup branch before risky rebases or resets.
4. Keep changes atomic and finish with a Conventional Commit message that matches the actual diff.
5. Re-run relevant validation after rebases, cherry-picks, or commit surgery before pushing.
6. Use recovery tools like `reflog` and `bisect` instead of guessing.

## Fast Rules

- Never rewrite shared history unless it is clearly safe.
- Prefer `git push --force-with-lease` over `git push --force`.
- Verify project-local worktree directories are ignored before creating worktrees.
- Keep one logical change per commit whenever practical.
- Mark breaking changes explicitly with `!` or `BREAKING CHANGE:`.
- Abort in-progress rebase, merge, cherry-pick, or bisect cleanly before switching strategies.

## Reference Map

Load only what the task needs:

- `references/using-git-worktrees.md` -> safe workspace isolation, directory selection, ignore checks, setup, and baseline verification.
- `references/git-advanced-workflows.md` -> rebase, autosquash, cherry-pick, split commits, bisect, reflog, force-push safety, and recovery commands.
- `references/conventional-commits.md` -> commit message format, type selection, scope guidance, breaking changes, and review checklist.

## Suggested Routing

- If the task starts with new implementation or risky parallel work, read `references/using-git-worktrees.md` first.
- If the task is branch cleanup, release prep, backports, regressions, or recovery, read `references/git-advanced-workflows.md`.
- If the task is commit drafting or review, read `references/conventional-commits.md`.
- If the task spans worktree setup plus branch cleanup plus final commits, load all three references.

## Notes

- Prefer this skill over `using-git-worktrees` or `conventional-commits` when the request crosses multiple Git workflow concerns.
- The narrower skills still fit one-off requests that are only about worktree setup or only about commit-message drafting.
- Keep the repository's existing branching model and release conventions when they differ from generic examples.
