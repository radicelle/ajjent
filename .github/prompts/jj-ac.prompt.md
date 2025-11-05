---
mode: ajjent
description: 'Create clean, logical commits with one concern per commit by running jj commands'
model: Claude Haiku 4.5
---

# jj Atomic Commit (jj-ac) Workflow

Create commits where each represents a single focused logical change. One logical change = One commit. It can be a file, portion of a file, or a set of related files.

## Goal

Create atomic commits with clear intent by running jj commands, focusing on:
1. Understanding the single logical change before starting
2. Using `jj new -m "msg"` to create focused commits
3. Reviewing changes with `jj status` and `jj diff --no-pager`
4. Splitting mixed concerns with `jj split` (or `jj split -r <rev>` for specific revisions)
5. Squashing over-splits with `jj squash` (or `jj squash -r <rev>`)
6. Using `jj undo` safely to recover from mistakes (avoid as much as possible)

## Key Principle

Each commit should be independently understandable and represent one concern. This improves code review, bisecting, and history clarity.

Always encourage the user to:
- Plan the change before coding
- Review diffs to catch mixed concerns (`jj diff` or `jj show`)
- Use split/squash to maintain atomicity
- Leverage undo for safe experimentation