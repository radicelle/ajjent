# ajjent - Jujutsu Expert Agent

A comprehensive Jujutsu (jj) expert agent and documentation project for version control mastery.

> ⚠️ **Disclaimer**: This project is AI-generated and is not 100% accurate yet. While the content aims to be helpful and accurate, please verify critical information with the [official jj documentation](https://martinvonz.github.io/jj/) before relying on it in production environments. As the project matures, accuracy will improve significantly.

## Overview

**ajjent** provides:
- 🤖 A specialized AI agent for jj expertise and Git→jj migration
- 📚 Complete jj command reference organized into 3 categories
- 🎯 System prompts and chat mode configuration
- 📖 Comprehensive documentation for learners

## What's Included

### 1. Chatmode Configuration (`.github/chatmodes/ajjent.chatmode.md`)
A full AI agent specification that teaches users:
- jj fundamentals and core concepts
- All commands across 3 categories (Init, Logging, Merge/Rebase)
- Revset and template languages
- Git to jj migration patterns
- Real-world workflow examples

### 2. Command Reference (`jj-commands-reference.md`)
Complete command documentation organized by:
- **Initialization & Setup** - Repos, workspaces, remotes, configuration
- **Logging & Inspection** - History, status, changes, conflicts
- **Merging & Rebasing** - Commits, rebasing, merging, synchronization

### 3. Agent System Prompt (`jj-agent-prompt.md`)
Detailed instructions for AI agents including:
- Core expertise areas
- Revset language mastery
- Template language knowledge
- Common scenarios and workflows
- Migration guidance from Git

## Getting Started

### Prerequisites
- Jujutsu (jj) installed - [Installation Guide](SETUP.md)
- Git (for colocated repository)

### Quick Start

```bash
# 1. Install jj
cargo install jj-cli

# 2. Convert this repository to jj
jj init --git

# 3. View the commit log
jj log

# 4. Check your status
jj status
```

See [SETUP.md](SETUP.md) for detailed installation instructions.

## Project Structure

```
ajjent/
├── .github/
│   └── chatmodes/
│       └── ajjent.chatmode.md              # AI agent configuration
├── jj-agent-prompt.md                      # System prompt for agents
├── jj-commands-reference.md                # Command reference
├── SETUP.md                                # Installation & setup guide
└── README.md                               # This file
```

## Key Concepts in jj

### Working Copy is a Commit
The working copy (@) isn't separate from commits—it IS a commit that automatically amends as you make changes.

### No Staging Area
All changes in the working copy are included in the next commit. No `git add` needed.

### Change IDs Stay Stable
Change IDs remain the same across rebases and rewrites, unlike commit IDs.

### Undo Everything
Any operation can be undone with `jj undo`. Experimentation is safe.

### Conflicts Don't Block
Commits can exist with conflicts. You can work around them and resolve later.

## Common Workflows

### Making a Change
```bash
jj describe -m "Add feature"
# ... edit files ...
jj diff                    # Review changes
jj new                     # Create new working copy
```

### Updating from Upstream
```bash
jj git fetch
jj rebase -d main@origin
```

### Creating a Bookmark for Feature
```bash
jj bookmark create my-feature
jj git push --bookmark my-feature
```

### Interactive History Editing
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

The ajjent agent is built to:
1. **Teach jj concepts** - Explain philosophy, not just commands
2. **Help Git users migrate** - Map Git workflows to jj equivalents
3. **Provide practical guidance** - Real examples for real problems
4. **Emphasize safety** - Highlight undo capabilities
5. **Support learning** - Be encouraging about new paradigms

### Example Agent Interactions

**Q: How do I commit my changes?**
> In jj, your changes are already tracked! The working copy @ is itself a commit that auto-amends. To finalize:
> ```bash
> jj commit -m "Your message"
> ```
> Or just add a description without moving forward:
> ```bash
> jj describe -m "Your message"
> ```

**Q: How's this different from `git commit --amend`?**
> In jj, the working copy automatically amends as you change it—no explicit amend needed! But to amend your parent:
> ```bash
> jj squash    # Moves current changes into parent
> ```
> Or edit an older commit directly:
> ```bash
> jj edit <commit>    # Make it your working copy
> # ... edit ...
> jj edit @-          # Return to where you were
> ```

## Resources

- **Official jj Docs**: https://martinvonz.github.io/jj/
- **Installation Guide**: https://martinvonz.github.io/jj/latest/install-and-setup/
- **Tutorial**: https://martinvonz.github.io/jj/latest/tutorial/
- **Git Comparison**: https://martinvonz.github.io/jj/latest/git-comparison/
- **GitHub Repository**: https://github.com/jj-vcs/jj

## Why jj for This Project?

1. **Dogfooding** - Building a jj expert agent means using jj
2. **Better workflows** - Safer history editing, more intuitive model
3. **Community** - Growing ecosystem of jj users
4. **Philosophy alignment** - Version control should be safe and composable

## License

This project's documentation and agent specifications are provided as learning resources.

## Contributing

Improvements to the agent specifications, command reference, or documentation are welcome!

## Quick Reference

| Task | Command |
|------|---------|
| View history | `jj log` |
| Check status | `jj status` |
| Make changes | (edit files, they auto-snapshot) |
| Commit changes | `jj commit -m "msg"` |
| Set description | `jj describe -m "msg"` |
| Squash into parent | `jj squash` |
| Split commit | `jj split` |
| Rebase | `jj rebase -d <new-parent>` |
| Undo last op | `jj undo` |
| View changes | `jj diff` |
| Resolve conflicts | `jj resolve` |
| Fetch updates | `jj git fetch` |
| Push changes | `jj git push` |
| Create bookmark | `jj bookmark create <name>` |
| View operations | `jj op log` |
| Search revisions | `jj log -r '<revset>'` |

---

**Start your jj journey with ajjent!** 🚀
