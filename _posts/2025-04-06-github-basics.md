---
title: "GitHub Basics"
categories: 
  - Version-Control-Systems
tags: 
  - Basic of GitHub
  - Introduction
date: 2025-04-06
layout: single
author_profile: false
---
## 🌍 Git vs GitHub: A Practical Overview for DevOps
<button onclick="printPost()" class="print-btn">🖨️ Print This Post</button>
### What is Git?
Git is a **distributed version control system**. It tracks code changes locally, lets you branch, experiment, and roll back — all on your machine. It’s a core tool for managing changes in any codebase.

### What is GitHub?
**GitHub** is a **cloud-based hosting service** for Git repositories. It provides a place to store your code online, collaborate with others, and integrate with CI/CD pipelines and tools.

- Secure, remote backup of your Git repos
- Shared platform for collaboration across teams
- Extra features like issues, pull requests, GitHub Actions

### How Git and GitHub Work Together
You manage your changes with Git on your local machine. GitHub acts as a central place where all team members can push their changes, review code, and automate deployments. It connects version control with collaboration and automation.

### DevOps Relevance
In DevOps, GitHub becomes a foundational piece:
- A single source of truth for configuration, scripts, IaC, etc.
- Integrated workflows for testing, building, and deploying code
- Supports audit, rollback, and collaboration among developers and ops teams

### 🛠 Real-World Scenario
Imagine you're a DevOps engineer managing cloud infrastructure using Terraform and scripts. Your team pushes updates to GitHub, triggering GitHub Actions to test and deploy infrastructure automatically. Git manages local changes. GitHub ensures the team works in sync and automates the delivery pipeline.

---

## 🚀 GitHub Basics for DevOps Engineers

### 1. 👤 Creating Your GitHub Account
To interact with GitHub — from viewing code to running automation — you need an account.

Steps:
1. Visit [https://github.com](https://github.com)
2. Sign up with your email and create a username
3. Select a plan (free works fine initially)

Once done, you're ready to create and manage repositories.

---

### 2. 📦 Creating Your First GitHub Repository
A repository (repo) is like a project folder on GitHub where all your tracked files live — code, scripts, documentation.

Steps:
1. Click the **+** at the top right > **New repository**
2. Name it, e.g., `infra-deployment`
3. Choose visibility (Private for team projects, Public for open-source)
4. Add README and .gitignore (optional)
5. Click **Create repository**

Use a new repo for each automation or configuration module.

---

### 3. 🔗 Connecting Local Git to GitHub Repo
After you create a GitHub repo, you’ll want to connect your local Git repo to it. This enables you to sync changes between your computer and GitHub.

```bash
git remote add origin https://github.com/youruser/infra-deployment.git
git branch -M main
git push -u origin main
```

This adds a link between your local and remote repositories and uploads your current code.

---

### 4. 📤 Pushing & 📥 Pulling Code
To keep your local repo and GitHub in sync, you push your committed changes to GitHub, and pull new updates made by your team.

```bash
# Upload your latest work
git push origin main

# Sync with the latest team updates
git pull origin main
```

Additional examples:
```bash
# Push a specific branch
git push origin feature-branch

# Pull updates from another branch
git pull origin staging
```

This way, your work stays up-to-date and integrated with the team’s progress. Always pull before starting new work to avoid conflicts, and push after your changes are tested locally.

---

### 5. 👥 ### 5. 👥 Collaborators and Access Control

When working on infrastructure projects or deployment pipelines, it's common for DevOps teams to work together or grant controlled access to external tools. GitHub provides an easy and secure way to manage permissions within a repository.

To add collaborators:
1. Navigate to your repository on GitHub.
2. Go to **Settings** > **Collaborators**.
3. Enter the GitHub username or email of the person to invite.
4. Assign a role: `Read`, `Triage`, `Write`, `Maintain`, or `Admin`.

Each permission level determines what actions the collaborator can take. For example:
- `Read`: View-only access, useful for monitoring or read-based automation tools.
- `Write`: Allows pushing commits, ideal for developers or engineers working directly on scripts or manifests.
- `Admin`: Full control, suitable for lead engineers or DevOps managers.

**Example Use Case**:
You’re managing a GitHub repo that contains Terraform scripts. You grant `Write` access to your teammates so they can update configurations. You also give your CI/CD service account `Read` access so it can pull the latest code and deploy.

This fine-grained control ensures security and collaboration while avoiding risks like accidental overwrites or unauthorized changes.
You can add team members to a repository without sharing passwords or SSH keys.

Steps:
1. Go to your repo > **Settings** > **Collaborators**
2. Add a GitHub username
3. Choose access level (Read / Write / Admin)

In a DevOps setup, use this to give developers push access, or grant read-only access to CI tools.

---

### 6. 📂 Forking and Cloning

#### Forking
Forking creates a personal copy of someone else’s repo under your account. Ideal for testing or contributing to projects without affecting the original.

Click **Fork** on any public repo to make your own editable version.

Use it when working on shared automation scripts maintained by other teams — fork, test changes independently, and merge if needed.

#### Cloning
Cloning copies a GitHub repo to your local machine. Use this to begin working with any repo locally.

```bash
git clone https://github.com/youruser/infra-deployment.git
cd infra-deployment
```

This helps when starting with a new IaC module or CI/CD pipeline code — get the latest version and begin tweaking for your environment.

---

### 7. 📝 README & .gitignore

#### README
A `README.md` file helps other users (and future you) understand the purpose of the repository.

Example:
```md
# Infra Deployment Repo
This repo contains Terraform modules and scripts used to deploy staging infrastructure.
```

Keep it clear and concise: mention tools, structure, and how to use it.

#### .gitignore
`.gitignore` tells Git which files or directories to ignore. This keeps your repo clean and avoids committing temporary or sensitive files.

Example:
```bash
*.log
.env
__pycache__/
dist/
*.tfstate
```

This is critical in DevOps to avoid leaking credentials, binaries, or temporary artifacts.
---
✅ With these basics, you're set to collaborate, share, and automate using GitHub.

Next, we’ll cover **GitHub Advanced Concepts** like Issues, Pull Requests, GitHub Actions, Environments, and more!
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

