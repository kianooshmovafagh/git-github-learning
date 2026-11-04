# Remote Repositories

## Introduction

A remote repository is a Git repository hosted somewhere other than your local machine. GitHub hosts Git repositories and adds collaboration features. Git performs version control; GitHub provides hosting, access control, code review, issues, pull requests, and automation.

**Scope:** This chapter covers lessons 1–12 of the Sabzlearn Git & GitHub course: the GitHub interface, account and repository setup, clone, remote, push, pull, fetch, remote branches, and pull conflicts.

## Learning Objectives

- Explain Git vs. GitHub and local vs. remote repositories.
- Navigate the main areas of a GitHub repository.
- Create a GitHub account and repository.
- Clone an existing repository.
- Connect an existing local project using HTTPS or SSH.
- Inspect and manage remotes.
- Push commits, fetch changes, and pull updates.
- Understand remote-tracking branches and upstream tracking.
- Resolve conflicts during a pull safely.

## 1. Git and GitHub

**Git** is a distributed version control system. It records project history locally and lets developers exchange commits.

**GitHub** is a hosting and collaboration platform built around Git.

Key terms:

- **Local repository:** the repository on your computer, including its commits and branches.
- **Remote repository:** another copy hosted on a server, such as GitHub.
- **Remote name:** a local alias for a remote URL. The conventional name is origin.
- **Push:** sends local commits to a remote.
- **Fetch:** downloads remote objects and updates remote-tracking references.
- **Pull:** fetches and then integrates a remote branch into the current branch.

GitHub does not replace Git. Git handles version control; GitHub hosts repositories and provides collaboration tools.

## 2. Exploring a GitHub Repository

A repository page commonly contains:

- **Code:** files, folders, branches, and the latest commit.
- **Issues:** bug reports, questions, and planned work.
- **Pull requests:** proposed changes and code review.
- **Actions:** automation workflows and CI/CD runs.
- **Projects:** planning boards and task tracking.
- **Wiki, Security, Insights:** documentation, security information, and repository activity, when enabled.
- **README:** the project overview displayed on the repository landing page.
- **Branches and tags:** parallel lines of development and named release points.

The exact tabs depend on repository settings and permissions.

## 3. Account and Authentication Basics

