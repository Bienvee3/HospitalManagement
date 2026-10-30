# Git workflow (Lab 4)

## Working agreement

Work starts from a GitHub Issue and a current `main` branch. A branch uses
`<issue-number>-<story-or-task-id>-<short-description>`, for example
`150-t-l4-1-workflow-strategy`. Each commit contains one logical change, uses
imperative wording, and references the issue: `Add Git workflow guide (#150)`.

The normal path is: create the linked branch, make and inspect changes with
`git status` and `git diff`, commit, push, open a pull request with
`Closes #<issue-number>`, self-review the diff, squash-merge, then update
`main`, delete the local branch, and run `git fetch --prune`.

## Safe day-to-day commands

- Stage deliberately with `git add <path>` and inspect staged content with
  `git diff --staged` before committing.
- Use `git restore --staged <path>` to unstage without losing work. Use
  `git revert <commit>` for a published mistake; do not rewrite shared history.
- Use `git stash push -u -m "WIP: <description>"` before an interruption.
  `-u` includes untracked files. Use `pop` to restore and remove the stash, or
  `apply` when it must remain available.
- Run `git fetch` before integrating remote work. Use `git pull --rebase` only
  on the personal feature branch and resolve conflicts before pushing. Never
  force-push `main`; use `--force-with-lease` only after rebasing one's own
  branch.

## Merge and conflict policy

Pull requests into `main` use **Squash and merge**. It gives `main` one clear,
issue-linked commit per completed task while branches stay short lived. The
author reviews their own diff: scope, tests, documentation, secrets, and issue
closure wording.

For a conflict, inspect `git status`, the conflict markers, and the common
ancestor when needed. Keep the intended combination by editing the file, then
`git add <file>` and continue the active operation (`git commit`,
`git rebase --continue`, or `git cherry-pick --continue`). If the correct
outcome is unclear, abort the operation and resolve the requirement in the
Issue before retrying.

## Lab 4 evidence

Task #150 is the real-task cycle: it is created from its Issue, uses this
linked branch, has at least two issue-referencing commits, includes a stash
interruption, is reviewed through a pull request, and is released as `v0.1.0`.
The practice repositories and their commit graphs are documented in
`docs/branching-strategy.md`.
