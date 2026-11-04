# Remote Repositories – Practical Exercises

These exercises turn the concepts in this chapter into repeatable Git workflows. Use a test repository rather than an important production project.

## Exercise 1: Create a GitHub Repository

**Goal:** Create a remote repository and understand its basic settings.

1. Sign in to GitHub.
2. Create a repository named remote-practice.
3. Choose Public or Private intentionally.
4. Copy its HTTPS clone URL.
5. Identify the default branch and the Code, Issues, and Pull requests areas.

**Verify:** You can open the repository page and identify its URL and visibility.

## Exercise 2: Clone the Repository

~~~bash
git clone https://github.com/YOUR-USERNAME/remote-practice.git
cd remote-practice
git remote -v
git status
~~~

**Questions:** Which remote name was configured automatically? Which branch was checked out? What URLs are used for fetch and push?

## Exercise 3: Connect an Existing Local Project

1. Create a separate local folder and initialize Git.
2. Add a README file and create an initial commit.
3. Add your GitHub repository as origin.
4. Push your branch and set its upstream.

~~~bash
git init
echo "# Remote Practice" > README.md
git add README.md
git commit -m "Create practice README"
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/remote-practice.git
git push -u origin main
~~~

If the GitHub repository already has an independent commit, inspect the histories before integrating them. Do not force-push to bypass the problem.

## Exercise 4: Practice Remote Management

~~~bash
git remote -v
git remote rename origin github
git remote -v
git remote set-url github https://github.com/YOUR-USERNAME/remote-practice.git
git remote remove github
~~~

Re-add the remote after the exercise if you want to continue using this local repository.

**Verify:** The hosted repository still exists after removing the local remote alias.

## Exercise 5: Push a New Commit

1. Add a file named notes.md.
2. Commit it.
3. Push the current branch.
4. Refresh GitHub and confirm the file is visible.

~~~bash
echo "Learning remote repositories" > notes.md
git add notes.md
git commit -m "Add remote learning notes"
git push
~~~

## Exercise 6: Fetch Without Pulling

1. Open the same repository on GitHub.
2. Edit a file through the GitHub interface and commit the change.
3. On your computer, run:

~~~bash
git fetch origin
git status -sb
git log --oneline --graph --decorate --all
git diff main origin/main
~~~

4. Inspect the incoming change.
5. Confirm that your current working file has not been updated by fetch alone.

**Verify:** Explain why origin/main moved while your local main did not.

## Exercise 7: Pull Remote Changes

~~~bash
git pull origin main
git status
git log --oneline --graph -5
~~~

**Verify:** The remote change is now present in your local working tree and history.

## Exercise 8: Track a Remote Branch

1. Create a branch named feature/remote-demo on GitHub.
2. Fetch remote references.
3. Create a local tracking branch.

~~~bash
git fetch origin
git branch -r
git switch --track origin/feature/remote-demo
git branch -vv
~~~

**Verify:** git branch -vv shows the upstream branch.

## Exercise 9: Simulate and Resolve a Pull Conflict

1. Ensure your local main is synchronized with GitHub.
2. On local main, edit a line in conflict-demo.txt and commit it.
3. On GitHub, edit the same line differently and commit the remote change.
4. Fetch and inspect the divergence.
5. Pull the remote branch and observe the conflict.
6. Edit the file to produce the intended final content.
7. Stage the resolution and complete the merge.

~~~bash
git switch main
git fetch origin
git log --oneline --graph --all
git pull origin main
git status
# Resolve the file in your editor
git add conflict-demo.txt
git diff --staged
git commit
~~~

If Git says the pull is already up to date, verify that the local and remote edits were made on divergent histories and that you edited the same line.

**Verify:** No conflict markers remain, the final file contains the intended result, the merge commit includes both lines of history, and git status reports a clean working tree.

## Exercise 10: Explain the Workflow

Answer these questions in your own words:

1. What is the difference between Git and GitHub?
2. What does origin represent?
3. What is the difference between git fetch and git pull?
4. Why is origin/main called a remote-tracking branch?
5. What does git push -u configure?
6. Why can a push be rejected as non-fast-forward?
7. When should you use git merge --abort versus git rebase --abort?
8. Why is force-pushing risky on a shared branch?

## Completion Checklist

- [x] Created a GitHub repository.
- [x] Cloned a remote repository.
- [x] Connected an existing local repository.
- [x] Inspected and changed a remote.
- [x] Pushed a local commit.
- [x] Fetched remote changes without integrating them.
- [x] Pulled remote changes.
- [x] Created a local branch that tracks a remote branch.
- [x] Resolved a pull conflict.
- [x] Answered the workflow questions.
