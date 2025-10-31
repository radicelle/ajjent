# Jujutsu (jj) Command Reference - Compact Guide

## Core Concepts

- **Working Copy (@)**: The current commit being edited. Changes are automatically committed.
- **Change ID**: Unique identifier for a change (stable across rewrites)
- **Commit ID**: Hash of the commit content (changes when commit is rewritten)
- **Operation Log**: History of all operations performed on the repo
- **Revsets**: Functional language for selecting revisions (e.g., `@`, `@-`, `main..@`)

---

# Category 1: Initialization & Setup

## Repository Creation

### `jj init`

Create a new jj repository.

```bash
jj init                  # Initialize new repo
jj init --git            # Initialize with git backend
jj init --git-repo <path>  # Initialize pointing to existing git repo
```

### `jj git clone`

Clone a repository.

```bash
jj git clone <url>              # Clone repository
jj git clone --colocate <url>   # Clone with colocated git repo
```

## Workspace Setup

### `jj workspace add`

Create additional workspaces (multiple working copies).

```bash
jj workspace add <path>         # Add new workspace
jj workspace add --name <name> <path>  # Add with specific name
```

### `jj workspace list`

List all workspaces.

```bash
jj workspace list
```

### `jj workspace root`

Show workspace root directory.

```bash
jj workspace root
jj root                  # Shortcut
```

## Remote Configuration

### `jj git remote`

Manage remotes.

```bash
jj git remote list              # List remotes
jj git remote add <name> <url>  # Add remote
jj git remote remove <name>     # Remove remote
jj git remote rename <old> <new>  # Rename remote
jj git remote set-url <name> <url>  # Change remote URL
```

## Initial Configuration

### `jj config`

Configure jj settings.

```bash
jj config list          # List all config
jj config get <key>     # Get config value
jj config set --user <key> <value>  # Set user config
jj config set --repo <key> <value>  # Set repo config
jj config edit --user   # Edit user config file
jj config edit --repo   # Edit repo config file
jj config path          # Show config file paths
```

### Common Initial Settings

```bash
# Set user identity
jj config set --user user.name "Your Name"
jj config set --user user.email "you@example.com"

# Set default editor
jj config set --user ui.editor "vim"

# Configure diff/merge tools
jj config set --user ui.diff-editor "meld"
jj config set --user merge-tools.meld.program "meld"
```

## Bookmarks (Branch) Setup

### `jj bookmark create`

Create bookmarks for tracking work.

```bash
jj bookmark create <name>           # Create at @
jj bookmark create <name> -r <rev>  # Create at specific revision
```

### `jj bookmark track`

Track remote bookmarks.

```bash
jj bookmark track <name>@<remote>   # Start tracking remote bookmark
jj bookmark list --all              # List all bookmarks including remotes
```

## File Tracking Configuration

### `jj file track/untrack`

Configure which files to track.

```bash
jj file track <pattern>    # Track files matching pattern
jj file untrack <pattern>  # Untrack files matching pattern
```

### Sparse Checkout

```bash
jj sparse set <patterns>   # Set sparse patterns
jj sparse list             # Show current patterns
```

---

# Category 2: Logging & Inspection

## Viewing History

### `jj log`

Display commit history as a graph.

```bash
jj log                    # Show commit history
jj log -r <revset>       # Show specific revisions
jj log -r @              # Show current commit
jj log -r @-             # Show parent commit
jj log -r ::@            # Show ancestors of @
jj log -r main..@        # Show range from main to @
jj log --no-graph        # Linear output without graph
jj log -T <template>     # Use custom template
jj log --limit 20        # Limit number of commits shown
jj log --reversed        # Show oldest first
```

### Useful Log Patterns

```bash
jj log -r 'main..@'      # Your changes on current branch
jj log -r 'empty()'      # Show empty commits
jj log -r 'merges()'     # Show merge commits
jj log -r 'description("bug")' # Search by description
jj log -r 'author("alice")'    # Filter by author
jj log -r '@-10::@'      # Last 10 commits
```

## Examining Commits

### `jj show`

Show complete information about a commit.

