# 🧰 Git Cheat Sheet — Complete Command Reference

> **A full, step-by-step Git guide from installation to advanced workflows**  
> 📁 Part of the [LinuxCheatSheets](https://github.com/shahriarhasib/LinuxCheatSheets) collection

---

## 📚 Table of Contents

1. [Installing Git on Windows 11](#1--installing-git-on-windows-11)
2. [Installing Git on Linux](#2--installing-git-on-linux)
3. [First-Time Git Configuration](#3--first-time-git-configuration)
4. [Create a New Git Repository](#4--create-a-new-git-repository)
5. [Create a New Folder Under a Repo](#5--create-a-new-folder-under-a-repo)
6. [Create a New Branch](#6--create-a-new-branch)
7. [Add, Commit, Push & Pull](#7--add-commit-push--pull)
8. [Working Across Branches and Folders](#8--working-across-branches-and-folders)
9. [Cloning a Repository](#9--cloning-a-repository)
10. [Syncing & Updating Your Repo](#10--syncing--updating-your-repo)
11. [Merging & Resolving Conflicts](#11--merging--resolving-conflicts)
12. [Undoing Mistakes](#12--undoing-mistakes)
13. [Viewing History & Status](#13--viewing-history--status)
14. [Tags & Releases](#14--tags--releases)
15. [Tips, Tricks & Aliases](#15--tips-tricks--aliases)
16. [Git Workflows](#16--git-workflows)
17. [Quick Reference Card](#17--quick-reference-card)

---

## 1. 🪟 Installing Git on Windows 11

### Method 1: Official Git Installer (Recommended)

**Step 1 — Download the Installer**

1. Visit: **https://git-scm.com/download/win**
2. It auto-detects Windows and offers the 64-bit installer
3. Click **"Click here to download"** — the download starts automatically

**Step 2 — Run the Installer**

Follow the wizard. Here are the important screens:

```
📌 Screen: "Select Components"
   ✅ Git Bash Here           (right-click menu in folders)
   ✅ Git GUI Here            (optional graphical tool)
   ✅ Associate .git* files   (recommended)

📌 Screen: "Choosing the default editor"
   → Choose: Notepad, VS Code, or Vim (Vim is default, harder for beginners)
   → Recommended: Visual Studio Code (if installed)

📌 Screen: "Adjusting your PATH environment"
   → Choose: "Git from the command line and also from 3rd-party software"
   (This lets you use 'git' in CMD, PowerShell, and Git Bash)

📌 Screen: "Choosing HTTPS transport backend"
   → Choose: "Use the OpenSSL library"

📌 Screen: "Configuring line ending conversions"
   → Choose: "Checkout Windows-style, commit Unix-style line endings"
   (This prevents line-ending issues when collaborating across OS)

📌 Screen: "Configuring the terminal emulator"
   → Choose: "Use MinTTY (default terminal of MSYS2)"
```

**Step 3 — Verify Installation**

Open **Git Bash** (right-click on Desktop → "Git Bash Here") or **PowerShell** and run:

```bash
git --version
# Output: git version 2.x.x.windows.x
```

---

### Method 2: Using winget (Windows Package Manager)

```powershell
# Open PowerShell as Administrator and run:
winget install --id Git.Git -e --source winget

# Verify
git --version
```

---

### Method 3: Using Chocolatey

```powershell
# If you have Chocolatey installed:
choco install git

# Verify
git --version
```

---

### Setting Up Git Bash on Windows

Git Bash gives you a Linux-like terminal on Windows:

```bash
# Open Git Bash and configure it (see Section 3 for full config)
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

> 💡 **Tip:** Pin Git Bash to your taskbar — you'll use it constantly!

---

## 2. 🐧 Installing Git on Linux

### On Debian / Ubuntu / Linux Mint

```bash
# Step 1: Update package list
sudo apt update

# Step 2: Install Git
sudo apt install git -y

# Step 3: Verify installation
git --version
# Output: git version 2.x.x
```

**Install Latest Version via PPA (Optional)**

The default apt repo may have an older version. For the latest:

```bash
# Add the official Git PPA
sudo add-apt-repository ppa:git-core/ppa
sudo apt update
sudo apt install git -y

# Verify
git --version
```

---

### On CentOS / RHEL / Fedora

**Fedora (modern):**
```bash
# Fedora uses dnf
sudo dnf install git -y

# Verify
git --version
```

**CentOS 7 / RHEL 7:**
```bash
# Uses older yum package manager
sudo yum install git -y

# Verify
git --version
```

**CentOS 8 / RHEL 8:**
```bash
# CentOS 8 uses dnf
sudo dnf install git -y

# Verify
git --version
```

**Install Latest Git from Source on CentOS (Optional)**

```bash
# Install build dependencies
sudo yum groupinstall "Development Tools" -y
sudo yum install gettext-devel openssl-devel perl-CPAN perl-devel zlib-devel -y

# Download and compile
wget https://github.com/git/git/archive/refs/tags/v2.43.0.tar.gz
tar -xzf v2.43.0.tar.gz
cd git-2.43.0
make configure
./configure --prefix=/usr/local
make install

git --version
```

---

### On All Linux Distros (via Snap)

```bash
sudo snap install git --classic
git --version
```

---

## 3. ⚙️ First-Time Git Configuration

Before using Git, you must tell it who you are. These settings are stored globally and attached to every commit you make.

### Essential Configuration

```bash
# Set your name (appears in commit history)
git config --global user.name "Shahriar Hasib"

# Set your email (must match your GitHub/GitLab account for contributions)
git config --global user.email "shahriar@example.com"

# Set your default code editor
git config --global core.editor "code --wait"    # VS Code
git config --global core.editor "nano"           # Nano (easy)
git config --global core.editor "vim"            # Vim (powerful)
git config --global core.editor "notepad"        # Windows Notepad
```

### Configure Default Branch Name

```bash
# GitHub uses 'main' by default (old default was 'master')
git config --global init.defaultBranch main
```

### Configure Line Endings

```bash
# Windows users (converts LF→CRLF on checkout, CRLF→LF on commit)
git config --global core.autocrlf true

# Linux/macOS users (only converts CRLF→LF on commit)
git config --global core.autocrlf input
```

### Configure Colors (Makes output easier to read)

```bash
git config --global color.ui auto
```

### View Your Configuration

```bash
# See all settings
git config --list

# See where settings are stored
git config --list --show-origin

# Check a specific setting
git config user.name
git config user.email
```

### Configuration File Locations

| Scope | File Location | Applies To |
|-------|---------------|-----------|
| `--system` | `/etc/gitconfig` | All users on the machine |
| `--global` | `~/.gitconfig` or `~/.config/git/config` | Your user account only |
| `--local` | `.git/config` inside repo | This repo only |

> 💡 **Local settings override global, which override system.**

### Set Up SSH Key (Recommended for GitHub/GitLab)

Using SSH avoids typing your password every time you push:

```bash
# Step 1: Generate SSH key pair
ssh-keygen -t ed25519 -C "your.email@example.com"
# Press Enter for all prompts (or set a passphrase for extra security)

# Step 2: Start SSH agent and add your key
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519

# Step 3: Copy your public key
cat ~/.ssh/id_ed25519.pub
# Copy the entire output

# Step 4: Add to GitHub
# GitHub → Settings → SSH and GPG keys → New SSH key → Paste key

# Step 5: Test connection
ssh -T git@github.com
# Should say: "Hi username! You've successfully authenticated..."
```

---

## 4. 📦 Create a New Git Repository

### Option A: Start From Scratch (Local)

```bash
# Step 1: Create a new folder
mkdir my-awesome-project
cd my-awesome-project

# Step 2: Initialize Git
git init
# Output: Initialized empty Git repository in .../my-awesome-project/.git/

# Step 3: Create your first file
echo "# My Awesome Project" > README.md
echo "node_modules/" > .gitignore

# Step 4: Stage all files
git add .

# Step 5: Make your first commit
git commit -m "Initial commit: add README and .gitignore"

# Step 6: Connect to GitHub remote
git remote add origin https://github.com/yourusername/my-awesome-project.git

# Step 7: Push to GitHub
git branch -M main        # Rename branch to 'main' if needed
git push -u origin main   # -u sets upstream tracking
```

### Option B: Start From GitHub (Clone Existing)

```bash
# Clone an existing repo from GitHub
git clone https://github.com/yourusername/my-awesome-project.git

# Clone into a specific folder name
git clone https://github.com/yourusername/my-awesome-project.git custom-folder-name

# Clone via SSH (if SSH key is set up)
git clone git@github.com:yourusername/my-awesome-project.git

# Navigate into it
cd my-awesome-project
```

### Understanding `git init` vs `git clone`

| | `git init` | `git clone` |
|-|------------|-------------|
| Use When | Starting a brand new project | Getting a copy of an existing project |
| Remote Set Up | You add it manually with `git remote add` | Automatically set as `origin` |
| Files | Empty (you create them) | All files from the remote included |

---

## 5. 📂 Create a New Folder Under a Repo

> ⚠️ **Important:** Git does NOT track empty folders. You must put at least one file inside.

```bash
# Step 1: Navigate to your repo
cd my-awesome-project

# Step 2: Create a new folder
mkdir src
mkdir docs
mkdir tests

# Step 3: Git ignores empty folders, so add a placeholder file
touch src/.gitkeep       # Convention for keeping empty folders
# OR create a real file:
echo "# Source Code" > src/README.md

# Step 4: Stage and commit
git add src/
git commit -m "Add src folder with README"
```

### Creating Nested Folder Structures

```bash
# Create multiple levels at once
mkdir -p src/components/ui
mkdir -p src/utils
mkdir -p tests/unit/components

# Add files
touch src/components/ui/Button.jsx
touch src/utils/helpers.js
touch tests/unit/components/Button.test.js

# Stage everything new
git add .
git commit -m "Set up project folder structure"
```

### Renaming or Moving Folders

```bash
# Move/rename a folder (Git tracks this as a rename)
git mv old-folder-name new-folder-name
git commit -m "Rename old-folder-name to new-folder-name"

# Move a file to a different folder
git mv src/oldfile.js src/utils/oldfile.js
git commit -m "Move oldfile.js into utils folder"
```

---

## 6. 🌿 Create a New Branch

Branches let you work on features independently without affecting the main codebase.

### Creating and Switching Branches

```bash
# See all existing branches
git branch

# See all branches including remote ones
git branch -a

# Create a new branch (but stay on current branch)
git branch feature/user-login

# Switch to that branch
git checkout feature/user-login

# ✅ Better: Create AND switch in one command
git checkout -b feature/user-login

# Modern Git (2.23+) uses 'switch' instead of 'checkout'
git switch -c feature/user-login     # Create and switch
git switch main                      # Switch to existing branch
```

### Branch from a Specific Commit or Tag

```bash
# Create branch from a specific commit hash
git checkout -b hotfix/bug-123 a3f5c9d

# Create branch from a tag
git checkout -b release/v2.0 v2.0-tag

# Create branch from a remote branch
git checkout -b local-branch origin/remote-branch
```

### Publishing a Branch to GitHub

```bash
# Push new branch to GitHub and set up tracking
git push -u origin feature/user-login

# After this, just use:
git push     # No need to specify remote/branch
```

### Deleting Branches

```bash
# Delete a local branch (safe — prevents deleting unmerged)
git branch -d feature/user-login

# Force delete (even if unmerged)
git branch -D feature/user-login

# Delete a remote branch on GitHub
git push origin --delete feature/user-login

# Clean up stale remote-tracking references
git remote prune origin
```

---

## 7. ➕ Add, Commit, Push & Pull

This is the **core daily workflow** of Git.

### The Full Workflow

```
Edit Files  →  git add  →  git commit  →  git push
                ↑                             ↓
           Staging Area                  GitHub/GitLab
                                              ↓
                                          git pull
                                              ↓
                                     Your Local Repo
```

---

### `git add` — Stage Changes

```bash
# Stage a specific file
git add README.md

# Stage multiple files
git add index.html style.css app.js

# Stage all changes in current directory (and subdirectories)
git add .

# Stage all tracked files that have been modified (not new untracked files)
git add -u

# Stage ALL changes (new, modified, deleted)
git add -A

# Interactively choose what to stage (patch mode — very useful!)
git add -p
# Then: y=yes, n=no, s=split chunk, q=quit, ?=help
```

---

### `git commit` — Save a Snapshot

```bash
# Commit with a message
git commit -m "Add user login feature"

# Stage and commit tracked files in one step (skips staging for NEW files)
git commit -am "Fix typo in README"

# Open editor to write a longer commit message
git commit

# Amend the last commit (change message or add forgotten files)
git add forgotten-file.js
git commit --amend -m "Add user login feature and config file"
# ⚠️ WARNING: Only amend commits that haven't been pushed yet!
```

### Writing Good Commit Messages

```
✅ Good commit messages:
   feat: add user authentication with JWT
   fix: resolve null pointer in payment module
   docs: update README installation steps
   style: format code with Prettier
   refactor: extract helper functions to utils/
   test: add unit tests for login component

❌ Bad commit messages:
   "fixed stuff"
   "asdf"
   "changes"
   "wip"
```

> 💡 Follow the **Conventional Commits** standard: `type(scope): description`

---

### `git push` — Upload to Remote

```bash
# Push current branch to its tracked remote
git push

# Push a specific branch to origin
git push origin feature/user-login

# Push and set upstream tracking (first push of new branch)
git push -u origin feature/user-login

# Force push (DANGEROUS — only use on your own feature branches!)
git push --force
# Safer version of force push:
git push --force-with-lease

# Push all local branches
git push --all origin

# Push tags to remote
git push origin --tags
```

---

### `git pull` — Download & Merge from Remote

```bash
# Pull latest changes from tracked remote branch
git pull

# Pull from specific remote and branch
git pull origin main

# Pull using rebase instead of merge (cleaner history)
git pull --rebase origin main

# Fetch without merging (just download, don't apply yet)
git fetch origin
git fetch --all   # Fetch from all remotes
```

### `git pull` vs `git fetch`

| Command | What it does |
|---------|-------------|
| `git fetch` | Downloads changes from remote, but doesn't apply them |
| `git pull` | Downloads changes AND merges them into your current branch |
| `git pull --rebase` | Downloads changes AND replays your commits on top |

```bash
# Fetch then inspect, then merge manually
git fetch origin
git log HEAD..origin/main --oneline   # See what's new on remote
git merge origin/main                 # Then apply
```

---

## 8. 🔀 Working Across Branches and Folders

### Working Under a Different Branch

```bash
# Scenario: You're on 'main' but need to work on 'feature/dashboard'

# Step 1: Make sure your current work is committed or stashed
git stash               # Temporarily save uncommitted changes
git status              # Check nothing is left staged

# Step 2: Switch to the target branch
git checkout feature/dashboard
# or:
git switch feature/dashboard

# Step 3: Do your work
echo "Dashboard content" > src/dashboard.html
git add src/dashboard.html
git commit -m "Add dashboard page"

# Step 4: Push that branch
git push origin feature/dashboard

# Step 5: Return to main
git checkout main
git stash pop           # Restore your previously stashed changes (if any)
```

### Working in a Specific Folder on a Branch

```bash
# Navigate to the folder within your branch
cd src/components

# Create files, edit, etc.
touch NewButton.jsx
echo "export default function NewButton() {}" > NewButton.jsx

# Come back to repo root to commit
cd ../..

# Stage only files in a specific subfolder
git add src/components/

# Or stage a specific file by path
git add src/components/NewButton.jsx

# Commit
git commit -m "Add NewButton component to src/components"
```

### Stashing — Save Work Without Committing

```bash
# Save your uncommitted work temporarily
git stash
# or with a name:
git stash push -m "half-done login form"

# See all stashes
git stash list
# Output: stash@{0}: half-done login form
#         stash@{1}: On main: WIP on navbar

# Restore the most recent stash
git stash pop

# Restore a specific stash (keep it in stash list)
git stash apply stash@{1}

# Delete a stash
git stash drop stash@{0}

# Clear all stashes
git stash clear
```

---

## 9. 📥 Cloning a Repository

### Basic Clone

```bash
# Clone via HTTPS
git clone https://github.com/shahriarhasib/LinuxCheatSheets.git

# Clone via SSH (faster, no password needed)
git clone git@github.com:shahriarhasib/LinuxCheatSheets.git

# Clone into a specific local folder name
git clone https://github.com/shahriarhasib/LinuxCheatSheets.git my-cheatsheets
```

### Clone a Specific Branch

```bash
# Clone only a specific branch
git clone -b feature/dark-mode https://github.com/user/repo.git

# Clone with limited depth (faster for large repos)
git clone --depth 1 https://github.com/user/repo.git
```

### After Cloning — Common Next Steps

```bash
cd LinuxCheatSheets

# See which branch you're on
git branch

# See all available remote branches
git branch -r

# Check out a remote branch locally
git checkout -b feature/dark-mode origin/feature/dark-mode
# or simply:
git switch feature/dark-mode
```

---

## 10. 🔄 Syncing & Updating After Changes

### Full Sync Workflow (Daily Routine)

```bash
# Morning routine — start fresh:
git checkout main
git pull origin main

# Work on your feature branch
git checkout feature/my-task

# Merge latest main into your feature branch to stay up to date
git merge main
# or use rebase for cleaner history:
git rebase main

# Commit your new work
git add .
git commit -m "Complete task XYZ"

# Push your work
git push origin feature/my-task
```

### Handling "Your branch is behind"

```bash
# Git says: "Your branch is behind 'origin/main' by 3 commits"
git pull origin main          # Simple merge pull
git pull --rebase origin main # Or rebase (no merge commit created)
```

### Handling "Diverged branches"

When both your local and remote have new commits:

```bash
git pull --rebase origin main
# Git will:
# 1. Fetch remote changes
# 2. Put your commits on top of remote changes
# Result: Linear history without a merge commit
```

---

## 11. 🔀 Merging & Resolving Conflicts

### Merging a Branch

```bash
# Step 1: Switch to the branch you want to merge INTO
git checkout main

# Step 2: Merge your feature branch
git merge feature/user-login

# Fast-forward merge (no merge commit if possible)
git merge --ff-only feature/simple-fix

# Always create a merge commit (preserves branch history)
git merge --no-ff feature/user-login -m "Merge feature/user-login into main"
```

### Resolving Merge Conflicts

When Git can't automatically merge:

```bash
# Step 1: See which files have conflicts
git status
# Output: both modified: src/app.js

# Step 2: Open the conflicted file — it looks like:
```

```
<<<<<<< HEAD (your changes)
const greeting = "Hello World";
=======
const greeting = "Hi there!";
>>>>>>> feature/user-login (incoming changes)
```

```bash
# Step 3: Edit the file — choose one, or combine:
const greeting = "Hello World";   # Delete the conflict markers
# Remove <<<<<<, =======, and >>>>>>> lines

# Step 4: Stage the resolved file
git add src/app.js

# Step 5: Complete the merge
git commit -m "Merge feature/user-login: resolve greeting conflict"

# To ABORT a merge mid-conflict (go back to before)
git merge --abort
```

### Using a Merge Tool

```bash
# Configure a visual merge tool
git config --global merge.tool vscode

# Launch the merge tool on conflicts
git mergetool
```

---

## 12. ↩️ Undoing Mistakes

### Undo Staged Changes (before commit)

```bash
# Unstage a file (keep changes in working directory)
git restore --staged README.md
# Old way: git reset HEAD README.md

# Unstage all files
git restore --staged .
```

### Undo Working Directory Changes

```bash
# Discard changes to a file (revert to last commit)
git restore README.md
# ⚠️ This permanently discards your changes!

# Discard all changes in working directory
git restore .
```

### Undo a Commit (Safe — keeps history)

```bash
# Create a new commit that reverses a previous one
git revert a3f5c9d      # Revert by commit hash
git revert HEAD         # Revert the most recent commit
```

### Undo Commits with Reset

```bash
# Soft reset — undo commit but keep changes staged
git reset --soft HEAD~1

# Mixed reset (default) — undo commit, unstage changes, keep files
git reset HEAD~1

# Hard reset — undo commit AND discard all changes ⚠️ DESTRUCTIVE
git reset --hard HEAD~1
git reset --hard a3f5c9d   # Reset to a specific commit
```

### Revert vs Reset — Which to Use?

| Situation | Use |
|-----------|-----|
| Commit was already pushed to shared branch | `git revert` (safe, adds new commit) |
| Commit only exists locally | `git reset` is fine |
| Want to keep history clean | `git revert` |
| Cleaning up local mess before pushing | `git reset` |

---

## 13. 🔍 Viewing History & Status

### Check Current Status

```bash
# See staged, unstaged, and untracked files
git status

# Short status format
git status -s
# Output:
# M  README.md      (modified and staged)
#  M style.css      (modified, not staged)
# ?? newfile.txt    (untracked)
# A  added.js       (new file, staged)
```

### View Commit History

```bash
# Full log
git log

# One-line summary
git log --oneline

# Graph view (great for seeing branches)
git log --oneline --graph --all --decorate

# Last 5 commits
git log -5

# Commits by a specific author
git log --author="Shahriar"

# Commits since a date
git log --since="2024-01-01"

# Search commit messages
git log --grep="fix"
```

### View Changes (Diff)

```bash
# See unstaged changes
git diff

# See staged changes (what will go in next commit)
git diff --staged
# Old way: git diff --cached

# Compare two branches
git diff main..feature/login

# Compare two commits
git diff a3f5c9d..b7e8f1a

# See what changed in a specific commit
git show a3f5c9d

# See changes in a specific file
git diff README.md
```

### Blame — Who Changed What?

```bash
# See who last changed each line of a file
git blame README.md

# Show blame with line numbers
git blame -n README.md
```

---

## 14. 🏷️ Tags & Releases

Tags mark specific points in history — usually version releases.

```bash
# Create a lightweight tag
git tag v1.0

# Create an annotated tag (recommended — includes message and author info)
git tag -a v1.0.0 -m "Version 1.0.0 - First stable release"

# Tag a specific commit
git tag -a v1.0.0 a3f5c9d -m "Version 1.0.0"

# List all tags
git tag

# View tag details
git show v1.0.0

# Push a tag to GitHub
git push origin v1.0.0

# Push all tags
git push origin --tags

# Delete a local tag
git tag -d v1.0.0

# Delete a remote tag
git push origin --delete v1.0.0
```

---

## 15. 💡 Tips, Tricks & Aliases

### Useful Git Aliases

Set up shortcuts in your `~/.gitconfig`:

```bash
# Add aliases
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.cm "commit -m"
git config --global alias.lg "log --oneline --graph --all --decorate"
git config --global alias.last "log -1 HEAD"
git config --global alias.unstage "restore --staged"
git config --global alias.whoami "config user.email"

# Usage:
git st          # Instead of: git status
git co main     # Instead of: git checkout main
git br          # Instead of: git branch
git lg          # Beautiful branch graph
```

### Useful Tricks

```bash
# See a visual summary of your project graph
git log --oneline --graph --all --decorate

# Find which commit introduced a bug (binary search)
git bisect start
git bisect bad                 # Current commit is broken
git bisect good v1.0           # This version worked
# Git checks out midpoint commits — you test each and mark good/bad
git bisect good                # or: git bisect bad
# Git finds the exact commit!
git bisect reset               # Exit bisect mode

# Show all files tracked by Git
git ls-files

# Show what would be removed by git clean
git clean -n

# Remove untracked files and folders
git clean -fd

# Store credentials so you don't retype password
git config --global credential.helper store       # Permanent (less secure)
git config --global credential.helper cache       # 15 minutes
git config --global credential.helper "cache --timeout=3600"  # 1 hour

# Temporarily ignore a tracked file's changes
git update-index --assume-unchanged config/local.php
# Unignore it later:
git update-index --no-assume-unchanged config/local.php
```

### The .gitignore Cheat Sheet

```gitignore
# Ignore a specific file
secrets.env

# Ignore all .log files
*.log

# Ignore a folder
node_modules/
dist/

# Ignore a folder only in root (not subdirectories)
/build

# Ignore all files in any folder named tmp
**/tmp

# Never ignore a specific file even if pattern matches
!important.log
```

---

## 16. 🌊 Git Workflows

### GitHub Flow (Simple — best for most projects)

```
1. Create a branch from main
2. Make commits
3. Open a Pull Request
4. Review and discuss
5. Merge into main
6. Deploy immediately
```

### Git Flow (Structured — good for versioned releases)

```
main       ──●───────────────────────────●──  (only stable releases)
              │                         ↑│
develop    ──●──●──●──●──●──●──●──●──●── │
              │         ↑   │            │
feature    ──●──●──●────┘   │            │
                             │            │
release                    ──●──●──●──────┘
```

**Branches in Git Flow:**
- `main` — Production code only
- `develop` — Integration branch
- `feature/*` — New features (branch off develop)
- `release/*` — Prep for release (branch off develop)
- `hotfix/*` — Emergency production fixes (branch off main)

---

## 17. 📋 Quick Reference Card

```
╔══════════════════════════════════════════════════════════════════╗
║                    GIT QUICK REFERENCE                           ║
╠══════════════╦═══════════════════════════════════════════════════╣
║ SETUP        ║ git config --global user.name "Name"              ║
║              ║ git config --global user.email "email"            ║
╠══════════════╬═══════════════════════════════════════════════════╣
║ START        ║ git init                  (new repo)              ║
║              ║ git clone <url>           (copy repo)             ║
╠══════════════╬═══════════════════════════════════════════════════╣
║ SNAPSHOT     ║ git status                (check state)           ║
║              ║ git add .                 (stage all)             ║
║              ║ git add <file>            (stage file)            ║
║              ║ git commit -m "msg"       (save snapshot)         ║
╠══════════════╬═══════════════════════════════════════════════════╣
║ SYNC         ║ git push origin main      (upload)                ║
║              ║ git pull origin main      (download+merge)        ║
║              ║ git fetch                 (download only)         ║
╠══════════════╬═══════════════════════════════════════════════════╣
║ BRANCHES     ║ git branch                (list)                  ║
║              ║ git checkout -b <name>    (create+switch)         ║
║              ║ git switch <name>         (switch)                ║
║              ║ git merge <branch>        (merge into current)    ║
║              ║ git branch -d <name>      (delete local)          ║
╠══════════════╬═══════════════════════════════════════════════════╣
║ HISTORY      ║ git log --oneline         (compact log)           ║
║              ║ git diff                  (show changes)          ║
║              ║ git show <hash>           (show commit)           ║
╠══════════════╬═══════════════════════════════════════════════════╣
║ UNDO         ║ git restore <file>        (discard changes)       ║
║              ║ git restore --staged <f>  (unstage)               ║
║              ║ git revert HEAD           (safe undo)             ║
║              ║ git reset --soft HEAD~1   (undo commit, keep)     ║
║              ║ git reset --hard HEAD~1   (undo commit, delete)   ║
╠══════════════╬═══════════════════════════════════════════════════╣
║ STASH        ║ git stash                 (save temporarily)      ║
║              ║ git stash pop             (restore)               ║
║              ║ git stash list            (see all)               ║
╠══════════════╬═══════════════════════════════════════════════════╣
║ REMOTE       ║ git remote -v             (show remotes)          ║
║              ║ git remote add o <url>    (add remote)            ║
╚══════════════╩═══════════════════════════════════════════════════╝
```

---

<div align="center">

📖 Back to [README.md](./README.md) | ⭐ Star the repo if this helped!

Made with ❤️ by [Shahriar Hasib](https://github.com/shahriarhasib)

</div>
