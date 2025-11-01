# ajjent - Jujutsu Expert Agent

An AI-generated reference and agent specification for learning Jujutsu (jj), a modern version control system.

> **Note**: This project is AI-generated. While the content is well-structured and comprehensive, verify critical details with the [official jj documentation](https://martinvonz.github.io/jj/) before deploying to production.

## Overview

This repository includes:

- An AI agent specification for teaching jj concepts and workflows
- A complete command reference organized by functional category
- System prompts and chat mode configuration for integration
- Documentation resources for getting started with jj

## What's Included

**Chatmode Configuration** (`.github/chatmodes/ajjent.chatmode.md`)
- Full AI agent specification
- jj fundamentals and core concepts
- Complete command reference
- Revset and template language guides
- Git to jj migration patterns

**Command Reference** (`jj-commands-reference.md`)
- Commands organized by category: initialization, inspection, merge/rebase
- Detailed descriptions and examples
- Quick lookup for common tasks

**Agent System Prompt** (`jj-agent-prompt.md`)
- Instructions for using jj as an AI agent
- Coverage of core concepts and workflows
- Migration guidance for Git users

## Getting Started

### Prerequisites

- Jujutsu (jj) installed - [Installation Guide](SETUP.md)
- Git (for colocated repository)

### Quick Start

```bash
# Install jj
cargo install jj-cli

# Convert this repository to jj
jj init --git

# View the commit log
jj log

# Check your status
jj status
```

See [SETUP.md](SETUP.md) for detailed installation instructions.

## Project Structure

```
ajjent/
├── .github/
│   └── chatmodes/
│       └── ajjent.chatmode.md
├── jj-agent-prompt.md
├── jj-commands-reference.md
├── SETUP.md
└── README.md
```

## Core Concepts

**Working Copy is a Commit** - The working copy (@) is itself a commit that automatically amends as you make changes. There's no separate working state.

**No Staging Area** - All changes in the working copy are included in commits. No `git add` equivalent exists.

**Change IDs Stay Stable** - Change IDs remain the same across rebases and history rewrites, unlike commit IDs in Git.

**Undo Everything** - Operations can be undone with `jj undo`. This makes experimentation safe by default.

**Conflicts Don't Block** - Commits can exist with unresolved conflicts. You can work around them and resolve later.

## Common Workflows

**Making a Change**

```bash
jj describe -m "Add feature"
# ... edit files ...
jj diff
jj new
```

**Updating from Upstream**

```bash
jj git fetch
jj rebase -d main@origin
```

**Creating a Bookmark for Feature**

```bash
jj bookmark create my-feature
jj git push --bookmark my-feature
```

**Interactive History Editing**

```bash
# Squash into parent
jj squash -r <commit>

# Split into two
jj split -r <commit>

# Move to new location
jj rebase -r <commit> -d <new-parent>

# Undo if needed
jj undo
```

## Understanding the Agent

This agent is built to:

- Teach jj concepts and philosophy, not just commands
- Help Git users translate their existing workflows
- Provide practical guidance with real examples
- Emphasize safety and the ability to undo operations
- Support learning through clear explanations

### Example Interactions

**Q: How do I commit my changes?**

In jj, the working copy is already tracked as a commit. To finalize:

```bash
jj commit -m "Your message"
```

Or add a description without moving:

```bash
jj describe -m "Your message"
```

**Q: How's this different from Git's `--amend`?**

In jj, the working copy automatically amends as you change files. To amend your parent:

```bash
jj squash
```

Or edit an older commit:

```bash
jj edit <commit>
# ... make changes ...
jj edit @-
```

## Resources

- Official jj documentation: https://martinvonz.github.io/jj/
- Installation guide: https://martinvonz.github.io/jj/latest/install-and-setup/
- Tutorial: https://martinvonz.github.io/jj/latest/tutorial/
- Git comparison: https://martinvonz.github.io/jj/latest/git-comparison/
- GitHub repository: https://github.com/jj-vcs/jj

## Why jj?

This project uses jj for practical reasons:

- The VCS itself is well-designed and reflects thoughtful version control philosophy
- It provides safer history editing and fewer gotchas than Git
- The growing community around jj is building interesting tooling
- Working with jj reveals better patterns for version control workflows

## License

This project's documentation is provided as a learning resource.

## Contributing

Suggestions for improvements to the agent specifications, command reference, or documentation are welcome.

## Quick Reference

| Task | Command |
|------|---------|
| View history | `jj log` |
| Check status | `jj status` |
| Commit changes | `jj commit -m "msg"` |
| Set description | `jj describe -m "msg"` |
| Squash into parent | `jj squash` |
| Split commit | `jj split` |
| Rebase | `jj rebase -d <new-parent>` |
| Undo | `jj undo` |
| View changes | `jj diff` |
| Resolve conflicts | `jj resolve` |
| Fetch updates | `jj git fetch` |
| Push changes | `jj git push` |
| Create bookmark | `jj bookmark create <name>` |
| View operations | `jj op log` |
| Search revisions | `jj log -r '<revset>'` |
