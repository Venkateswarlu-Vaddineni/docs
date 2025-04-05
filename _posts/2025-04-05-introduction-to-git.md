---
title: "Introduction to git"
categories: 
  - Version-Control-Systems
tags: 
  - Basic of git
  - Introduction
date: 2025-04-05
layout: single
author_profile: false
---
<!-- Shrink code block spacing + Add print button -->
<style>
/* Shrink spacing inside code blocks */
pre, pre code {
  font-size: 13px !important;
  line-height: 1.3 !important;
  padding: 0.5em 0.8em !important;
  border-radius: 6px !important;
  margin-top: 1em !important;
  margin-bottom: 1em !important;
}

/* Inline code style (optional) */
code {
  font-size: 13px !important;
  padding: 0.15em 0.4em;
}

/* Optional: Print button */
#print-btn {
  background: #007acc;
  color: white;
  padding: 6px 12px;
  font-size: 14px;
  text-decoration: none;
  border-radius: 4px;
  display: inline-block;
  margin: 1em 0;
}
</style>

<a id="print-btn" href="#" onclick="window.print()">🖨️ Print This Page</a>


## 🧠 Git Basics – Just What You Must Know

<button onclick="printPost()" class="print-btn">🖨️ Print This Post</button>

Let's walk through Git using a simple real-world scenario:
> Imagine you're writing a small program and want to track your changes efficiently, experiment safely, and roll back when needed. Git helps you do all of that, locally, without any remote server.

### 📌 What is Git?
Git is a **free and open-source distributed version control system**, created by **Linus Torvalds** in 2005 to manage the Linux kernel codebase.
It lets you track changes, collaborate efficiently, and experiment without fear of breaking things.
- **Distributed Version Control System**
- Tracks **changes in code** and enables **collaboration**
- Every developer gets a **full local repo** with history

## ⚙️ First-Time Git Setup
Before using Git, configure your identity and preferred editor (VS Code in our case):

```
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
git config --global core.editor "code --wait"
git config --list
```

This sets your name, email, and editor globally (applies to all repos). The last command confirms the setup.

## 🔧 Basic Git Commands

### 📁 Initialize a Repo
To start a Git repository:
1. First, **create a folder** (or use an existing one) and move into it.
2. Then initialize the Git repository:

```
mkdir myproject
cd myproject
git init
```

This sets up the folder as a Git repository by creating a hidden `.git` directory inside it.

Alternatively, if you're working with a remote project, you may **clone** an existing repo which initializes it automatically:

```
git clone https://example.com/your-repo.git
```

This downloads the project and sets it up with Git tracking immediately.

### ➕ Stage & Commit
Once your code is ready, you need to save a snapshot of it in Git.

```
git add .
git commit -m "Initial commit"
```

- `git add .` stages all new and modified files.
- `git commit` permanently saves the staged snapshot with a message.

### 🔍 Status & Log
Monitor the state of your files and view history.

```
git status
git log
```

- `git status` shows tracked, modified, and untracked files.
- `git log` shows all commits, with author, timestamp, and message.

### 🔀 Branching

#### Why Branches?
Imagine you're developing a new feature, fixing a bug, or testing something experimental. You don’t want to mess up your main codebase, so you create a separate line of development called a **branch**. This way, you can work in isolation and merge it back only when it’s ready.

**Real-World Example**: 
You're building an app. The main branch has the working version. You want to add a "dark mode" feature without affecting the current app. So you create a branch `dark-mode`, build and test there, and merge it when done.

```
git branch
git checkout -b feature-x
git switch main
```

- `git branch` lists all branches.
- `git checkout -b` creates and switches to a new branch.
- `git switch` is the modern way to switch branches.

### ⇂ Merge Changes
After finishing work in another branch, bring changes into your main branch.

```
git merge feature-x
```

This merges the `feature-x` branch into your current branch.

### ⏺ Undo / Revert
Fix mistakes and undo recent work carefully.

```
git restore file.txt
git reset --soft HEAD~1
git reset --hard HEAD~1
```

#### `git restore file.txt`
Use when you made changes to a file but want to discard those changes and return the file to its last committed version.

**Real-World Example**: You changed a config setting and it broke the app. Use restore to undo the changes and go back to the last working version.

#### `git reset --soft HEAD~1`
Moves the HEAD pointer back by one commit but keeps all your changes in the staging area.

**Real-World Example**: You committed with a typo or forgot to include a file. Use this to fix your commit without redoing the work.

#### `git reset --hard HEAD~1`
Moves the HEAD back by one commit and completely removes any changes made — both in staging and working directory.

**Real-World Example**: Your last commit is entirely wrong and you want to erase it and its changes completely.

**⚠️ Important:**
- Once you use `--hard`, the removed commits are lost unless recovered via `git reflog`.
- You can’t move forward again unless you've noted the commit hash before reset.

### ⏲ Navigate to Previous Commits
You can move back to earlier commits using `HEAD~n`, where `n` is how many commits to go back.

```
git reset --hard HEAD~3
```

Alternatively, you can use the commit hash:

```
git reset --hard abc1234
```

To find commit hashes, use `git log`. You only need the first few unique characters.

To explore a past commit without changing the project history:

```
git checkout abc1234
```

This puts you in a detached HEAD state — great for viewing or testing past versions.

**Note**: After a hard reset, if you didn’t note the commit hash, recovery is difficult.

---

{% raw %}
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
{% endraw %}
