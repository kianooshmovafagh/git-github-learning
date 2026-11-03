
# Advanced Git - Practical Exercises

This document contains practical exercises for learning advanced Git commands.

The exercises are designed to practice inspecting changes, managing files, navigating commit history, and undoing changes safely.

> Important: Perform destructive operations in a temporary test repository, not in your main learning repository.

---

## Exercise 1: Inspecting Changes

**Objective:** Understand the difference between working directory changes and staged changes.

### Tasks

1. Create a new file named `notes.txt`.
2. Add some text to the file.
3. Run `git status`.
4. Run `git diff`.
5. Stage the file using `git add`.
6. Run `git diff --staged`.
7. Modify the file again.
8. Run `git diff` and compare the output.

### Commands

```bash
git status
git diff
git add notes.txt
git diff --staged
git diff
```

**Expected Result:** Understand how Git displays unstaged and staged changes separately.

---

## Exercise 2: Inspecting Commit History

**Objective:** Learn how to inspect previous commits.

### Tasks

1. Display the commit history.
2. Display the history in one-line format.
3. Inspect the latest commit.
4. Inspect a specific commit using its hash.

### Commands

```bash
git log
git log --oneline
git show
git show <commit-hash>
```

**Expected Result:** Understand how to find and inspect previous commits.

---

## Exercise 3: Working with .gitignore

**Objective:** Prevent unnecessary files from being tracked.

### Tasks

1. Create a `.gitignore` file.
2. Add common Python patterns.
3. Create a `.env` file for testing.
4. Check the repository status.
5. Confirm that ignored files do not appear as untracked files.

### Example .gitignore

```gitignore
__pycache__/
*.py[cod]
.venv/
.env
*.log
```

**Expected Result:** Understand how Git ignores untracked files.

---

## Exercise 4: Restoring Files

**Objective:** Practice restoring files and unstaging changes.

### Tasks

1. Modify an existing test file.
2. Run `git restore <file>` to discard unstaged changes.
3. Modify the file again.
4. Stage the changes.
5. Run `git restore --staged <file>`.
6. Check the repository status.

### Commands

```bash
git restore <file>
git restore --staged <file>
git status
```

**Expected Result:** Understand the difference between restoring working-directory changes and unstaging changes.

---

## Exercise 5: Removing Untracked Files

**Objective:** Learn how to safely remove untracked files.

### Tasks

1. Create a temporary untracked file.
2. Run `git clean -n`.
3. Review the files that would be removed.
4. Run `git clean -f` only after confirming the preview.

### Commands

```bash
git clean -n
git clean -f
```

**Expected Result:** Understand how to preview and remove untracked files safely.

---

## Exercise 6: Git Reset

**Objective:** Understand the three reset modes.

Perform this exercise only in a temporary test repository.

### Tasks

1. Create and commit a test file.
2. Make another change and commit it.
3. Test `git reset --soft HEAD~1`.
4. Inspect the staging area.
5. Recreate the test commits.
6. Test `git reset --mixed HEAD~1`.
7. Inspect the working directory and staging area.
8. Recreate the test commits.
9. Test `git reset --hard HEAD~1` only with disposable test data.

### Commands

```bash
git reset --soft HEAD~1
git reset --mixed HEAD~1
git reset --hard HEAD~1
```

**Expected Result:** Understand how each reset mode affects HEAD, the staging area, and the working directory.

---

## Exercise 7: Git Revert

**Objective:** Undo a commit without deleting it from history.

### Tasks

1. Create a test commit.
2. Find its commit hash.
3. Revert the commit.
4. Inspect the new commit.
5. Review the commit history.

### Commands

```bash
git log --oneline
git revert <commit-hash>
git log --oneline
```

**Expected Result:** Understand how revert creates a new commit that reverses an earlier commit.

---

## Exercise 8: Comparing Branches

**Objective:** Compare the contents of two branches.

### Tasks

1. Create a test branch.
2. Make a change and commit it.
3. Compare the branch with `main`.
4. Review the differences.

### Commands

```bash
git switch -c feature/test-comparison
git diff main..feature/test-comparison
```

**Expected Result:** Understand how to compare the snapshots of two branches.

---

## Exercise 9: Commit Message Practice

**Objective:** Write clear and meaningful commit messages.

### Tasks

Write commit messages for the following scenarios:

1. Adding a new feature.
2. Fixing a bug.
3. Updating documentation.
4. Refactoring existing code.
5. Adding tests.

### Examples

```bash
git commit -m "feat: add user registration"
git commit -m "fix: handle invalid login credentials"
git commit -m "docs: update installation guide"
git commit -m "style: update formatting"
git commit -m "refactor: simplify database service"
git commit -m "test: add authentication tests"
```

**Expected Result:** Develop the habit of writing descriptive commit messages.

---

## Learning Checklist

- [x] Inspect unstaged and staged changes.
- [x] Review commit history.
- [x] Create and use `.gitignore`.
- [x] Restore files and unstage changes.
- [x] Preview and remove untracked files.
- [x] Understand `git reset --soft`.
- [x] Understand `git reset --mixed`.
- [x] Understand `git reset --hard`.
- [x] Undo commits using `git revert`.
- [x] Compare branches.
- [x] Write meaningful commit messages.

---

## Final Notes

Advanced Git commands should be used carefully.

Always inspect repository status before and after operations.

Destructive commands such as `git clean -f` and `git reset --hard` should be practiced only with disposable test data until their behavior is fully understood.
