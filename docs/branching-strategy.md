# Branching strategy (Lab 5)

## Decision

This individual, four-sprint project uses **GitHub Flow (feature branching)**.
It suits one developer because each task gets a short-lived, issue-linked
branch; it supports parallel work without maintaining a long-lived `develop`
branch; and it works directly with the planned CI/CD triggers on pull requests,
`main`, and `v*` tags. Git Flow would add release and merge-back overhead with
no team or release cadence benefit, while trunk-based development requires a
more mature automated test suite and feature-flag discipline than the project
currently has.

## Branches, review, and release

- `main` is the only permanent branch, always releasable, and accepts changes
  only through a pull request. GitHub branch protection enforces this policy,
  including for administrators; direct pushes, force pushes, and deletion are
  disabled. Approvals are not required for this individual project.
- Task branches are created from an Issue and named
  `<issue-number>-<story-or-task-id>-<short-description>`.
- The author self-reviews the PR, checking scope, automated checks,
  documentation, secrets, and `Closes #<issue-number>`. PRs use **Squash and
  merge**; head branches are deleted after merging.
- Releases use annotated Semantic Versioning tags on `main`:
  `vMAJOR.MINOR.PATCH`. `v0.1.0` is the first working release.
- Once CI exists, its lint and test checks must also be required before merge.

```text
main:     A------M------R (v0.1.0)
                 ^
task:       B---C   squash merge
             issue-linked, short lived
```

## Conflict policy

The branch author resolves conflicts against current `main`, preferring a
manual edit that preserves the accepted intent. During a rebase, `ours` is the
branch being rebased onto and `theirs` is the replayed commit. If intent is
ambiguous, the operation is aborted and the Issue is clarified; no side is
chosen merely to make Git continue.

## Practice evidence

The public repository list does not contain the four `branching-*` practice
repositories described in the earlier draft. Their exercises must not be
treated as completed evidence. The existing merged PR for issue `#3` verifies
the feature-branch/PR workflow only; it does not demonstrate trunk-based
development, Git Flow, or the conflict exercises.

At the project owner's request, practice repositories will not be published
publicly. Any remaining Lab 5 hands-on exercises need local evidence before
they can be marked complete. The forking exercise also needs a second GitHub
identity or a partner, so it remains blocked until one is available.
