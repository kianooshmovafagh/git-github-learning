
# Git Merge Commands

This file contains commonly used Git merge commands with practical examples and explanations.

## 1. Basic Merge

### Merge a Branch into the Current Branch

```bash
git merge branch-name
```

Merges the specified branch into the current branch.

**Example:**

```bash
git switch main
git merge feature/login
```

In this example:
- `git switch main` switches to the `main` branch.
- `git merge feature/login` merges `feature/login` into the current branch (`main`).

**Important:** The branch you want to merge into must be the current branch.

## 2. Fast Forward Merge

A Fast Forward Merge happens when the target branch has no new commits since the source branch was created.

Git simply moves the target branch pointer forward without creating a merge commit.

**Command:**

```bash
git merge branch-name
```

**Example:**

```bash
git switch main
git merge feature/login
```

If a Fast Forward Merge is possible, Git performs it automatically by default.

### Fast Forward Only Merge

```bash
git merge --ff-only branch-name
```

Allows a merge only when Git can perform a Fast Forward Merge.

If a Fast Forward Merge is not possible, Git refuses to merge the branches.

**Why use it?**

- Prevents unexpected merge commits.
- Keeps the commit history linear.
- Ensures that the merge can be completed using Fast Forward only.

## 3. Non-Fast-Forward Merge

A Non-Fast-Forward Merge creates a new merge commit, even when Git could perform a Fast Forward Merge.

**Command:**

```bash
git merge --no-ff branch-name
```

**Example:**

```bash
git switch main
git merge --no-ff feature/login
```

The `--no-ff` option forces Git to create a merge commit.

**Why use it?**

- Keeps the history of feature branches visible.
- Makes it easier to identify when a feature was merged.
- Preserves a clear record of integration points.

## 4. Merge Conflicts

A Merge Conflict happens when Git cannot automatically combine changes from different branches.

This usually happens when:
- Two branches modify the same lines in a file.
- One branch deletes a file while another branch modifies it.
- Git cannot determine which changes should be kept.

### Check Merge Status

```bash
git status
```

Shows the current state of the repository and identifies files with merge conflicts.

### Abort a Merge

```bash
git merge --abort
```

Cancels the current merge operation and attempts to return the repository to its state before the merge started.

### Continue After Resolving Conflicts

After manually resolving all conflicts:

```bash
git add filename
git merge --continue
```

- `git add` stages the resolved file and marks its conflicts as resolved.
- `git merge --continue` continues the merge operation.

Alternatively, you can use:

```bash
git commit
```

to complete the merge by creating the merge commit.

**Important:** Make sure all conflicted files are resolved and staged before continuing the merge.

## 5. Inspect Merge History

### View Commit History

```bash
git log --oneline --graph --all
```

Displays the commit history as a graph.

This command is useful for:
- Understanding branch relationships.
- Identifying merge commits.
- Seeing how branches have diverged and merged.

### Show Commit Details

```bash
git show commit-hash
```

Displays detailed information about a specific commit, including changes and commit metadata.

## 6. Useful Merge Commands

### Check Current Branch

```bash
git branch
```

Lists local branches and marks the current branch with an asterisk (`*`).

### Check Working Directory Status

```bash
git status
```

Shows the current state of the working directory and staging area.

### View Differences

```bash
git diff
```

Shows unstaged changes in the working directory.

### View Staged Differences

```bash
git diff --staged
```

Shows changes that have been staged but not committed.
