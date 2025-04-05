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
## 🧠 Git Basics – Just What You Must Know

### 📌 What is Git?
Git is a **free and open-source distributed version control system**, created by **Linus Torvalds** in 2005 to manage the Linux kernel codebase.
It lets you track changes, collaborate efficiently, and experiment without fear of breaking things.
- **Distributed Version Control System**
- Tracks **changes in code** and enables **collaboration**
- Every developer gets a **full local repo** with history

---

### 📂 Git vs GitHub
- **Git** – the tool (installed locally)
- **GitHub** – remote hosting platform for Git repositories

---

## ⚖️ First-Time Git Setup
```
git config --global user.name "Your Name"       # Set your name
git config --global user.email "you@example.com" # Set your email
git config --list                               # Check current config
git config --global core.editor "code --wait"   # Set default editor to VS Code
```

---

## 🔧 Basic Git Commands

### 📁 Initialize a Repo
```
git init          # Create a new Git repo in the current folder
```

### ➕ Stage & Commit
```
git add .         # Add all modified or new files to staging area
git commit -m "Message"   # Create a commit with a short description
```

### 🔍 Status & Log
```
git status        # Show current state of working directory and staging area
git log           # List all past commits with details
```

### 🔀 Branching
```
git branch                    # List branches
git checkout -b feature-x     # Create & switch to new branch
git switch main               # Modern way to switch branches
```

### 🔁 Merge Changes
```
git merge feature-x   # Merge feature-x into current branch
```

### ⏪ Undo / Revert
```
git restore file.txt         # Revert file back to last committed version (undo unsaved changes)
git reset --soft HEAD~1      # Undo last commit, keep all changes staged
```

---
