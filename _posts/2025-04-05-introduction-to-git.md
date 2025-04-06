---
title: "Introduction to git"
categories: 
  - Version-Control-Systems
tags: 
  - Basic of git
  - git
date: 2025-04-05
layout: single
author: Venkat Vaddineni
author_profile: false
---
## 🧠 Git Basics – Just What You Must Know
<button onclick="printPost()" class="print-btn">🖨️ Print This Post</button>
Let’s walk through Git using a simple real-world scenario:
> Imagine you're writing a small program and want to track your changes efficiently, experiment safely, and roll back when needed. Git helps you do all of that, locally, without any remote server.

---

## 📌 What is Git?

Git is a **free and open-source distributed version control system**, created by **Linus Torvalds** in 2005 to manage the Linux kernel codebase.

### Why It Matters
- It tracks changes to your codebase over time.
- It helps teams collaborate efficiently without overwriting each other's work.
- Every developer has a **complete local copy** of the entire project history.

### Key Concepts
- **Snapshots, not differences**: Git saves a snapshot of the entire project at each commit.
- **Branching and merging**: Work on multiple features or bug fixes in isolation.
- **Local-first**: Make all changes locally and push when you're ready to share.

#### 🧪 Practice:
- Try using a text editor to make a small change in a file and manually save versions with different names.
- Now imagine Git doing that automatically, but much smarter and more efficient.

---

## ⚙️ First-Time Git Setup

Before using Git, you need to configure your personal information and preferred editor (VS Code in this example):

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
git config --global core.editor "code --wait"
git config --list
```

- `user.name` and `user.email` will be attached to every commit you make.
- `core.editor` sets VS Code as your default Git editor.
- `git config --list` confirms your global settings.

#### 🧪 Practice:
- Run the config commands and check with `git config --list`.
- Try changing your name and verify the update.

---

## 🔧 Basic Git Commands

### 📁 Initialize a Repository

Start tracking a folder with Git:

```bash
mkdir myproject
cd myproject
git init
```

This creates a hidden `.git` folder — Git's database for tracking your project. You can now begin version controlling this folder.

#### 🧪 Practice:
- Create a test folder on your machine and initialize it with `git init`.
- Use `ls -a` to view the hidden `.git` folder.

### Clone an Existing Repo

Instead of starting from scratch, clone a remote repository:

```bash
git clone https://example.com/your-repo.git
```

This downloads the project, initializes Git, and sets the remote origin.

#### 🧪 Practice:
- Try cloning any public GitHub repo, like `https://github.com/octocat/Hello-World.git`.

More Examples:
```bash
git clone git@github.com:user/repo.git           # Using SSH
git clone --depth=1 <url>                        # Shallow clone (faster)
git clone --branch dev <url>                     # Clone specific branch
```

---

### ➕ Stage & Commit Changes

One of the key steps in using Git is saving your work in stages. First, you "stage" the files — this tells Git which changes you want to include in the next snapshot (commit). Then you "commit" those staged changes, creating a permanent record in your project’s history.

Think of it like this:
- You’re editing a document (working directory).
- You select what you want to save (staging area).
- Then you save it (commit) to your project history.

```bash
git add .
git commit -m "Initial commit"
```

- `git add .` stages all modified and new files.
- `git commit` records the current snapshot of staged changes.

More Useful Variants:
```bash
git add file.txt                      # Add a single file
git add *.js                          # Add all JS files
git commit -am "Quick update"         # Stage & commit tracked files
git commit --amend                   # Modify the last commit
git reset HEAD file.txt              # Unstage a file
git add -p                           # Interactively stage changes
```

### When to Use Them:
- Use `git add file.txt` to add a specific file instead of everything.
- Use `git commit -am` for a quick save if you're working with tracked files.
- Use `git add -p` when you only want to commit *part* of your changes in a file — great for splitting up work.

#### 🧪 Practice:
- Create a `hello.txt` file, write something, and use `git add` and `git commit` to save it.
- Edit the file again, then use `git add -p` to stage only a portion of your changes.
- Try `git commit --amend` to edit the last commit message or add forgotten files. changes and record them:

```bash
git add .
git commit -m "Initial commit"
```

- `git add .` stages all modified and new files.
- `git commit` records the current snapshot of staged changes.

Other Useful Variants:
```bash
git add file.txt                      # Add a single file
git add *.js                          # Add all JS files
git commit -am "Quick update"         # Stage & commit tracked files
git commit --amend                   # Modify the last commit
git reset HEAD file.txt              # Unstage a file
git add -p                           # Interactively stage changes
```

#### 🧪 Practice:
- Create a `hello.txt` file, write something, and use `git add` and `git commit` to save it.
- Run `git log` to see your commit.

---

### 🔍 Monitor Your Work

Check status and view your commit history:

```bash
git status
git log
```

- `git status`: Shows what’s staged, unstaged, or untracked.
- `git log`: Shows commit history with author, date, and message.

More Examples:
```bash
git log --oneline                    # Condensed history
git log --graph --decorate           # Show branches, tags, merge lines
git diff                            # See unstaged changes
git diff --cached                   # See staged but uncommitted changes
git show <commit>                   # Show details of a specific commit
git log --author="Your Name"        # Filter commits by author
```

#### 🧪 Practice:
- Modify a tracked file and use `git status` to see the change.
- Use `git log` after several commits and note the difference between full and one-line views.

---

### 🔀 Branching

#### Why Use Branches?
Imagine working on a new feature like "dark mode" while your main branch is stable. Branches let you experiment safely.

```bash
git branch                          # List branches
git checkout -b dark-mode           # Create and switch
```

