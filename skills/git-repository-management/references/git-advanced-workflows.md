---
name: git-advanced-workflows
description: Use advanced Git workflows to keep history clean, recover from mistakes, and manage multi-branch collaboration safely.
---

# Git Advanced Workflows

Use this reference for branch cleanup, selective history edits, backports, regression hunts, and recovery.

## When to Load It

- Cleaning feature branches before a PR
- Reordering, squashing, or splitting commits
- Backporting a fix across release branches
- Recovering from a bad reset or deleted branch
- Finding the commit that introduced a bug
- Working across multiple branches without losing context

## Safety Baseline

Before risky operations:

1. Check `git status` and make sure the working tree state is understood.
2. Check whether commits are already shared upstream.
3. Create a backup branch before complex rebases or resets.
4. Prefer `--force-with-lease` if a rewritten branch must be pushed.

```bash
git status
git branch backup/<topic>
git push --force-with-lease origin <branch>
```

## Interactive Rebase

Use interactive rebase to clean local history.

Common actions:

- `pick`: keep commit
- `reword`: change commit message
- `edit`: stop and modify commit contents
- `squash`: combine with previous commit and keep both messages
- `fixup`: combine with previous commit and discard this message
- `drop`: remove commit

Common commands:

```bash
git rebase -i HEAD~5
git rebase -i $(git merge-base HEAD main)
git rebase -i <commit>
```

Use it to:

- squash typo or follow-up commits
- reword unclear messages
- reorder commits into a logical story
- drop accidental noise before review

## Autosquash

Use fixup commits plus autosquash for safe cleanup.

```bash
git commit -m "feat: add user authentication"
git commit --fixup HEAD
git rebase -i --autosquash main
```

## Split a Commit

When one commit mixes concerns:

```bash
git rebase -i HEAD~3
# mark the commit as edit
git reset HEAD^
git add path/to/file1
git commit -m "feat: add validation"
git add path/to/file2
git commit -m "feat: add error handling"
git rebase --continue
```

## Cherry-Pick

Use cherry-pick to apply a specific change without merging a whole branch.

```bash
git cherry-pick <commit>
git cherry-pick <start>..<end>
git cherry-pick -n <commit>
git cherry-pick -e <commit>
```

Typical uses:

- backport a hotfix to release branches
- bring a single safe fix into another branch
- stage a picked change without committing yet

If conflicts appear:

```bash
git cherry-pick --continue
git cherry-pick --abort
```

## Bisect

Use `git bisect` to find the first bad commit by binary search.

```bash
git bisect start
git bisect bad
git bisect good <known-good-commit-or-tag>
```

Then test each checked-out commit and mark it:

```bash
git bisect good
git bisect bad
git bisect reset
```

Automated variant:

```bash
git bisect start HEAD <known-good-commit-or-tag>
git bisect run ./test.sh
```

The test script should exit `0` for good and a non-zero code for bad, except `125`.

## Worktrees

Use worktrees when you need multiple branches checked out at once.

```bash
git worktree list
git worktree add ../project-feature feature/new-feature
git worktree add -b hotfix/urgent ../project-hotfix main
git worktree remove ../project-feature
git worktree prune
```

Prefer the dedicated worktree reference when the task is primarily about safe setup and baseline verification.

## Reflog Recovery

Use reflog to recover from bad resets, deleted branches, or lost commits.

```bash
git reflog
git reflog show <branch>
git branch recovered-branch <commit>
git checkout <commit>
```

Typical recovery flow:

```bash
git reflog
# find the lost commit
git reset --hard <commit>
```

Or recover without moving `HEAD`:

```bash
git branch recovery/<topic> <commit>
```

## Rebase vs Merge

Prefer rebase when:

- cleaning up your local branch
- updating a private feature branch on top of `main`
- creating a linear PR history that is easier to review

Prefer merge when:

- integrating completed work into a shared branch
- preserving the exact collaboration history matters
- the branch is already public and used by others

## Common Recovery Commands

```bash
git rebase --abort
git merge --abort
git cherry-pick --abort
git bisect reset
git restore --source=<commit> path/to/file
git reset --soft HEAD^
git reset --hard HEAD^
```

## Practical Patterns

- Clean PR branch: interactive rebase, autosquash, test, then `push --force-with-lease`
- Hotfix backport: commit once, cherry-pick onto release branches, validate each branch
- Regression hunt: use `bisect` with an automated test when possible
- Risky history rewrite: create `backup/<topic>` first, then edit history

## Common Pitfalls

- Rebasing public branches used by teammates
- Force-pushing without lease
- Editing history without a backup branch
- Running `bisect` on a dirty working tree
- Forgetting to clean up stale worktrees
