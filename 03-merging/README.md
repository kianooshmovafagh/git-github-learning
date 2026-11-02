
# Git Merging

## Introduction

Merging is a Git operation that combines changes from one branch into another. It allows developers to integrate independently developed features or fixes while keeping the project history organized.

## What is Merging?

Merging combines the histories of two branches.

The branch currently checked out is the **target branch**, and the branch passed to `git merge` is the **source branch**.

For example:

```bash
git switch main
git merge feature/login
```

In this example:
- `main` is the target branch.
- `feature/login` is the source branch.

## Why Use Merge?

Merging helps developers to:

- Integrate completed features into the main codebase.
- Combine work developed on separate branches.
- Keep project history organized.
- Work on features independently.
- Resolve conflicting changes before integration.

## Main Concepts

### 1. Source Branch

The source branch contains the changes that we want to integrate into another branch.

Example:

`feature/login`

### 2. Target Branch

The target branch is the branch that receives the changes.

Example:

`main`

### 3. Fast Forward Merge

A Fast Forward Merge happens when the target branch has not received new commits since the source branch was created.

Git simply moves the target branch pointer forward without creating a merge commit.

### 4. Non Fast Forward Merge

A Non Fast Forward Merge creates a separate merge commit to connect the histories of two branches.

### 5. Merge Conflict

A merge conflict happens when Git cannot automatically combine changes from different branches.

Developers must resolve the conflicting changes manually.

## Topics Covered

- [x] Understanding Git Merge
- [x] Fast Forward Merge
- [x] Non Fast Forward Merge
- [x] Merge Conflicts
- [x] Resolving Merge Conflicts
- [x] Merge Best Practices
- [x] Writing Meaningful Commit Messages

## Practical Exercises

- [x] Practice Fast Forward Merge.
- [x] Practice Non Fast Forward Merge.
- [x] Resolve a Merge Conflict.
- [x] Inspect Merge Commit History.
- [x] Write meaningful commit messages.

## Useful Commands

See [commands.md](commands.md) for a detailed list of Git merging commands and examples.
