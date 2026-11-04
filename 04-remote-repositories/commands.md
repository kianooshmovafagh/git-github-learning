# Remote Repository Commands

A practical reference for connecting local Git repositories to GitHub and synchronizing changes.

## 1. Clone a Remote Repository

~~~bash
git clone https://github.com/OWNER/REPOSITORY.git
git clone git@github.com:OWNER/REPOSITORY.git
git clone https://github.com/OWNER/REPOSITORY.git my-folder
~~~

The first command clones using HTTPS, the second uses SSH, and the third clones into a custom local directory.

## 2. Initialize and Connect a Local Project

~~~bash
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/OWNER/REPOSITORY.git
git push -u origin main
~~~

Run git status before staging to understand what will be committed. Replace the URL and branch name with your own values.

## 3. Inspect Remotes

~~~bash
git remote
git remote -v
git remote show origin
~~~

- git remote: lists remote names.
- git remote -v: lists fetch and push URLs.
- git remote show origin: displays remote branches and tracking information.

## 4. Add, Rename, Change, and Remove a Remote

~~~bash
git remote add origin https://github.com/OWNER/REPOSITORY.git
git remote rename origin github
git remote set-url github git@github.com:OWNER/REPOSITORY.git
git remote remove github
~~~

Removing a remote does not delete the repository hosted on GitHub.

## 5. Push Changes

~~~bash
git status
git add .
git commit -m "Add project documentation"
git push origin main
~~~

Publish a new branch and set its upstream:

~~~bash
git switch -c feature/profile
git push -u origin feature/profile
~~~

Once upstream tracking is configured, git push is often enough.

## 6. Fetch Changes

~~~bash
git fetch
git fetch origin
git fetch --all
git fetch --prune origin
~~~

- git fetch: fetches from the configured upstream.
- git fetch origin: fetches from origin.
- git fetch --all: fetches from all configured remotes.
- git fetch --prune origin: also removes stale remote-tracking references that no longer exist on that remote.

Inspect what arrived:

~~~bash
git branch -r
git log --oneline --graph --decorate --all
git diff main origin/main
~~~

## 7. Pull Changes

~~~bash
git pull
git pull origin main
git pull --ff-only
git pull --rebase
~~~

- git pull: fetches and integrates the configured upstream.
- git pull origin main: fetches and integrates remote main into the current branch.
- git pull --ff-only: refuses to create a merge commit; succeeds only when fast-forward is possible.
- git pull --rebase: replays local commits on top of the fetched upstream instead of creating a merge commit.

Choose merge or rebase intentionally and follow the project's conventions.

## 8. Remote Branches and Tracking

~~~bash
git branch
git branch -r
git branch -a
git branch -vv
git switch --track origin/feature/search
git switch -c feature/search --track origin/feature/search
git push -u origin feature/search
~~~

- git branch: lists local branches.
- git branch -r: lists remote-tracking branches.
- git branch -a: lists local and remote-tracking branches.
- git branch -vv: shows upstream tracking information.
- git switch --track: creates a local branch that tracks the specified remote-tracking branch.

## 9. Inspect Ahead/Behind State

~~~bash
git status -sb
git branch -vv
git log --oneline main..origin/main
git log --oneline origin/main..main
~~~

- main..origin/main: commits on origin/main but not local main.
- origin/main..main: commits on local main but not origin/main.

Fetch first so the remote-tracking reference is up to date.

## 10. Resolve a Pull/Merge Conflict

~~~bash
git status
# Edit conflicted files and remove conflict markers
git add path/to/file
git status
git commit
~~~

For a merge in progress, cancel it with:

~~~bash
git merge --abort
~~~

For a rebase in progress, cancel it with:

~~~bash
git rebase --abort
~~~

After resolving:

~~~bash
git diff --check
git diff --staged
# Run project tests, then complete the operation
~~~

## 11. Authentication Checks

For SSH, test the connection:

~~~bash
ssh -T git@github.com
~~~

To inspect which URL Git will use:

~~~bash
git remote -v
~~~

Do not share private keys or access tokens. For HTTPS, use Git Credential Manager or GitHub's supported authentication flow rather than an account password.

## 12. Useful Diagnostic Commands

~~~bash
git status
git remote -v
git branch -avv
git log --oneline --graph --decorate --all
git diff
git diff --staged
git ls-remote origin
~~~

git ls-remote origin lists references advertised by the remote without updating local remote-tracking branches.

## Quick Comparison: Fetch vs. Pull

| Command | Downloads remote commits | Integrates into current branch | Changes working files |
| --- | --- | --- | --- |
| git fetch | Yes | No | No |
| git pull | Yes | Yes | May do so |
