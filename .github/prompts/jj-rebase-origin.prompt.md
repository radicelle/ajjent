---
mode: ajjent
description: 'Fetch latest origin and rebase local commits safely on top'
model: Claude Haiku 4.5
---

# jj Rebase Origin (jj-rebase-origin) Workflow

Sync local commits with latest origin state by fetching and rebasing safely.

## Goal

Guide the user to fetch the latest from origin and rebase their local commits on top of origin/main, handling conflicts if needed, then push cleanly.

## Key Principle

Rebasing keeps history linear and clean. Always fetch first, review what will move, handle conflicts as they appear, and use `jj undo` as your safety net.

Always encourage the user to:
- Fetch before any rebase to ensure latest state
- Review commits with `jj log -r main@origin..@`
- Handle conflicts immediately with `jj resolve`
- Use `--force-with-lease` for safe pushes
- Leverage undo to recover from any misstep