Create an account at [GitHub](https://github.com/). Use an email address you can access, a strong unique password, and enable two-factor authentication (2FA).

Before pushing, confirm that you are signed in to the correct account, have write permission, and have configured an authentication method.

**HTTPS:** GitHub does not accept an account password for Git authentication. Use a supported credential flow such as Git Credential Manager, or a personal access token when required. Never commit a token.

**SSH:** Create a key pair locally, add the public key to your GitHub account, and keep the private key secret.

## 4. Create a Repository on GitHub

On GitHub, choose **New repository**, select an owner, enter a repository name, add an optional description, and choose Public or Private.

You can initialize the repository with a README, .gitignore, or license. If your local project already has commits, avoid creating an unrelated initial history unless you know how you will reconcile it.

After creation, copy the repository URL. Use it to clone the repository or add it as a remote.

## 5. Clone an Existing Repository

Cloning creates a local copy of a remote repository, including its history and remote configuration.

~~~bash
git clone https://github.com/OWNER/REPOSITORY.git
cd REPOSITORY
~~~

With SSH:

~~~bash
git clone git@github.com:OWNER/REPOSITORY.git
~~~

By default, the remote is named origin. Clone is usually the best choice when you are starting work on a repository that already exists on GitHub.

## 6. Connect an Existing Local Project to GitHub

If the project already exists locally and has Git history:

~~~bash
git status
git remote add origin https://github.com/OWNER/REPOSITORY.git
git remote -v
git push -u origin main
~~~

Replace main with your actual local branch name if it differs.

If the local project is not yet a Git repository:

~~~bash
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/OWNER/REPOSITORY.git
git push -u origin main
~~~

If GitHub already contains commits (for example, an automatically created README), your first push may be rejected because the histories differ. Fetch and integrate the remote history deliberately before pushing. Do not force-push as a shortcut.

## 7. Understanding and Managing Remotes

A remote is a named reference to another repository's URL. origin is only a conventional name; it has no special magic.

~~~bash
git remote
git remote -v
git remote show origin
~~~

Add or change a remote:

~~~bash
git remote add origin https://github.com/OWNER/REPOSITORY.git
git remote set-url origin git@github.com:OWNER/REPOSITORY.git
~~~

Rename or remove a remote:

~~~bash
git remote rename origin github
git remote remove github
~~~

Removing a remote removes the local alias and its remote-tracking references; it does not delete the hosted repository.

## 8. Push Local Changes to GitHub

A push transfers commits reachable from your local branch to the remote.

~~~bash
git status
git add .
git commit -m "Add user authentication"
git push origin main
~~~

For the first push of a branch, set its upstream:

~~~bash
git push -u origin feature/login
~~~

After an upstream is configured, you can often use git push without specifying the remote and branch. A push can be rejected when the remote branch contains commits your local branch does not have. Fetch and integrate those commits rather than overwriting them.

## 9. Fetch: Download Without Integrating

git fetch downloads commits and other objects from a remote and updates remote-tracking references such as origin/main. It does **not** merge those changes into your current local branch.

~~~bash
git fetch origin
git branch -r
git log --oneline --graph --decorate --all
git diff main origin/main
~~~

Fetch is useful when you want to inspect incoming changes before deciding how to integrate them.

## 10. Pull: Fetch and Integrate

git pull fetches from the configured remote and integrates the selected remote branch into the current branch. Depending on configuration and options, integration may use a merge or rebase.

~~~bash
git pull
git pull origin main
~~~

Before pulling, check your working tree:

~~~bash
git status
~~~

Commit or safely stash work in progress first. Pull does not always create a merge commit: if the local branch can fast-forward, Git may simply move the branch pointer.

## 11. Remote Branches and Upstream Tracking

A remote-tracking branch is your local record of the last observed state of a branch on a remote. For example, origin/main is not the live remote branch; it is updated by fetch or pull.

~~~bash
git branch
git branch -r
git branch -a
git branch -vv
git switch --track origin/feature/login
git switch -c feature/login --track origin/feature/login
~~~

A local branch can track a remote branch. This relationship makes pull and push simpler because Git knows the default upstream.

To publish a new local branch and configure tracking:

~~~bash
git push -u origin feature/login
~~~

## 12. Pull Conflicts

A pull conflict occurs when Git cannot automatically integrate the fetched changes with the current branch. Common causes include overlapping edits to the same lines or incompatible file operations.

Start by checking the state:

~~~bash
git status
git pull origin main
~~~

If Git reports conflicts:

1. Open each conflicted file.
2. Find conflict markers: <<<<<<<, =======, and >>>>>>>.
3. Decide which changes to keep and edit the file into its intended final form.
4. Remove all conflict markers.
5. Stage each resolved file.
6. Complete the merge if Git is waiting for a merge commit.

~~~bash
git add path/to/resolved-file
git status
git commit
~~~

If the pull used a merge and you want to cancel the in-progress merge:

~~~bash
git merge --abort
~~~

If you explicitly chose a rebase-based pull, use git rebase --abort instead. The abort command depends on the integration operation in progress.

**Important:** Do not blindly choose ours or theirs. Read both versions and preserve the intended behavior. After resolving, run the project's tests and inspect the final diff.

## Recommended Remote Workflow

~~~bash
git status
git switch main
git pull --ff-only
git switch -c feature/my-change
# edit files
git add .
git commit -m "Describe the change"
git push -u origin feature/my-change
~~~

For team projects, feature branches and pull requests are usually safer than committing directly to the default branch.

## Common Mistakes

- Confusing Git with GitHub.
- Assuming origin is a mandatory remote name.
- Pushing without checking the current branch.
- Pulling with uncommitted changes and then struggling to understand the result.
- Thinking fetch changes files in the working directory.
- Thinking origin/main is refreshed in real time.
- Force-pushing to solve a non-fast-forward rejection without understanding the consequences.
- Committing access tokens, passwords, or private keys.
- Resolving conflicts without reviewing the resulting code.

## Chapter Checklist

- [ ] I can explain Git vs. GitHub.
- [ ] I can create a GitHub repository and clone it.
- [ ] I can connect a local project to a remote repository.
- [ ] I can inspect and manage remotes.
- [ ] I can push a branch and set its upstream.
- [ ] I understand the difference between fetch and pull.
- [ ] I can inspect remote-tracking branches.
- [ ] I can resolve a pull conflict and verify the result.

## Related Files

- [Remote Repository Commands](commands.md)
- [Practical Exercises](exercises.md)

## Course Video Mapping

This chapter corresponds to **videos 1–12** in the Sabzlearn course:

1. GitHub introduction and interface
2. Creating a GitHub account
3. git clone
4. Creating a GitHub repository
5. Connecting a project to GitHub
6. git remote
7. git push
8. git pull
9. git fetch
10. Remote branches
11. Understanding GitHub workflow
12. git pull with conflicts

Course: [Sabzlearn – Git & GitHub](https://sabzlearn.ir/course/git-github/)
