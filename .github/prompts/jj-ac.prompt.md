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
2. Amend working copy with `jj describe` as you go through blocks of related changes
3. Use `jj new` to create focused commits
4. Reviewing changes with `jj status` and `jj diff --no-pager` (| head -100 for large diffs)
5. Push

## Key Principle

Each commit should be independently understandable and represent one concern. This improves code review, bisecting, and history clarity.
Always use --no-graph and --no-pager for diffs to see full context.