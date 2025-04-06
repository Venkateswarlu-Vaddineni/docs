---
title: "Mastering git"
categories: 
  - Version-Control-Systems
tags: 
  - git
  - Advanced git
  - Mastering git
date: 2025-04-05
layout: single
author: Venkat Vaddineni
author_profile: false
---
<button onclick="printPost()" class="print-btn">🖨️ Print This Post</button>
---
## Mastering Git:- Advanced Concepts

## Introduction

In the previous article, we explored Git basics like creating a repository, committing changes, and pushing to a remote. If you're familiar with those steps, you're ready to move forward. This post is a practical journey through advanced Git concepts—presented in a real-world order and explained clearly so even beginners can follow along and start applying them with confidence.

---

## Table of Contents

1. Branching and Merging (Including Merge Strategies)
2. Rebasing for a Clean History
3. Squashing Commits Before a Pull Request
4. Git Tags for Versioning
5. Cherry-Picking Specific Changes
6. Stashing Work in Progress
7. Reflog for Recovery
8. Bisecting to Find Bugs
9. Worktrees for Parallel Work

---

## 1. Branching and Merging (Including Merge Strategies)

> Start here: branching is the foundation of collaboration in Git.

**Branches** are like parallel versions of your project. You use them to develop features or fixes independently from the main line of work (`main` or `master`).

### Create and Switch to a Branch

```bash
git checkout -b feature-login
```

You’re now on a new branch called `feature-login`. Make your changes and commit as usual.

### Merging Back into Main

Once done, switch back to `main` and merge your changes:

```bash
git checkout main
git merge feature-login
```

Now, let’s understand how Git decides *how* to merge:

### Fast-Forward Merge

If no one else updated `main` while you were working, Git just moves the branch pointer. This creates a clean, straight history.

```bash
git merge feature-login
```

You’ll see no extra commit.

### True Merge Commit

If `main` has new commits since you branched off, Git will create a merge commit:

```bash
git merge feature-login
```

This preserves both histories and shows exactly when the feature branch was merged.

### Octopus Merge

Used when merging multiple unrelated branches at once:

```bash
git merge bugfix docs refactor
```

All branches are merged if there are no conflicts. Ideal for housekeeping tasks.

### “Ours” Merge Strategy

When you want to ignore the incoming branch’s changes but still record the merge:

```bash
git merge -s ours legacy-code
```

Useful when deprecating a branch while preserving its history.

---

## 2. Rebasing for a Clean History

Rebasing rewrites the base of your branch so your changes appear as if they were made on top of the latest main branch.

This helps keep history linear and clean.

### How to Rebase

```bash
git checkout feature-login
git rebase main
```

Git replays your commits on top of `main`, one by one.

If a conflict happens:

1. Git will pause and let you fix the conflict.
2. After fixing, stage the changes:

```bash
git add .
```

3. Continue rebasing:

```bash
git rebase --continue
```

After the rebase is complete, you may need to force-push your branch:

```bash
git push --force-with-lease
```

### When to Use It

Use rebase before opening a pull request to avoid unnecessary merge commits and simplify the project history.

---

## 3. Squashing Commits (Clean Up Before Merging)

When you're developing a feature, it's common to make several small commits—some meaningful, others like "fix typo" or "style update." Before merging your branch or creating a pull request, it's a good idea to squash those commits into one or two well-structured commits. This keeps the commit history clean and easier for your team to review.

### How to Squash Commits

Let's say you've made 5 commits. To squash them:

```bash
git rebase -i HEAD~5
```

This opens an interactive editor showing your last 5 commits. You'll see something like:

```
pick a1b2c3 Add login page
pick d4e5f6 Fix layout
pick g7h8i9 Add validation
pick j1k2l3 Fix typo
pick m4n5o6 Update button style
```

Change all but the first `pick` to `squash` (or simply `s`):

```
pick a1b2c3 Add login page
squash d4e5f6 Fix layout
squash g7h8i9 Add validation
squash j1k2l3 Fix typo
squash m4n5o6 Update button style
```

Save and close the editor. Git will prompt you to write a new commit message. You can edit or combine the messages from the squashed commits.

### What to Do Next

Once saved, you’ll have a single commit. Push it using:

```bash
git push --force-with-lease
```

This ensures your remote branch reflects your cleaned-up commit history, making code review easier.

---

## 4. Git Tags for Versioning

