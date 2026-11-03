
# Advanced Git Commands

This document contains essential Git commands for inspecting changes, managing files, navigating project history, and safely undoing changes.

## 1. Inspecting Changes

### git status

Displays the current state of the working directory and staging area.

```bash
git status
```

### git status --short

Displays a compact version of the repository status.

```bash
git status --short
```

Common status codes:

- `??` : Untracked file
- `A` : Added file
- `M` : Modified file
- `D` : Deleted file

The first column represents the staging area, and the second column represents the working directory.

### git diff

Shows unstaged changes between the working directory and the staging area.

```bash
git diff
```

### git diff --staged

Shows changes that have been staged but not committed.

```bash
git diff --staged
```

### git diff HEAD

Shows all changes in the working directory compared with the latest commit, including staged and unstaged changes.

```bash
git diff HEAD
```

### Compare commits

Compares the contents of two commits.

```bash
git diff <commit1> <commit2>
```

### Compare branches

Shows differences between two branch snapshots.

```bash
git diff main..feature/example
```

## 2. Inspecting Commit History

### git log

Displays the commit history.

```bash
git log
```

### git log --oneline

Displays commits in a compact format.

```bash
git log --oneline
```

### git show

Displays information about a commit, including its changes.

```bash
git show
```

To inspect a specific commit:

```bash
git show <commit-hash>
```

## 3. Commit Message Guidelines

A good commit message should clearly describe the purpose of the change.

Examples:

```bash
git commit -m "Add user authentication"
git commit -m "Fix database connection error"
git commit -m "Update project documentation"
```

Common Conventional Commit prefixes:

- `feat:` New feature
- `fix:` Bug fix
- `docs:` Documentation changes
- `refactor:` Code restructuring
- `test:` Test-related changes
- `chore:` Maintenance tasks

Example:

```bash
git commit -m "docs: add advanced Git commands"
```

## 4. Working with .gitignore

The `.gitignore` file specifies untracked files and directories that Git should ignore.

Example:

```gitignore
# Python
__pycache__/
*.py[cod]

# Virtual environments
.venv/
venv/

# Environment variables
.env

# Logs
*.log

# IDE
.idea/

# Operating system
.DS_Store
Thumbs.db
```

Important: `.gitignore` does not automatically stop tracking files that have already been committed.

To stop tracking a file while keeping it locally:

```bash
git rm --cached <file>
```

To stop tracking a directory:

```bash
git rm -r --cached <directory>
```

## 5. Restoring Files

### git restore

Discards unstaged changes in a file by restoring it from the staging area.

```bash
git restore <file>
```

Warning: This discards the unstaged changes in that file.

### git restore --staged

Removes a file from the staging area without discarding its working-directory changes.

```bash
git restore --staged <file>
```

### git restore --source

Restores a file from a specific commit.

```bash
git restore --source=<commit-hash> <file>
```

## 6. Navigating Previous Commits

### git checkout

Checks out a specific commit.

```bash
git checkout <commit-hash>
```

Checking out a commit directly usually puts Git into a detached HEAD state.

To return to the main branch:

```bash
git switch main
```

For inspecting an old version of a file, prefer:

```bash
git show <commit-hash>:<file>
```

## 7. Removing Untracked Files

### git clean --dry-run

Previews which untracked files would be removed.

```bash
git clean -n
```

### git clean -f

Removes untracked files.

```bash
git clean -f
```

### git clean -fd

Removes untracked files and directories.

```bash
git clean -fd
```

Warning: These commands permanently remove files from the working directory. Always preview with `git clean -n` first.

## 8. Git Reset

`git reset` moves the current branch pointer and can also change the staging area and working directory.

### git reset --soft

Moves HEAD to the previous commit while keeping changes staged.

```bash
git reset --soft HEAD~1
```

### git reset --mixed

Moves HEAD and resets the staging area while keeping working-directory changes.

```bash
git reset --mixed HEAD~1
```

This is the default reset mode.

```bash
git reset HEAD~1
```

### git reset --hard

Moves HEAD, resets the staging area, and discards tracked working-directory changes.

```bash
git reset --hard HEAD~1
```

Warning: This operation can permanently discard work. Use it carefully.

## 9. Git Revert

`git revert` creates a new commit that reverses the changes introduced by an earlier commit.

```bash
git revert <commit-hash>
```

Unlike reset, revert does not remove the previous commit from history.

### Resolving revert conflicts

If a revert causes conflicts:

1. Open the conflicted files.
2. Resolve the conflicts.
3. Stage the resolved files.
4. Continue the revert.

```bash
git add <file>
git revert --continue
```

To cancel the revert operation:

```bash
git revert --abort
```

## 10. Reset vs Revert

| Command | Main Purpose |
|---|---|
| `git reset` | Moves the branch pointer and may modify staged or working changes |
| `git revert` | Creates a new commit that reverses an earlier commit |

Use revert when undoing changes in shared or published history. Reset is generally more appropriate for local history that has not been shared.

---

## Important Safety Notes

- Always inspect changes with `git status` and `git diff`.
- Use `git clean -n` before removing untracked files.
- Be careful with `git reset --hard`.
- Avoid rewriting published history without coordinating with collaborators.
- Never commit passwords, API keys, or sensitive environment files.
