```prompt
---
mode: ajjent
description: 'Squash and consolidate related commits into logical units'
model: Claude Haiku 4.5
---

# jj Combine Commits (jj-combine-commits) Workflow

## Intent

Consolidate multiple small related commits into single logical units before merging.

**Key Principle**: Many small commits with related concerns  Fewer cohesive commits with clear intent.

## When to Use

- Before creating a merge request
- After finishing a feature with many small commits
- Cleaning up "WIP" or experimental commits
- Preparing history for code review
- Removing intermediate fix-up commits

## Workflow

### 1. Review your commits
```bash
jj log -r main..@          # See all your commits
jj diff -r <rev>           # Review each commit
```

### 2. Identify which to combine
Group related commits (e.g., "Add function" + "Fix function" + "Add tests for function").

### 3. Squash into parent
```bash
jj squash -r <child-rev>   # Move child into parent
# Repeat until group is consolidated
```

### 4. Update parent message
```bash
jj describe -r <parent-rev> -m "Clear combined message"
```

### 5. Review result
```bash
jj log
jj diff -r <parent-rev>
```

## Key Commands

| Command | Purpose |
|---------|---------|
| `jj squash -r <rev>` | Move commit into parent |
| `jj describe -r <rev> -m "msg"` | Update message |
| `jj log -r @-5::@` | View last 5 commits |
| `jj diff -r <rev>` | Review specific commit |
| `jj undo` | Undo last squash |
| `jj op log` | See operation history |
| `jj op restore <op-id>` | Restore to previous state |

## Quick Reference

```bash
# Review commits
jj log -r main..@
jj diff -r <rev>

# Combine related commits
jj squash -r <child>
jj describe -r <parent> -m "Updated message"

# Review
jj log
jj diff -r <parent>

# If wrong
jj undo
jj op restore <op-id>
```

## Examples

### Simple: Combine 2 commits
```bash
# Commit B: "Add function", Commit C: "Add tests for function"
jj squash -r C
# Now B contains both function and tests
```

### Multiple groups
```bash
# You have: A, B, C (database), D, E (auth)
# Combine B and C into A
jj squash -r B
jj squash -r C

# Then combine D and E
jj squash -r E
```

## Related Workflows

- **jj-ac**: Creates atomic commits that may later need combining
- **jj-rebase-origin**: After rebasing, use this to consolidate
- **jj-polish**: Final pass after combining

---
**Remember**: Squash to create clear, logical history. Parent message is keptupdate it to reflect combined changes.
```