Tags are markers you place on specific commits—usually to indicate versions or releases. They make it easy to refer to key milestones in your project.

### Creating a Tag

```bash
git tag v1.0
```

This tags the current commit with `v1.0`. If you want to tag a previous commit:

```bash
git tag v1.0 <commit-hash>
```

### Sharing Tags with Others

Tags aren’t pushed by default. To share them:

```bash
git push origin v1.0
```

Or push all tags:

```bash
git push --tags
```

### When to Use Tags

Use tags for marking release points like `v1.0`, `v2.1-beta`, or `release-2024-01`. They’re useful when deploying or debugging a specific version.

---

## 5. Cherry-Picking Specific Changes

Sometimes, you only want one commit from another branch—not the whole thing. Cherry-picking helps you grab and apply that specific commit wherever needed.

### Real Example

Let’s say your teammate fixed a bug on the `hotfix` branch, and you need that fix in your `release` branch.

```bash
git checkout release
git cherry-pick <commit-hash>
```

This applies the changes from that commit onto your current branch.

### Handling Conflicts

If conflicts arise during the cherry-pick:

```bash
git add .
git cherry-pick --continue
```

After it finishes, test your branch to make sure the cherry-picked change integrates well.

---

## 6. Stashing Work in Progress

You’re mid-task when an urgent bug appears in another branch. But your current work isn’t ready to be committed. Use `git stash` to quickly save your changes and switch branches without losing progress.

### How to Stash

```bash
git stash
```

This stores your uncommitted changes temporarily and resets your working directory.

Now you can switch branches:

```bash
git checkout main
```

### Applying Stashed Work

When you’re ready to resume:

```bash
git stash list
```

Find your stash entry (e.g., `stash@{0}`), then apply it:

```bash
git stash apply stash@{0}
```

If you no longer need it after applying:

```bash
git stash drop stash@{0}
```

Or pop it (apply and remove in one go):

```bash
git stash pop
```

### Custom Named Stash

Give your stash context:

```bash
git stash save "WIP: redesign navbar"
```

This makes it easier to recall why you stashed something.

---

## 7. Reflog for Recovery

Reflog tracks where your Git references (like HEAD or branch pointers) have been—even after operations like `reset` or `rebase`. It helps you recover lost commits that aren’t visible in the regular `git log`.

### View the Reflog

```bash
git reflog
```

You’ll see a list of recent HEAD movements with commit hashes. Example:

```
0f1c2d1 HEAD@{0}: reset: moving to HEAD~1
a2b3c4d HEAD@{1}: commit: Fix navbar alignment
...
```

### Recover a Lost Commit

If you accidentally reset or deleted a branch:

```bash
git checkout -b recovery-branch <commit-hash>
```

Git usually retains reflog entries for 90 days (by default).

---

## 8. Bisecting to Find Bugs

Git Bisect is a tool that uses binary search to help you find the exact commit that introduced a bug. It’s efficient when you have many commits between a known good and bad state.

### Starting Bisect

```bash
git bisect start
git bisect bad       # Current commit has the bug
git bisect good v1.0 # v1.0 was working fine
```

Git now checks out a middle commit. You test your code:

- If the bug is present:

```bash
git bisect bad
```

- If the bug is not present:

```bash
git bisect good
```

Repeat the process. Git will continue narrowing it down.

### End Bisect

Once Git identifies the problematic commit:

```bash
git bisect reset
```

Use this commit’s hash to inspect or revert the change as needed.

---

## 9. Worktrees for Parallel Work

Worktrees let you have multiple working directories from the same Git repo. This is useful when you want to check out different branches at the same time without cloning the repo again.

### Create a New Worktree

```bash
git worktree add ../feature-login feature-login
```

This checks out the `feature-login` branch into a new directory one level above the current one.

### Switch Between Worktrees

Just navigate into each folder and work independently. Changes in one don’t affect the other.

### List All Worktrees

```bash
git worktree list
```

### Remove a Worktree

```bash
git worktree remove ../feature-login
```
---

## Final Thoughts

Git is powerful, but it doesn’t have to be overwhelming. By mastering these commands step-by-step and applying them in real-world scenarios, you’ll grow more confident in managing code and collaborating with others.

Next up, we’ll explore working with remotes: pushing, pulling, managing remotes, and contributing to shared projects.

Stay curious, keep experimenting—and Git better every day!


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

