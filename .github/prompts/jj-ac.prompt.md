---
mode: ajjent
description: 'Create clean, logical commits with one concern per commit'
model: Claude Haiku 4.5
---

# jj Atomic Commit (jj-ac) Workflow

Create commits where each represents a single focused logical change. One logical change = One commit.

## Goal

Guide the user toward creating atomic commits with clear intent, focusing on:
1. Understanding the single logical change before starting
2. Using `jj new -m "msg"` to create focused commits
3. Reviewing changes with `jj status` and `jj diff`
4. Splitting mixed concerns with `jj split -r <rev>` or squashing over-splits with `jj squash -r <rev>`
5. Using `jj undo` safely to recover from mistakes

## Key Principle

Each commit should be independently understandable and represent one concern. This improves code review, bisecting, and history clarity.

Always encourage the user to:
- Plan the change before coding
- Review diffs to catch mixed concerns
- Use split/squash to maintain atomicity
- Leverage undo for safe experimentation