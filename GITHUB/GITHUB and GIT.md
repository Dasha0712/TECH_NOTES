# Git and GitHub — Complete Guide

---

## 1. What is Git and What is GitHub?

These are two different things that work together. People confuse them all the time.

**Git** is a tool that runs on your laptop. It tracks every change you make to your code over time. Think of it like a save history in a video game — you can go back to any previous save point at any time. Git works completely offline on your computer.

**GitHub** is a website (github.com) where you upload your project so it is stored online. This is how you access your project from another laptop, share it with others, back it up, and collaborate with a team.

**Real life analogy:**
- Git is like your personal diary where you write down every change you made to your project
- GitHub is like a locker where you store that diary online so you can access it from anywhere

So the flow is:
- You write code on your laptop
- Git tracks every change locally
- You push (upload) to GitHub
- From any other laptop you clone or pull (download) it back

---

## 2. Installing and Verifying Git

Download Git from git-scm.com and install it. After installing, open VS Code terminal and verify:

```bash
git --version
```

You should see something like:
```
git version 2.44.0
```

If you see this — Git is installed and in your PATH correctly.

---

## 3. One Time Setup — Tell Git Who You Are

Before using Git for the first time, you need to tell it your name and email. Git will attach this information to every commit you make. Do this only once on each laptop.

```bash
git config --global user.name "Your Name"
git config --global user.email "youremail@gmail.com"
```

> **Important:** Use the same email you used to create your GitHub account.

Verify it worked:
```bash
git config --global --list
```

You should see:
```
user.name=Your Name
user.email=youremail@gmail.com
```

---

## 4. Understanding the 3 States of Git

Every file in your project lives in one of 3 states:

**Untracked / Modified** — you created or changed a file but Git does not know about it yet. Shows in red in `git status`.

**Staged** — you told Git "I want to save this file in the next snapshot". Shows in green in `git status`. You do this with `git add`.

**Committed** — Git has taken a snapshot and saved it permanently in history. You do this with `git commit`.

**Real life analogy:**
- Modified = you wrote something on paper
- Staged = you put that paper in an envelope ready to send
- Committed = you sealed and posted the envelope — it is now saved forever

---

## 5. Starting a New Project — Full Flow

### Step 1 — Initialize Git in your project folder

Make sure you are inside your project folder in the terminal:
```bash
cd D:\your-project-folder
```

Then initialize Git:
```bash
git init
```

You will see:
```
Initialized empty Git repository in D:\your-project-folder\.git\
```

Git created a hidden folder called `.git` inside your project. This is where Git stores all the history. Never delete or edit this folder.

### Step 2 — Check status

```bash
git status
```

All your files will show in red — untracked.

### Step 3 — Stage all files

```bash
git add .
```

The `.` means add everything in the current folder.

### Step 4 — Make your first commit

```bash
git commit -m "first commit"
```

The message inside quotes describes what you did. Make it meaningful.

You will see:
```
[main (root-commit) 3e887ab] first commit
 5 files changed, 100 insertions(+)
```

---

## 6. Creating a Repository on GitHub and Uploading Your Project

### Step 1 — Create repository on GitHub

1. Go to github.com and log in
2. Click the **"+"** icon at top right
3. Click **"New repository"**
4. Give it the same name as your project folder
5. Choose Public or Private
6. **DO NOT tick** "Add a README file", "Add .gitignore", or "Choose a license"

> **Why not tick those?** Because your project already has files locally. If GitHub creates files too, they will conflict when you try to push.

7. Click **"Create repository"**

### Step 2 — Connect local project to GitHub

After creating, GitHub shows you commands. Copy your repository URL and run these one by one:

```bash
git remote add origin https://github.com/yourusername/yourproject.git
```

```bash
git branch -M main
```

```bash
git push -u origin main
```

After the last command it may open a browser asking you to authorize Git with GitHub — click authorize and come back.

You will see:
```
Enumerating objects: 5, done.
Writing objects: 100% (5/5), done.
To https://github.com/yourusername/yourproject.git
 * [new branch]      main -> main
```

Now go to your GitHub page and refresh — your files are there.

> **Note:** `git push -u origin main` is only used the first time. After that just use `git push`.

---

## 7. The Daily Workflow — Making Changes and Pushing

This is what you do every single day when working on a project. Always the same 4 steps:

```
make changes → git add . → git commit -m "message" → git push
```

### Step by step:

**Step 1** — Make changes to your files and save them with `Ctrl + S`

**Step 2** — Check what changed:
```bash
git status
```
Changed files show in red.

**Step 3** — Stage your changes:
```bash
git add .
```

**Step 4** — Commit with a meaningful message:
```bash
git commit -m "describe what you did"
```

**Step 5** — Push to GitHub:
```bash
git push
```

Go to GitHub and refresh — your changes are live.

---

## 8. Downloading a Project From GitHub — git clone

When you want to download a project from GitHub to any laptop:

**Step 1** — Go to your GitHub repository page

**Step 2** — Click the green **"Code"** button

