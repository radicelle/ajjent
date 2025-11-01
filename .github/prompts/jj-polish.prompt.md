```prompt
---
mode: ajjent
description: 'Final cleanup, review, and refinement before merging'
model: Claude Haiku 4.5
---

# jj Polish (jj-polish) Workflow

## Intent

Final pass before merging: review commits, clean messages, remove experimental code, verify tests pass.

**Key Principle**: Every commit must be intentional, well-described, tested, and adds value.

## When to Use

- Right before pushing a branch
- Before creating a merge/pull request
- Final check before merging to main
- Before tagging a release
- When handing off to code review

## Polish Checklist

- [ ] All commits are intentional (no experimental code)
- [ ] Each commit message is clear and imperative
- [ ] Related changes are grouped together
- [ ] No duplicate or redundant commits
- [ ] All tests pass
- [ ] No merge conflicts with main
- [ ] Changes ordered logically
- [ ] Each commit is self-contained
- [ ] No large unrelated changes mixed together

## Workflow

### 1. Review your branch
```bash
jj log -r main..@       # See all your commits
jj diff -r main         # See all changes combined
```

### 2. Inspect each commit
```bash
jj diff -r <rev>       # Review each commit individually
# Look for: experimental code, accidental changes, incomplete work
```

### 3. Remove unwanted commits
```bash
jj abandon <experimental-rev>   # Drop unwanted commits
```

### 4. Consolidate related changes
```bash
jj squash -r <child-rev>
jj describe -r <parent-rev> -m "Clear message"
```

### 5. Refine messages
```bash
jj describe -r <rev> -m "Verb: clear, specific description"
# Good: "Add email validation for user signup"
# Bad: "Update stuff" or "Fix bug"
```

### 6. Rebase on latest main (if needed)
```bash
jj git fetch
jj rebase -d main
```

### 7. Run full tests
```bash
npm test          # or your project's test command
cargo test        # or other language equivalent
```

### 8. Final review
```bash
jj log -r main..@
jj diff -r main --stat   # Summary of changes
```

### 9. Push for review/merge
```bash
jj git push --bookmark <branch>
# Or with force-with-lease if rebased:
jj git push --force-with-lease --bookmark <branch>
```

## Key Commands

| Command | Purpose |
|---------|---------|
| `jj log -r main..@` | See all your commits |
| `jj diff -r <rev>` | Review specific commit |
| `jj diff -r main` | See all changes combined |
| `jj abandon <rev>` | Remove unwanted commit |
| `jj describe -r <rev> -m "msg"` | Update message |
| `jj squash -r <rev>` | Combine into parent |
| `jj git fetch` | Get latest remote |
| `jj rebase -d main` | Rebase onto main |
| `jj git push --bookmark <branch>` | Push to remote |

## Quick Reference

```bash
# Review
jj log -r main..@
jj diff -r main

# Clean
jj abandon <unwanted>
jj squash -r <related>
jj describe -r <rev> -m "Better message"

# Test
npm test

# Rebase if needed
jj git fetch
jj rebase -d main

# Final check
jj log -r main..@
jj diff -r main --stat

# Push
jj git push --bookmark <branch>
```

## Related Workflows

- **jj-ac**: Used to create atomic commits that you then polish
- **jj-combine-commits**: Often used during polish to consolidate
- **jj-rebase-origin**: After rebasing, polish is your next step

---
**Remember**: Polish is your last chance to ensure quality. Spend 10 minutes here to save hours of confusion later.
```