```bash
jj show                 # Show current commit
jj show <rev>          # Show specific revision
jj show --summary      # Show summary only
jj show --stat         # Show diffstat
```

### `jj status` / `jj st`

Show working copy status.

```bash
jj status              # Show working copy state
jj status              # Shows current commit info and changes
```

## Viewing Changes

### `jj diff`

Show changes in commits.

```bash
jj diff                  # Diff of working copy changes
jj diff -r <rev>        # Diff of specific revision
jj diff -r @-           # Diff of parent commit
jj diff --from <r1> --to <r2>  # Diff between revisions
jj diff --git           # git-style diff format
jj diff --stat          # Show diffstat
jj diff --summary       # Show summary of changes
jj diff <path>          # Diff specific file/path
```

### `jj interdiff`

Compare changes between two commits.

```bash
jj interdiff --from <r1> --to <r2>  # Compare commit changes
```

## Evolution & History

### `jj evolog`

Show evolution history of a change.

```bash
jj evolog              # Show evolution of @
jj evolog -r <rev>    # Show evolution of specific revision
jj evolog -l 10       # Limit to 10 entries
```

### `jj op log` / `jj operation log`

Show operation history.

```bash
jj op log               # Show operation log
jj op log --limit 20    # Show recent operations
jj op log --no-graph    # Linear format
jj op show <op-id>      # Show specific operation details
```

## File Inspection

### `jj file list`

List tracked files.

```bash
jj file list            # List all tracked files
jj file list -r <rev>  # List files in specific revision
jj file list <pattern>  # List files matching pattern
```

### `jj file show`

Show file contents.

```bash
jj file show <path>           # Show file from @
jj file show <path> -r <rev>  # Show file from revision
```

## Bookmark & Tag Inspection

### `jj bookmark list`

List bookmarks.

```bash
jj bookmark list              # List local bookmarks
jj bookmark list --all        # Include remote bookmarks
jj bookmark list --tracked    # Show only tracked bookmarks
```

### `jj tag list`

List tags.

```bash
jj tag list                   # List all tags
```

## Conflict Inspection

### `jj resolve --list`

List conflicted paths.

```bash
jj resolve --list       # Show all conflicts
```

## Revset Reference for Logging

### Basic Selectors

```bash
@                       # Current commit (working copy)
@-                      # Parent of current commit
@--                     # Grandparent
<bookmark>              # Commit at bookmark
<change-id>             # Commit by change ID
root()                  # The root commit
```

### Operators

```bash
::@                     # All ancestors of @
@::                     # All descendants of @
main..@                 # Range from main to @
(main..@)::             # Branch including descendants
x | y                   # Union of sets
x & y                   # Intersection
x ~ y                   # Difference
```

### Functions

```bash
ancestors(x)            # All ancestors
descendants(x)          # All descendants
parents(x)              # Direct parents
children(x)             # Direct children
heads(x)                # Heads in set
roots(x)                # Roots in set
empty()                 # Empty commits
merges()                # Merge commits
description("pattern")  # By description
author("pattern")       # By author
bookmarks()             # Bookmarked commits
```

---

# Category 3: Merging & Rebasing

## Creating & Modifying Commits

### `jj new`

Create a new commit.

```bash
jj new                   # Create new commit on top of @
jj new <rev>            # Create new commit on top of revision
jj new <rev1> <rev2>    # Create merge commit with multiple parents
jj new -m "message"     # Create with description
jj new --insert-after <rev>  # Insert new commit after revision
jj new --insert-before <rev> # Insert new commit before revision
```

### `jj describe`

Set or edit commit description.

```bash
jj describe              # Edit description of @ in $EDITOR
jj describe -m "message" # Set description directly
jj describe -r <rev>     # Describe a specific revision
jj describe -r <rev> --reset-author  # Reset author to current user
```

### `jj commit`

Finalize current change.

```bash
jj commit -m "message"   # Commit with message, create new @
jj commit                # Opens editor for message
```

### `jj edit`

Edit a specific commit.

```bash
jj edit <rev>           # Make <rev> the working copy commit
```

## Moving Changes Between Commits

### `jj squash`

Move changes into parent commit.