Or with the modern command:

```bash
git switch -c dark-mode
```

Switch back to `main` with:

```bash
git switch main
```

More Commands:
```bash
git branch -d dark-mode             # Delete a branch
git branch -m old-name new-name     # Rename a branch
git switch -                       # Switch to last used branch
git branch --merged                # See branches already merged
git branch --no-merged             # See branches not yet merged
```

#### 🧪 Practice:
- Create a branch called `feature-test`, switch to it, and make a commit.
- Switch back to `main` and confirm your changes aren’t visible there.

---

### ⇂ Merging Changes

After testing in a branch, merge it into the main codebase:

```bash
git checkout main
git merge dark-mode
```

Git will try to automatically merge changes. If there are conflicts, Git will prompt you to resolve them manually.

More Examples:
```bash
git merge --no-ff feature           # Preserve branch history
git merge --squash feature          # Combine all branch commits into one
git merge --abort                   # Cancel a conflicted merge
```

#### 🧪 Practice:
- Edit the same file on both `main` and your feature branch. Merge to observe a conflict.
- Use a code editor or `git status` to resolve the conflict and finish the merge.

---

### ⏺ Undo / Revert

Undoing in Git has layers. Here's how to handle different situations.

#### Discard Local Changes (Unstaged)
```bash
git restore file.txt
```
Reverts `file.txt` to the last committed version.

#### Unstage a File
```bash
git restore --staged file.txt
```
Removes `file.txt` from staging, but keeps your working copy.

#### Soft Reset (Keep Changes Staged)
```bash
git reset --soft HEAD~1
```
Moves back one commit, but keeps your changes staged.

#### Mixed Reset (Unstage Changes)
```bash
git reset --mixed HEAD~1
```
Moves back one commit, keeps changes but unstaged.

#### Hard Reset (Remove Everything)
```bash
git reset --hard HEAD~1
```
Moves back one commit and discards all local changes.

#### Revert a Commit
```bash
git revert <commit-hash>
```
Creates a new commit that undoes the effect of a previous one.

More Useful Examples:
```bash
git checkout -- file.txt             # Legacy way to discard local changes
git clean -fd                        # Remove untracked files & folders
git reflog                           # Recover lost commits
```

#### 🧪 Practice:
- Commit a dummy file. Try `--soft` and `--hard` resets. Observe staged vs. removed content.
- Use `git revert` on an earlier commit and note the new reversal commit.

---

### ⏲ Navigate to Previous Commits

Sometimes you need to explore or revert to an earlier state of your project — for debugging, testing, or recovering lost progress. Git allows you to move through the history of commits with ease.

To **view or test older versions** of your project without affecting current progress, use:
```bash
git checkout abc1234
```
- This puts you in **detached HEAD mode**, meaning you're viewing an old snapshot of your code.
- You can explore, run, and even make changes (though these changes won’t be saved to a branch unless explicitly committed to one).

To **return to your working branch**, simply run:
```bash
git switch main
```

To **rewind your current branch** to a previous state:
```bash
git reset --hard abc1234
```
- This resets the branch to a specific commit and deletes all changes after that commit.

More Examples:
```bash
git checkout HEAD~2          # Go back 2 commits
```
```bash
git reset --soft HEAD~1      # Go back one commit but keep changes staged
```
```bash
git reset --mixed HEAD~3     # Go back 3 commits and keep changes in working directory
```
```bash
git reflog                   # View history of HEAD, useful to recover lost work
```

#### 🧪 Practice:
- Use `git log --oneline` to list recent commits.
- Pick one hash and run `git checkout <hash>` to view that version.
- Try switching back using `git switch main`.
- Experiment with `git reset` variants and note how each behaves with your files and staging.

You can go back in time to explore or test past versions:

```bash
git checkout abc1234
```

- Detached HEAD mode allows inspection without altering history.

Return to latest:
```bash
git switch main
```

Reset back to a specific commit:
```bash
git reset --hard abc1234
```

More Examples:
```bash
git checkout HEAD~2       # Go back 2 commits
git log --oneline         # View commit hashes
git reflog                # See HEAD history for recovery
```

#### 🧪 Practice:
- Use `git log` to find an earlier commit and checkout that commit.
- Return to your latest commit with `git switch main`.

---

## 🧩 Real-World Use Cases

- **New Feature**: Branch off, build, test, and merge.
- **Oops Moment**: Use `git reset`, `restore`, or `revert` to undo.
- **Explore Past**: Use `git log`, `checkout`, and `reflog` to navigate.
- **Track Progress**: `git status`, `diff`, and `log` keep you informed.

---

## ✅ Next Steps

Now that you’re comfortable with Git basics, you’re ready for more advanced workflows like branching strategies, rebasing, cherry-picking, and using tags.

Head over to our next guide: **"Mastering Git: Advanced Concepts"** to level up your Git game!
---
<script>
function printPost() {
  const printContent = document.querySelector('.page__content');
  const original = document.body.innerHTML;
  document.body.innerHTML = `<main>${printContent.innerHTML}</main>`;
  window.print();
  document.body.innerHTML = original;
  location.reload();
}
</script>

<style>
.print-btn {
  float: right;
  margin-top: -20px;
  margin-bottom: 20px;
  background: #f0f0f0;
  border: 1px solid #ccc;
  padding: 5px 10px;
  font-size: 14px;
  cursor: pointer;
  border-radius: 5px;
}

@media print {
  header, footer, nav, aside, .print-btn {
    display: none !important;
  }
  main {
    width: 100%;
    margin: 0 auto;
  }
}
</style>