**Step 3** — Copy the URL shown

**Step 4** — In terminal navigate to where you want the project:
```bash
cd D:\
```

**Step 5** — Clone it:
```bash
git clone https://github.com/yourusername/yourproject.git
```

You will see:
```
Cloning into 'yourproject'...
remote: Enumerating objects: 10, done.
Receiving objects: 100% (10/10), done.
```

**Step 6** — Go into the folder and open in VS Code:
```bash
cd yourproject
code .
```

**Step 7** — Verify it is connected to GitHub:
```bash
git remote -v
```

You should see:
```
origin  https://github.com/yourusername/yourproject.git (fetch)
origin  https://github.com/yourusername/yourproject.git (push)
```

fetch = can download, push = can upload. Both should show.

---

## 9. Seeing History and Going Back to Previous Versions

### See all commits

```bash
git log --oneline
```

You will see something like:
```
cf9add1 I added to what to do today       ← latest
586b686 Merge branch main
5afb003 Initialization of uploading project
1b326bb Initial commit                     ← oldest
```

Each line is one commit. The 7 character code on the left is the commit ID.

---

### Option 1 — Just VIEW an old version without changing anything

```bash
git checkout 586b686
```

This lets you see your project exactly as it was at that commit. Your files will change to that old version. To come back to the latest:

```bash
git checkout main
```

---

### Option 2 — Undo last commit but keep your file changes

```bash
git reset HEAD^
```

Removes the last commit but your file changes are still there. Useful when you committed too early or with a wrong message.

---

### Option 3 — Completely go back and delete everything after a commit

```bash
git reset --hard 586b686
```

Replace `586b686` with the commit ID you want to go back to.

> **Warning:** This permanently deletes all changes after that commit. Cannot be undone.

Then push the revert to GitHub:
```bash
git push --force
```

---

## 10. What is a Branch?

A branch is a separate copy of your project where you can work without affecting the main version.

**main branch** is the official clean working version of your project. In companies nobody ever works directly on main.

**feature branch** is a copy you create to work on a specific task. When done you merge it back into main.

**Real life analogy:**
Imagine you have the original copy of an important document. Instead of writing directly on the original, you photocopy it and write on the copy. When you are happy with your changes, you transfer them back to the original. That is a branch.

---

### Why branches are important in companies

Imagine 3 people working on the same project:
- Dasha is adding a login page
- Rahul is fixing a bug in payment
- Sara is updating the home page

If all 3 work directly on main — they will overwrite each other's work and break everything.

So instead:
- Dasha creates branch `feature-login`
- Rahul creates branch `fix-payment-bug`
- Sara creates branch `update-homepage`

Everyone works independently on their own branch. When done, each person merges their branch into main through a Pull Request.

---

## 11. Working With Branches — Commands

### See which branch you are on

```bash
git branch
```

The `*` shows your current branch:
```
* main
```

### Create a new branch and switch to it

```bash
git switch -c feature-login
```

`-c` means create. Name it something descriptive. Common naming in companies:
- `feature-login` — adding a new feature
- `fix-payment-bug` — fixing a bug
- `update-homepage` — updating something existing

### Confirm you switched

```bash
git branch
```

```
  main
* feature-login
```

### Switch between existing branches

```bash
git switch main
git switch feature-login
```

### Push a new branch to GitHub

```bash
git push -u origin feature-login
```

### Delete a branch after merging

```bash
git branch -d feature-login
```

---

## 12. Pull Request — The Most Important Corporate Workflow

A Pull Request (PR) means you are saying to your team:

**"I finished my work on my branch. Please review my code and if it looks good, merge it into main."**

In a company your team lead or senior developer reviews your code before it goes into main. They can approve it, ask for changes, or reject it.

### How to create a Pull Request on GitHub

**Step 1** — Push your branch to GitHub:
```bash
git push -u origin feature-gitnotes
```

**Step 2** — Go to your GitHub repository page and refresh it

**Step 3** — You will see a yellow banner:
```
feature-gitnotes had recent pushes
```
Click the green **"Compare & pull request"** button

**Step 4** — Fill in the form:
- **Title** — what you did: `added git notes file`
- **Description** — explain in detail: `created a new markdown file with basic git commands for reference`
- At the bottom you can see exactly what lines changed — green is added, red is deleted

**Step 5** — Click **"Create pull request"**

Now your PR is open. In a company your team lead gets notified and reviews it.

---

## 13. Merging — Bringing Branch Work Into Main

After a Pull Request is approved, you merge the branch into main.

### Merging on GitHub

**Step 1** — On the Pull Request page click **"Merge pull request"**

**Step 2** — Click **"Confirm merge"**

**Step 3** — You will see:
```
Pull request successfully merged and closed
```

**Step 4** — Click **"Delete branch"** — branch is no longer needed after merging. This is standard in companies.

### Update your local main after merging on GitHub

Your laptop's main does not automatically know about the merge. You need to pull:

```bash
git switch main
git pull
```

Check the log:
```bash
git log --oneline
```

