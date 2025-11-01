# Setting Up the ajjent Project with Jujutsu

This project is designed to be used with **Jujutsu (jj)**, a modern version control system.

## Installation

### Option 1: Using Cargo (Recommended)
If you have Rust installed:

```bash
cargo install jj-cli
```

### Option 2: Using Homebrew (macOS)
```bash
brew install jujutsu
```

### Option 3: Pre-built Binaries
Download from: https://github.com/jj-vcs/jj/releases/latest

### Option 4: Using cargo-binstall
```bash
cargo binstall jj-cli
```

## Converting the Repository to jj

Once jj is installed, initialize the repository:

```bash
# Navigate to the project directory
cd ajjent

# Initialize jj with git backend (colocated)
jj git init
```

This creates a jj repository that is colocated with git, allowing both tools to work together.

## Verify the Setup

```bash
# Check jj is working
jj --version

# View the commit log
jj log

# Check status
jj status
```

## Project Structure

```
ajjent/
├── .git/                                    (git backend)
├── .jj/                                     (jj internal)
├── .github/
│   └── chatmodes/
│       └── ajjent.chatmode.md              (Agent specification)
├── jj-agent-prompt.md                      (System prompt)
├── jj-commands-reference.md                (Command reference)
└── SETUP.md                                (This file)
```

## Next Steps

1. Install jj following the instructions above
2. Initialize the repo: `jj git init`
3. Start using jj commands:
   - `jj log` - View history
   - `jj status` - Check working copy
   - `jj describe -m "message"` - Add descriptions
   - `jj new` - Create new commits

## Resources

- **Official Documentation**: https://martinvonz.github.io/jj/
- **Installation Guide**: https://martinvonz.github.io/jj/latest/install-and-setup/
- **Tutorial**: https://martinvonz.github.io/jj/latest/tutorial/
- **Git Comparison**: https://martinvonz.github.io/jj/latest/git-comparison/

## Why Jujutsu?

This project uses jj because:
1. **Safer workflow** - Can undo any operation
2. **Better history management** - Change IDs persist across rewrites
3. **Flexible branching** - Bookmarks are more explicit
4. **Consistent interface** - Works on any commit, not just HEAD
5. **Dogfooding** - We're building a jj expert agent, so we use jj!

## Colocated Git Backend

The `--git` flag initializes a colocated repository where:
- jj and git can both work on the same repository
- Commits are stored in git format
- Both `git` and `jj` commands work
- Easy collaboration with git-only users
- Can push to GitHub/GitLab using either tool

For more info: https://martinvonz.github.io/jj/latest/git-backend/
