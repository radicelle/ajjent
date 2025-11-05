---
mode: ajjent
description: 'Squash and consolidate related commits into logical units by running jj commands'
model: Claude Haiku 4.5
---

# jj Combine Commits (jj-combine-commits) Workflow

## Goal

Consolidate multiple small related commits into logical by running jj commands, cohesive units.

## Process

1. Review your commits: `jj log -r main..@` and `jj diff -r <rev>` to inspect each
2. Group related commits together (e.g., "Add function" + "Fix function" + "Add tests")
3. Squash children into parents: `jj squash -r <child-rev>` (moves child INTO parent, repeat bottom-up for each group)
4. Update parent message: `jj describe -r <parent-rev> -m "Clear combined message"`
5. Verify result: `jj log` and `jj diff -r <parent-rev>`
6. If wrong, undo: `jj undo` or `jj op restore <op-id>`

## Key Commands

- `jj squash -r <rev>` – Move commit into parent
- `jj squash -r <rev> -i` – Interactively choose which changes to squash
- `jj describe -r <rev> -m "msg"` – Update message
- `jj log -r main..@` – View your commits
- `jj diff -r <rev>` – Inspect changes in a commit
- `jj undo` – Undo last operation (use cautiously)
- `jj op restore <op-id>` – Restore to a specific operation (advanced - use cautiously)