You will see the merge commit at the top and the new files in your project.

Delete local branch too:
```bash
git branch -d feature-gitnotes
```

---

## 14. Conflicts — When Two People Edit the Same Line

A conflict happens when two people edit the exact same line in the same file and Git does not know which version to keep.

### Real corporate example

- Dasha edits line 3 of `index.html` and writes `background: blue`
- Rahul also edits line 3 of the same file and writes `background: red`
- Both push their branches
- When merging — Git says "I don't know which one to keep — you decide"

### What a conflict looks like in your file

When you try to merge and there is a conflict, Git edits your file and adds markers:

```
<<<<<<< HEAD
1. this is from main branch
=======
1. this is from conflict-test branch
>>>>>>> conflict-test
```

`<<<<<<< HEAD` — your current branch version

`=======` — divider between the two versions

`>>>>>>> conflict-test` — the incoming branch version

### How to fix a conflict

You have 3 choices:

**Keep your version (main)** — delete everything except:
```
1. this is from main branch
```

**Keep their version (incoming branch)** — delete everything except:
```
1. this is from conflict-test branch
```

**Keep both** — delete only the conflict markers, keep both lines:
```
1. this is from main branch
1. this is from conflict-test branch
```

VS Code also shows 4 clickable buttons above the conflict:
- **Accept Current Change** — keeps your version
- **Accept Incoming Change** — keeps their version
- **Accept Both Changes** — keeps both
- **Compare Changes** — shows side by side

After resolving, save the file and commit:
```bash
git add .
git commit -m "resolved conflict"
```

### How conflicts are handled in companies

When a conflict happens your team lead will say "pull the latest main and resolve the conflicts in your branch". You sit with your team mate, look at both versions together and decide what the final code should look like. Then commit the resolved version and push.

---

## 15. The Complete Corporate Daily Workflow

This is exactly what happens in every software company every single day:

```
1.  Get assigned a task from team lead
2.  Switch to main and pull latest → git switch main → git pull
3.  Create a new branch → git switch -c feature-name
4.  Do your work — write code, edit files
5.  Check what changed → git status
6.  Stage changes → git add .
7.  Commit with message → git commit -m "what you did"
8.  Push branch to GitHub → git push -u origin feature-name
9.  Go to GitHub and create a Pull Request
10. Team lead reviews your code
11. If changes needed → fix them → git add . → git commit → git push
12. If approved → team lead merges into main
13. Switch back to main → git switch main
14. Pull latest main → git pull
15. Delete old branch → git branch -d feature-name
16. Repeat for next task
```

---

## 16. Common Error — Rejected Push (Fetch First)

You will see this error when someone else pushed to the same branch before you:

```
! [rejected]    main -> main (fetch first)
error: failed to push some refs
hint: Updates were rejected because the remote contains work you do not have locally
```

**Fix:**
```bash
git pull origin main --allow-unrelated-histories
git push
```

This pulls their changes first, merges with yours, then pushes everything together.

---

## 17. Quick Reference — All Commands in One Place

```bash
# ── SETUP ─────────────────────────────────────────
git config --global user.name "Your Name"
git config --global user.email "email@gmail.com"
git config --global --list              # verify setup

# ── STARTING A PROJECT ────────────────────────────
git init                                # start tracking a folder
git status                              # see current state of files

# ── STAGING AND COMMITTING ────────────────────────
git add .                               # stage all changes
git add <file>                          # stage one specific file
git commit -m "message"                 # save a snapshot
git commit -am "message"                # stage and commit in one step

# ── PUSHING AND PULLING ───────────────────────────
git remote add origin <url>             # connect to GitHub
git push -u origin main                 # first time push
git push                                # push after first time
git pull                                # get latest from GitHub
git clone <url>                         # download project from GitHub

# ── HISTORY AND GOING BACK ────────────────────────
git log --oneline                       # see all commits
git checkout <commit-id>                # view old version
git checkout main                       # come back to latest
git reset HEAD^                         # undo last commit keep changes
git reset --hard <commit-id>            # go back and delete everything after
git push --force                        # push after hard reset

# ── BRANCHES ──────────────────────────────────────
git branch                              # see all branches
git switch -c feature-name              # create and switch to new branch
git switch main                         # switch to main branch
git push -u origin feature-name        # push new branch to GitHub
git merge feature-name                  # merge branch into current branch
git branch -d feature-name              # delete branch after merging

# ── CHECKING REMOTE ───────────────────────────────
git remote -v                           # see connected GitHub URL
```

---

## 18. Key Rules to Remember

> **Never work directly on main.** Always create a branch for every task.

> **Always pull before starting new work.** This keeps you up to date with what your team pushed.

> **Commit often with clear messages.** Small frequent commits are better than one big commit.

> **Delete branches after merging.** Keeps the repository clean.

> **Never force push to main in a company.** Only force push on your own personal branches.

---

*Git feels confusing at first but after doing it a few times it becomes muscle memory. The flow is always the same — branch, work, add, commit, push, pull request, merge.*