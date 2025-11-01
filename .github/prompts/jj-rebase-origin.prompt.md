```prompt
---
mode: ajjent
description: 'Fetch latest origin and rebase local commits safely on top'
model: Claude Haiku 4.5
---

# jj Rebase Origin (jj-rebase-origin) Workflow

## Intent

Fetch latest from origin and rebase your local commits safely while preserving all your changes.

**Key Principle**: Get latest remote state, reset your branch point to origin, rebase your commits on top.

## When to Use

- Remote has moved ahead and you want clean sync
- Before creating a pull request with latest main
- Recovering from incomplete or botched push
- Re-synchronizing before continuing work
- Syncing multiple feature branches

## Core Steps

### 1. Fetch latest from origin
```bash
jj git fetch    # Updates remote bookmarks
```

### 2. See your commits
```bash
jj log -r main@origin..@    # What you'll add on top of origin/main
```

### 3. Rebase onto origin/main
```bash
jj rebase -d main@origin    # All your commits rebased in one command

# Or to target only your commits explicitly:
jj rebase -r main..@ -d main@origin
```

### 4. Handle conflicts (if any)
```bash
jj resolve --list           # See which commits have conflicts
jj edit <conflicted-rev>    # Open editor to fix
# ... resolve conflict markers ...
jj resolve <file>           # Mark file resolved
# Or resolve all at once:
jj resolve --all
```

### 5. Verify and push
```bash
jj log
jj diff
jj git push --force-with-lease --bookmark <branch>
```

## Key Commands

| Command | Purpose |
|---------|---------|
| `jj git fetch` | Update remote bookmarks |
| `jj log -r main@origin..@` | See commits to rebase |
| `jj rebase -d main@origin` | Rebase onto origin/main |
| `jj rebase -r main..@ -d main@origin` | Rebase only your commits |
| `jj resolve --list` | See conflicted commits |
| `jj edit <rev>` | Edit a commit directly |
| `jj resolve <file>` | Mark file resolved |
| `jj resolve --all` | Resolve all conflicts |
| `jj undo` | Undo rebase if wrong |
| `jj op log` | See operation history |

## Quick Reference

```bash
# Fetch and rebase
jj git fetch
jj rebase -d main@origin

# Review
jj log -r main@origin..@
jj diff -r <rev>

# Handle conflicts
jj resolve --list
jj edit <conflicted-rev>
jj resolve --all

# Push
jj git push --force-with-lease --bookmark <branch>

# If wrong
jj undo
```

## Examples

### Simple: Rebase feature branch
```bash
jj git fetch
jj rebase -d main@origin
jj git push --force-with-lease --bookmark feature
```

### With conflicts
```bash
jj git fetch
jj rebase -d main@origin
# jj detects conflicts in one commit

jj resolve --list
jj edit <conflicted-commit>
# ... fix conflicts in editor ...
jj resolve --all

jj git push --force-with-lease --bookmark feature
```

### Keep only some commits
```bash
jj git fetch
jj rebase -d main@origin

# Abandon unwanted commits
jj abandon <unwanted-1>
jj abandon <unwanted-2>

jj git push --force-with-lease --bookmark feature
```

## Safety Tips

- Always fetch first: `jj git fetch`
- Use `--force-with-lease` instead of `--force` (safer)
- Review what will rebase: `jj log -r main@origin..@`
- Don't rebase main itself: `jj rebase -r main -d main@origin` is wrong
- Use `jj undo` to recover from mistakes

## Related Workflows

- **jj-ac**: Creates atomic commits that you'll rebase
- **jj-combine-commits**: After rebasing, consolidate if needed
- **jj-polish**: Final cleanup before merge after rebase

---
**Remember**: jj's rebase is explicit and safe. You can see exactly what's happening, and `jj undo` gets you back if needed.
```
