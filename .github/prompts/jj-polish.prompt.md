---
mode: ajjent
description: 'Final cleanup, review, and refinement before merging by running jj commands'
model: Claude Haiku 4.5
---

# jj Polish (jj-polish) Workflow

## Goal

Ensure every commit is intentional, well-described, tested, and ready for merging. Remove experimental code, consolidate related changes, and verify no conflicts with `<base-branch>` by running jj commands.

## Process

**Note**: Replace `<base-branch>` with your default branch (e.g., `master`, `main`, `develop`). Deduce from repo context or ask the user.

1. Review all commits: `jj log -r <base-branch>..@` and `jj diff -r <base-branch>`
2. Inspect each commit individually: `jj diff -r <rev>` (look for experimental/accidental code)
3. Remove unwanted commits: `jj abandon <rev>`
4. Consolidate related changes: `jj squash -r <child-rev>` into parent, then refine with `jj describe -r <parent-rev>`
5. Refine commit messages: `jj describe -r <rev> -m "Verb: clear description"` (be specific, not vague)
6. Rebase on latest base branch: `jj git fetch` then `jj rebase -d <base-branch>@origin`
7. Run all tests: `npm test` (or your project's equivalent)
8. Final check: `jj log -r <base-branch>..@` and `jj diff -r <base-branch> --stat`
9. Push changes: `jj git push --bookmark <branch>` (ensure bookmark is tracked)