```bash
jj squash                # Squash @ into its parent
jj squash -r <rev>      # Squash specific revision into parent
jj squash -i             # Interactive mode (select changes)
jj squash -i -r <rev>    # Interactive squash of revision
jj squash --from <rev>   # Squash from revision into @
jj squash --into <rev>   # Squash @ into specific revision
```

### `jj split`

Split a commit into multiple commits.

```bash
jj split                 # Interactive split of @
jj split -r <rev>       # Split specific revision
```

### `jj move`

Move changes between commits.

```bash
jj move --from <source> --to <dest>  # Move changes
jj move --from <source>              # Move to @
jj move --from <source> -i           # Interactive selection
```

### `jj diffedit`

Edit changes in a commit interactively.

```bash
jj diffedit             # Edit changes in @
jj diffedit -r <rev>   # Edit changes in specific commit
jj diffedit --from <rev1> --to <rev2>  # Edit diff range
```

### `jj absorb`

Automatically move changes to appropriate ancestors.

```bash
jj absorb               # Absorb working copy changes
jj absorb --from <rev>  # Absorb from specific revision
```

## Rebasing

### `jj rebase`

Move commits to new parent(s).

```bash
# Basic rebasing
jj rebase -d <dest>              # Rebase @ to destination
jj rebase -s <source> -d <dest>  # Rebase source and descendants
jj rebase -b <rev> -d <dest>     # Rebase entire branch
jj rebase -r <rev> -d <dest>     # Rebase single revision only

# Insert commits into history
jj rebase -r <rev> --insert-after <target>   # Insert after target
jj rebase -r <rev> --insert-before <target>  # Insert before target
jj rebase -r <rev> -A <target>               # Shorthand for insert-after
jj rebase -r <rev> -B <target>               # Shorthand for insert-before

# Advanced: Multiple destinations
jj rebase -r <rev> -d <dest1> -d <dest2>     # Create merge with multiple parents
```

### Rebase Strategies

```bash
# Rebase your work onto updated main
jj rebase -s <your-base> -d main@origin

# Rebase single commit without descendants
jj rebase -r <commit> -d <new-parent>

# Insert commit between parent and child
jj rebase -r <commit> --insert-before <child>
```

## Merging

### Creating Merges

```bash
# Create merge commit
jj new <parent1> <parent2>              # Merge two commits
jj new <p1> <p2> <p3>                   # Octopus merge (multiple parents)
jj new <p1> <p2> -m "Merge description" # With description
```

### `jj resolve`

Resolve merge conflicts.

```bash
jj resolve              # Launch merge tool for conflicts
jj resolve <file>       # Resolve specific file
jj resolve --list       # List conflicted files
jj resolve --tool <tool>  # Use specific merge tool
```

### Conflict Strategies

```bash
# View conflicts
jj log -r 'conflict()'  # Show all commits with conflicts
jj resolve --list       # List conflicted paths

# Resolve conflicts
jj resolve              # Interactive resolution
jj diffedit             # Edit conflict markers directly
jj restore --from <rev> <path>  # Take version from specific commit
```

## History Manipulation

### `jj abandon`

Abandon commits (remove from history).

```bash
jj abandon <rev>        # Abandon revision (descendants reparented)
jj abandon              # Abandon @
jj abandon <rev1> <rev2>  # Abandon multiple commits
```

### `jj duplicate`

Create copy of a commit.

```bash
jj duplicate <rev>      # Duplicate revision
jj duplicate <rev1> <rev2>  # Duplicate multiple
```

### `jj parallelize`

Remove parent-child relationship between commits.

```bash
jj parallelize <revset>    # Make commits parallel/sibling
jj parallelize @- @        # Make @ a sibling of its parent
```

### `jj simplify-parents`

Remove redundant parents from merge commits.

```bash
jj simplify-parents           # Simplify @ if it's a merge
jj simplify-parents -r <rev>  # Simplify specific merge
```

### `jj revert`

Apply inverse of changes from revisions.

```bash
jj revert -r <rev>      # Revert changes from revision
jj revert -r <rev> -d <dest>  # Revert to destination
```

## Synchronizing with Remotes

### `jj git fetch`

