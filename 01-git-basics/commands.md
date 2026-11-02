# Git Basics - Commands Reference

## 1. Git Configuration

Check Git version:

```bash
git --version
```

Set username:

```bash
git config --global user.name "Your Name"
```

Set email:

```bash
git config --global user.email "your@email.com"
```

View configuration:

```bash
git config --list
```

## 2. Repository Initialization

Initialize a repository:

```bash
git init
```

Check repository status:

```bash
git status
```

## 3. Staging Changes

Stage a specific file:

```bash
git add file.txt
```

Stage all changes:

```bash
git add .
```

Unstage a file:

```bash
git restore --staged file.txt
```

## 4. Creating Commits

Create a commit:

```bash
git commit -m "commit message"
```

Stage tracked modified files and commit them:

```bash
git commit -am "commit message"
```

Note: `git commit -am` does not automatically include new untracked files.

## 5. Commit History

Show commit history:

```bash
git log
```

Show compact commit history:

```bash
git log --oneline
```

Show a graphical history:

```bash
git log --oneline --all --graph
```

Show the latest commit:

```bash
git show
```

Show a specific commit:

```bash
git show commit-hash
```

## 6. Git Diff

Show unstaged changes:

```bash
git diff
```

Show staged changes:

```bash
git diff --staged
```

Compare two commits:

```bash
git diff commit1 commit2
```

## 7. Git Aliases

Create an alias:

```bash
git config --global alias.st status
```

Use the alias:

```bash
git st
```

## 8. Git Ignore

Create a `.gitignore` file and specify files or directories that Git should ignore.

Example:

```gitignore
.env
__pycache__/
*.log
venv/
```

## 9. Restoring and Cleaning Files

Discard changes in a tracked file:

```bash
git restore file.txt
```

Remove untracked files interactively:

```bash
git clean -i
```

Preview untracked files that would be removed:

```bash
git clean -n
```

Remove untracked files:

```bash
git clean -f
```

## 10. Git Reset

Move HEAD and reset the staging area while keeping working directory changes:

```bash
git reset --soft HEAD~1
```

Reset the staging area but keep working directory changes:

```bash
git reset --mixed HEAD~1
```

Reset HEAD, staging area, and working directory:

```bash
git reset --hard HEAD~1
```

**Warning:** `git reset --hard` discards uncommitted changes in tracked files.

## 11. Git Revert

Create a new commit that reverses a previous commit:

```bash
git revert commit-hash
```

Revert the latest commit:

```bash
git revert HEAD
```

## Important Notes

- `git add` moves changes into the staging area.
- `git commit` records staged changes.
- `git diff` compares working directory changes with the staging area.
- `git diff --staged` compares staged changes with the latest commit.
- `git reset` moves the current branch reference and can change staging or working directory state.
- `git revert` reverses changes by creating a new commit.
- Always review the effects of destructive commands before running them.