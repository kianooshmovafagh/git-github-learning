
# Advanced Git

This section covers advanced Git commands and techniques used to inspect, manage, modify, and recover project history.

The goal is to understand how Git tracks changes, how different areas of a repository interact, and how to safely manage commits and working directory modifications.

## Learning Objectives

- Write clear and meaningful commit messages.
- Compare changes between the working directory, staging area, commits, and branches.
- Understand and configure `.gitignore`.
- Inspect previous commits and navigate through repository history.
- Restore files and discard unwanted changes.
- Remove untracked files safely.
- Understand the different modes of `git reset`.
- Undo previous commits using `git revert`.
- Identify and resolve revert conflicts.
- Inspect repository status using short status format.

## Topics Covered

### 1. Commit Messages and Change Inspection

- Writing meaningful commit messages
- Comparing changes with `git diff`
- Comparing the latest commit with staged changes
- Comparing the latest commit with working directory changes
- Comparing commits and branches

### 2. File Management and Recovery

- Working with `.gitignore`
- Inspecting previous commits using `git checkout`
- Discarding working directory changes
- Restoring files with `git restore`
- Removing untracked files with `git clean`

### 3. Git Reset

- Understanding the three reset modes
- `git reset --soft`
- `git reset --mixed`
- `git reset --hard`

### 4. Git Revert

- Reverting previous commits
- Understanding the difference between reset and revert
- Handling conflicts during revert operations

### 5. Repository Status

- Using `git status`
- Understanding short status output with `git status --short`

## Practical Exercises

The following exercises are designed to reinforce the concepts through hands-on practice.

- [ ] Write meaningful commit messages.
- [ ] Compare working directory and staging area changes.
- [ ] Compare two commits and two branches.
- [ ] Configure and test `.gitignore`.
- [ ] Inspect previous commits.
- [ ] Restore modified and staged files.
- [ ] Safely remove untracked files.
- [ ] Practice all three `git reset` modes.
- [ ] Revert a previous commit.
- [ ] Resolve a revert conflict.
- [ ] Interpret short status output.

## Important Notes

Some Git commands can permanently discard local changes or remove untracked files.

Commands such as `git reset --hard`, `git clean`, and certain restore operations should be used carefully.

All destructive operations should first be practiced in a dedicated test environment.

## Documentation

- [Git Advanced Commands](commands.md)
- [Practical Exercises](exercises.md)
