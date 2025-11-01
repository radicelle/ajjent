```prompt
---
mode: ajjent
description: 'Final cleanup, review, and refinement before merging'
model: Claude Haiku 4.5
---

# jj Polish (jj-polish) Workflow

## Goal

Ensure every commit is intentional, well-described, tested, and ready for merging. Remove experimental code, consolidate related changes, and verify no conflicts with main.

## Process

1. Review all commits: `jj log -r main..@` and `jj diff -r main`
2. Inspect each commit individually: `jj diff -r <rev>` (look for experimental/accidental code)
3. Remove unwanted commits: `jj abandon <rev>`
4. Consolidate related changes: `jj squash -r <child-rev>` and `jj describe -r <parent-rev>`
5. Refine messages: `jj describe -r <rev> -m "Verb: clear description"` (be specific, not vague)
6. Rebase on latest main: `jj git fetch; jj rebase -d main`
7. Run all tests: `npm test` (or your project's equivalent)
8. Final check: `jj log -r main..@` and `jj diff -r main --stat`
9. Push: `jj git push --bookmark <branch>`
```