Fetch from remotes.

```bash
jj git fetch               # Fetch from all remotes
jj git fetch --remote <name>  # Fetch from specific remote
jj git fetch --all-remotes    # Explicitly fetch all
```

### `jj git push`

Push changes to remotes.

```bash
jj git push                     # Push tracked bookmarks
jj git push --bookmark <name>   # Push specific bookmark
jj git push --all               # Push all bookmarks
jj git push --change <change>   # Push specific change
jj git push -c <rev>            # Create bookmark and push
jj git push --dry-run           # Show what would be pushed
jj git push --force             # Force push (careful!)
```

### Update Workflows

```bash
# Fetch and rebase onto updated main
jj git fetch
jj rebase -d main@origin

# Fetch and merge
jj git fetch
jj new @ main@origin -m "Merge main"
```

## Bookmark Management

### `jj bookmark set/delete`

Manage bookmarks.

```bash
jj bookmark set <name> -r <rev>     # Move bookmark to revision
jj bookmark delete <name>           # Delete local bookmark
jj bookmark forget <name>           # Forget bookmark everywhere
jj bookmark rename <old> <new>      # Rename bookmark
```

### `jj bookmark track/untrack`

Manage remote bookmark tracking.

```bash
jj bookmark track <name>@<remote>   # Start tracking remote
jj bookmark untrack <name>@<remote> # Stop tracking
```

## Navigation

### `jj next` / `jj prev`

Navigate through history.

```bash
jj next                 # Move to child commit
jj next --edit          # Move to child and edit
jj next --conflict      # Move to next conflict
jj prev                 # Move to parent commit
jj prev --edit          # Move to parent and edit
jj prev 2               # Move back 2 commits
```

## Undo & Recovery

### `jj undo`

Undo last operation.

```bash
jj undo                 # Undo last operation
jj undo --operation <id>  # Undo specific operation
```

### `jj op restore`

Restore to specific operation state.

```bash
jj op restore <op-id>   # Restore repo to operation state
```

### `jj op revert`

Revert an operation (create inverse).

```bash
jj op revert <op-id>    # Create operation that undoes specified op
```

## Advanced Techniques

### `jj restore`

Restore paths from another revision.

```bash
jj restore <path>              # Restore path from @-
jj restore --from <rev> <path> # Restore from specific revision
jj restore --to <rev> <path>   # Restore into revision
```

### `jj fix`

Run code formatters/fixers.

```bash
jj fix                  # Fix @ 
jj fix -s <rev>        # Fix revision and descendants
```

## Common Merge/Rebase Workflows

### Interactive History Editing

```bash
# Edit a commit in the middle of history
jj edit <commit-id>
# ... make changes ...
jj describe -m "Updated commit"
jj edit @-  # Return to where you were

# Split a commit
jj split -r <commit-id>

# Combine commits
jj squash -r <commit1> --into <commit2>
```

### Resolving Conflicts

```bash
# After rebase with conflicts
jj log -r 'conflict()'   # Find conflicted commits
jj new <conflicted>      # Create resolution commit on top
jj resolve               # Resolve conflicts
jj squash                # Squash resolution into conflicted
```

### Updating Feature Branch

```bash
# Rebase approach
jj git fetch
jj rebase -s <feature-start> -d main@origin

# Merge approach
jj git fetch
jj new @ main@origin -m "Merge main into feature"
```

### Cleaning Up History

```bash
# Squash fixup commits
jj squash -r <fixup-commit>

# Abandon empty or unwanted commits
jj abandon <commit>

# Reorder commits
jj rebase -r <commit> -d <new-parent>
```

---

## Tips for Merging & Rebasing

1. **Conflicts don't block**: You can commit and continue with conflicts
2. **Rebase preserves change IDs**: Change IDs stay stable across rebases
3. **Insert commits anywhere**: Use `--insert-before/after` to restructure
4. **Interactive is your friend**: Use `-i` for surgical precision
5. **Undo is always available**: `jj undo` reverses any operation
6. **Multiple parents**: Use `jj new <p1> <p2>` to create merges
7. **Test before pushing**: Use `jj git push --dry-run` to preview
