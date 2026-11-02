# Git Branching Commands

## 1. List Local Branches

```bash
git branch
```

Lists all local branches. The asterisk (`*`) indicates the current branch.

## 2. List All Branches

```bash
git branch -a
```

Lists all local and remote-tracking branches.

## 3. Create a New Branch

```bash
git branch feature/login
```

Creates a new branch without switching to it.

## 4. Create and Switch to a New Branch

```bash
git switch -c feature/login
```

Creates a new branch and switches to it.

## 5. Switch Between Branches

```bash
git switch main
```

Switches to the specified branch.

## 6. Rename the Current Branch

```bash
git branch -m new-branch-name
```

Renames the current branch.

## 7. Rename Another Branch

```bash
git branch -m old-branch-name new-branch-name
```

Renames a branch without switching to it.

## 8. Delete a Branch

```bash
git branch -d feature/login
```

Deletes a local branch if Git considers it safely merged.

## 9. Force Delete a Branch

```bash
git branch -D feature/login
```

Force deletes a local branch, even if it has unmerged commits.

**Warning:** This may cause unmerged work to become harder to recover.

## 10. Show Branch Information

```bash
git branch -v
```

Displays each local branch with its latest commit.

## 11. Show Detailed Branch Information

```bash
git branch -vv
```

Displays local branches, their latest commits, and upstream tracking information when configured.

## 12. Show Merged Branches

```bash
git branch --merged
```

Lists branches whose commits are already included in the current branch.

## 13. Show Unmerged Branches

```bash
git branch --no-merged
```

Lists branches that contain commits not merged into the current branch.

## 14. View Commit History of All Branches

```bash
git log --oneline --all --graph
```

Displays a compact graphical history of commits across all branches.

## Important Notes

- Branches allow independent development.
- Creating a branch does not duplicate the entire project.
- Each branch points to a commit.
- Commits made on one branch do not automatically appear on another branch.
- A branch cannot normally be deleted while it is currently checked out.
- The `-d` option is safer than `-D` because it checks whether the branch has been merged.
