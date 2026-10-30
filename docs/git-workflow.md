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

Issue [#150](https://github.com/Bienvee3/HospitalManagement/issues/150) is the
real task for this guide and uses the linked branch
`150-t-l4-1-workflow-strategy`. Its first issue-referencing commit added this
guide and the `.gitignore`. A stash interruption and restore was also
performed locally while an unrelated change was committed on the
`lab4-stash-interruption` branch; that practice commit is not part of this
task's pull request.

The issue's card is in progress on the Hospital Management Project. GitHub
branch protection is enabled on `main`: pull requests are required, direct
pushes, force pushes, and branch deletion are blocked, and no second approval
is required. CI checks can be made mandatory once the CI workflow exists.

The task is not complete until a second issue-referencing commit is included
in a pull request with `Closes #150`, the change is self-reviewed and merged,
and the annotated `v0.1.0` tag and GitHub Release are published. Do not infer
completion from this document alone.
