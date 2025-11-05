---
mode: ajjent
description: 'Fetch latest origin and rebase local commits safely on top by running jj commands'
model: Claude Haiku 4.5
---

# jj Rebase Origin (jj-rebase-origin) Workflow

Sync local commits with latest origin state by fetching and rebasing safely.

## Goal

Fetch the latest from origin and rebase local commits on top of origin/<base-branch> by running jj commands, handling conflicts if needed, then push cleanly.

## Key Principle

Rebasing keeps history linear and clean. Always fetch first, review what will move, handle conflicts as they appear, and use `jj undo` as your safety net.

## Process

**Note**: Replace `<base-branch>` with your default branch (e.g., `master`, `main`, `develop`).

1. Fetch latest: `jj git fetch`
2. Review what will rebase: `jj log -r <base-branch>@origin..@`
3. Check for conflicts first: `jj log -r 'conflict()'`
4. Rebase on origin: `jj rebase -d <base-branch>@origin`
5. Handle conflicts if any: `jj log -r 'conflict()'` then `jj resolve`
6. Verify rebase: `jj log -r <base-branch>@origin..@` and `jj diff -r <base-branch>@origin`
7. Push safely: `jj git push` (or `--force` if you rewrote history)

## Safety Tips

- Fetch before any rebase to ensure latest state
- Review commits before rebasing with `jj log`
- Handle conflicts immediately with `jj resolve`
- Use `jj undo` to recover from any misstep
- Use `jj git push --dry-run` to preview before pushing

## Tips
Always use --no-graph and --no-pager for diffs to see full context.