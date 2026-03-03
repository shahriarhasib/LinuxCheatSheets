# 🐙 Git & GitHub — The Complete Beginner's Guide

> **A clear, friendly, and comprehensive introduction to Git, GitHub, GitLab, and Version Control**
> 
> 📁 Part of the [LinuxCheatSheets](https://github.com/shahriarhasib/LinuxCheatSheets) collection

---

## 📚 Table of Contents

- [What is Git?](#-what-is-git)
- [Why is it called "GitHub"?](#-why-is-it-called-github)
- [GitHub vs GitLab](#-github-vs-gitlab)
- [Git vs Gist](#-git-vs-gist)
- [What is a Repository?](#-what-is-a-repository)
- [What is a Branch?](#-what-is-a-branch)
- [Folders, Files & the Working Tree](#-folders-files--the-working-tree)
- [Quick Start](#-quick-start)
- [More Resources](#-more-resources)

---

## 🔧 What is Git?

**Git** is a **distributed version control system (DVCS)** — a tool that tracks every change you make to your files over time.

Think of it like a **"time machine" for your code**:

```
You write code  →  Save a snapshot (commit)  →  Keep building
     ↑                                               |
     └──────── Go back to any snapshot anytime ──────┘
```

### Why do developers use Git?

| Problem Without Git | Solution With Git |
|---------------------|-------------------|
| Accidentally deleted important code | Restore any previous version instantly |
| Working with a team causes file conflicts | Git merges changes intelligently |
| No record of who changed what | Every change is logged with author & timestamp |
| "It worked yesterday…" | Roll back to any working state |
| Fear of breaking things | Work on separate branches safely |

### Key Concepts at a Glance

- 🗂️ **Repository (Repo)** — A project folder tracked by Git
- 📸 **Commit** — A saved snapshot of your changes
- 🌿 **Branch** — A separate line of development
- 🔀 **Merge** — Combining branches together
- ☁️ **Remote** — An online copy of your repo (e.g., on GitHub)

> 💡 Git was created in **2005** by **Linus Torvalds** — the same person who created the Linux kernel — to manage the Linux source code after a licensing dispute with BitKeeper.

---

## 🐙 Why is it called "GitHub"?

The name **GitHub** has two parts:

| Part | Meaning |
|------|---------|
| **Git** | The version control system the platform is built around |
| **Hub** | A central meeting point — like a "hub" in a wheel or network |

So **GitHub = a central hub for Git repositories**.

It was founded in **2008** by Tom Preston-Werner, Chris Wanstrath, PJ Hyett, and Scott Chacon.
In **2018**, Microsoft acquired GitHub for **$7.5 billion**.

> The **Octocat** (GitHub's mascot) is a fictional creature — half octopus, half cat — designed to represent the idea of a flexible, multi-armed collaboration tool.

---

## ⚔️ GitHub vs GitLab

Both are platforms to host Git repositories. Here's how they compare:

| Feature | **GitHub** | **GitLab** |
|---------|-----------|-----------|
| 🌍 Ownership | Microsoft | GitLab Inc. (independent) |
| 🎯 Best For | Open source, community sharing | DevOps, CI/CD pipelines |
| 🔒 Private Repos | Free (unlimited) | Free (unlimited) |
| 🏠 Self-Hosting | ❌ Not available | ✅ GitLab CE (free) |
| 🔁 CI/CD Built-in | GitHub Actions | GitLab CI/CD (more powerful) |
| 📦 Package Registry | GitHub Packages | GitLab Package Registry |
| 🔓 Open Source | Partially | Core is open source |
| 👥 Community Size | Larger (100M+ users) | Smaller but growing |
| 🛠️ Issue Boards | Basic | Advanced (Kanban, Epics) |
| 💰 Enterprise | GitHub Enterprise | GitLab EE |

### When to Choose Which?

```
Choose GitHub if...                 Choose GitLab if...
━━━━━━━━━━━━━━━━━━━━━━━━━━━         ━━━━━━━━━━━━━━━━━━━━━━━━━━━
✔ You want the largest community    ✔ You want all-in-one DevOps
✔ Open source contributions         ✔ You need to self-host
✔ Ease of use matters most          ✔ CI/CD is a priority
✔ Integrations with many tools      ✔ More control over your data
```

---

## 📌 Git vs Gist

These sound similar but serve very different purposes:

| | **Git** | **Gist** |
|-|---------|---------|
| 🧩 What is it? | A version control system | A service by GitHub to share code snippets |
| 📦 Size | Full projects & repositories | Single files or small snippets |
| 🌿 Branching | Full branch support | Limited (it IS a git repo underneath) |
| 🔍 Discoverability | Via GitHub search | Public Gists are searchable |
| 💬 Use Case | Complete software projects | Quick code sharing, notes, scripts |
| 🔒 Privacy | Public or Private repos | Public or Secret Gists |
| 🌐 URL | `github.com/username/repo` | `gist.github.com/username/hash` |

### When to Use Gist

```bash
# Perfect for Gist:
- A single configuration file (.bashrc, .vimrc)
- A quick Python script you want to share
- Code examples for a blog post
- Temporary pastes or notes with syntax highlighting

# Use a full Git repo instead:
- Multi-file projects
- Projects with history & collaboration needs
- Anything you'll actively develop over time
```

---

## 🗂️ What is a Repository?

A **repository** (or "repo") is the **heart of Git** — it's the container for your entire project, including all its files, folders, history, and configuration.

### Anatomy of a Git Repository

```
my-project/              ← Root of your repository
│
├── .git/                ← Hidden folder Git uses internally (DON'T touch this!)
│   ├── config           ← Repo-level Git settings
│   ├── HEAD             ← Points to current branch
│   ├── objects/         ← All commits, files, and data stored here
│   └── refs/            ← Branch and tag pointers
│
├── src/                 ← Your source code
├── docs/                ← Documentation
├── tests/               ← Test files
├── README.md            ← You are here! 👋
└── .gitignore           ← Files Git should ignore
```

### Types of Repositories

| Type | Description | Example |
|------|-------------|---------|
| **Local Repo** | Lives on your computer | `/home/user/my-project` |
| **Remote Repo** | Lives on a server | `github.com/user/my-project` |
| **Bare Repo** | Has no working directory, only Git data | Used on servers |
| **Fork** | Your personal copy of someone else's repo | Used for contributing |
| **Clone** | A local copy of a remote repo | `git clone <url>` |

### The Three States of a File

```
┌─────────────────────────────────────────────────────────┐
│                                                         │
│  Working Directory  →  Staging Area  →  Repository      │
│  (untracked/modified)  (git add)       (git commit)     │
│                                                         │
│  📝 You edit files    📦 You stage    💾 You save a      │
│  here                 changes here   permanent snapshot │
└─────────────────────────────────────────────────────────┘
```

### What's in a Commit?

Every **commit** is a permanent snapshot containing:
- 📸 A snapshot of all tracked files at that moment
- 💬 A commit message describing the change
- 👤 Author name and email
- 🕐 A timestamp
- 🔑 A unique SHA-1 hash (e.g., `a3f5c9d`)
- 🔗 A pointer to the parent commit(s)

---

## 🌿 What is a Branch?

A **branch** is an independent line of development — like a parallel universe for your code.

### Visual Explanation

```
main branch:
──●──●──●──────────────●──●──  (production-ready code)
           \          /
            ●──●──●──           (feature/login branch)
```

- The **main** (or **master**) branch is your primary, stable branch
- You **create a new branch** to develop a feature or fix a bug
- When done, you **merge** it back into main
- The original branch is **never affected** during development

### Why Use Branches?

| Use Case | Branch Name Convention |
|----------|----------------------|
| New feature | `feature/user-authentication` |
| Bug fix | `fix/login-error` |
| Release preparation | `release/v2.0` |
| Urgent production fix | `hotfix/payment-crash` |
| Experimental work | `experiment/new-algorithm` |

### Branch vs Tag

| | **Branch** | **Tag** |
|-|------------|---------|
| 🔄 Moves? | Yes — grows with new commits | No — fixed point in history |
| 📌 Use For | Active development | Marking releases (v1.0, v2.0) |
| Example | `feature/dark-mode` | `v1.0.0`, `v2.3.1` |

---

## 📁 Folders, Files & the Working Tree

### The Working Tree

The **working tree** (or working directory) is simply the folder on your computer where your project lives — the files you actually see and edit.

```
Working Tree                    What Git Sees
════════════                    ════════════
📁 my-project/                  
  📄 index.html      ────────▶  ✅ Tracked (committed before)
  📄 style.css       ────────▶  ✅ Tracked
  📄 notes.txt       ────────▶  ❌ Untracked (never added)
  📄 secret.env      ────────▶  🚫 Ignored (.gitignore)
```

### The .gitignore File

Tell Git which files to **never track**:

```gitignore
# Dependencies
node_modules/
vendor/

# Environment & secrets
.env
*.secret
config/local.php

# OS generated files
.DS_Store
Thumbs.db

# Build output
dist/
build/
*.o
*.log
```

### File Status Lifecycle

```
Untracked  ──git add──▶  Staged  ──git commit──▶  Committed (Unmodified)
                                                         │
                                                    (you edit it)
                                                         │
                                                         ▼
                                                      Modified  ──git add──▶  Staged
```

---

## 🚀 Quick Start

```bash
# 1. Install Git
# Windows: https://git-scm.com/download/win
# Linux:   sudo apt install git

# 2. Set your identity
git config --global user.name "Your Name"
git config --global user.email "you@example.com"

# 3. Create a new project
mkdir my-project && cd my-project
git init

# 4. Create a file and commit it
echo "# Hello World" > README.md
git add README.md
git commit -m "Initial commit"

# 5. Push to GitHub
git remote add origin https://github.com/yourusername/my-project.git
git push -u origin main
```

➡️ **For detailed commands with explanations, see [GitCheatSheet.md](./GitCheatSheet.md)**

---

## 📖 More Resources

| Resource | Link |
|----------|------|
| 📘 Official Git Docs | https://git-scm.com/doc |
| 🎓 GitHub Learning Lab | https://skills.github.com |
| 📗 Pro Git Book (Free) | https://git-scm.com/book |
| 🧪 Interactive Git Tutorial | https://learngitbranching.js.org |
| 🦊 GitLab Docs | https://docs.gitlab.com |

---

<div align="center">

Made with ❤️ by [Shahriar Hasib](https://github.com/shahriarhasib)  
Part of the [LinuxCheatSheets](https://github.com/shahriarhasib/LinuxCheatSheets) collection

⭐ **Star this repo if it helped you!** ⭐

</div>
