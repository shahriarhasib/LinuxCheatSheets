# 🧰 Git Cheat Sheet — Complete Command Reference

> **A full, step-by-step Git guide from installation to advanced workflows**  
> 📁 Part of the [LinuxCheatSheets](https://github.com/shahriarhasib/LinuxCheatSheets) collection

---

## 📚 Table of Contents

1. [Installing Git on Windows 11](#1--installing-git-on-windows-11)
2. [Installing Git on Linux](#2--installing-git-on-linux)
3. [First-Time Git Configuration](#3--first-time-git-configuration)
4. [SSH Key Setup & SSH to GitHub from Windows](#4--ssh-key-setup--ssh-to-github-from-windows)
5. [Create a New Git Repository](#5--create-a-new-git-repository)
6. [Create a New Folder Under a Repo](#6--create-a-new-folder-under-a-repo)
7. [Create a New Branch](#7--create-a-new-branch)
8. [Add, Commit, Push & Pull](#8--add-commit-push--pull)
9. [Working Across Branches and Folders](#9--working-across-branches-and-folders)
10. [Cloning a Repository](#10--cloning-a-repository)
11. [Fresh Clone — Replace an Existing Local Copy](#11--fresh-clone--replace-an-existing-local-copy)
12. [Syncing & Updating Your Repo](#12--syncing--updating-your-repo)
13. [Merging & Resolving Conflicts](#13--merging--resolving-conflicts)
14. [Undoing Mistakes](#14--undoing-mistakes)
15. [Viewing History & Status](#15--viewing-history--status)
16. [See All Repos, Submodules & Folder Structure](#16--see-all-repos-submodules--folder-structure)
17. [Rename a Repository](#17--rename-a-repository)
18. [Rename a File or Folder](#18--rename-a-file-or-folder)
19. [Git Submodules — Complete Guide](#19--git-submodules--complete-guide)
20. [Move a Repo into Another Repo as a Normal Folder](#20--move-a-repo-into-another-repo-as-a-normal-folder)
21. [Switch Context — Repo / Branch / Folder / Submodule](#21--switch-context--repo--branch--folder--submodule)
22. [Global .gitignore — Ignore .ini Files Everywhere](#22--global-gitignore--ignore-ini-files-everywhere)
23. [Tags & Releases](#23--tags--releases)
24. [Tips, Tricks & Aliases](#24--tips-tricks--aliases)
25. [Git Workflows](#25--git-workflows)
26. [Quick Reference Card](#26--quick-reference-card)

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

---

## 4. 🔐 SSH Key Setup & SSH to GitHub from Windows

SSH lets you authenticate with GitHub/GitLab **without typing your password** every time. It is faster, more secure, and required for many CI/CD setups.

### Why SSH over HTTPS?

| | HTTPS | SSH |
|-|-------|-----|
| 🔑 Auth method | Username + token/password | SSH key pair |
| 🔒 Security | Good | Better (key-based) |
| 🔁 Re-auth needed? | Yes (or credential cache) | No (once key is added) |
| 🖥️ Windows setup | Easy | One-time setup |
| 🤖 CI/CD friendly | ✅ | ✅ (preferred) |

---

### Step 1 — Generate an SSH Key Pair

Open **Git Bash** (Windows) or a **Terminal** (Linux/macOS):

```bash
# Generate a modern ed25519 key (recommended)
ssh-keygen -t ed25519 -C "your.email@example.com"

# If your system doesn't support ed25519, use RSA 4096-bit:
ssh-keygen -t rsa -b 4096 -C "your.email@example.com"
```

The prompts:
```
Enter file in which to save the key: → Press Enter (uses default ~/.ssh/id_ed25519)
Enter passphrase (empty for no passphrase): → Press Enter (or set one for extra security)
Enter same passphrase again: → Press Enter again
```

Your keys are now at:
```
~/.ssh/id_ed25519       ← PRIVATE key  ⚠️ Never share this!
~/.ssh/id_ed25519.pub   ← PUBLIC key   ✅ This goes to GitHub
```

---

### Step 2 — Start the SSH Agent (Windows — Git Bash)

The SSH agent holds your key in memory so you don't re-enter a passphrase:

```bash
# Start the agent
eval "$(ssh-agent -s)"
# Output: Agent pid 1234

# Add your private key to the agent
ssh-add ~/.ssh/id_ed25519

# Verify key is loaded
ssh-add -l
# Output: 256 SHA256:xxxx your.email@example.com (ED25519)
```

#### Make SSH Agent Auto-Start on Windows (Git Bash)

Add this to your `~/.bashrc` or `~/.bash_profile` so it starts automatically:

```bash
# Auto-start ssh-agent in Git Bash
cat >> ~/.bashrc << 'EOF'

# Auto-start SSH agent
env=~/.ssh/agent.env
agent_load_env () { test -f "$env" && . "$env" >| /dev/null ; }
agent_start () {
    (umask 077; ssh-agent >| "$env")
    . "$env" >| /dev/null ;
}
agent_load_env
agent_run_state=$(ssh-add -l >| /dev/null 2>&1; echo $?)
if [ ! "$SSH_AUTH_SOCK" ] || [ $agent_run_state = 2 ]; then
    agent_start
    ssh-add ~/.ssh/id_ed25519
elif [ "$SSH_AUTH_SOCK" ] && [ $agent_run_state = 1 ]; then
    ssh-add ~/.ssh/id_ed25519
fi
unset env
EOF
```

---

### Step 3 — Add Public Key to GitHub

```bash
# Display your public key — copy ALL of this output
cat ~/.ssh/id_ed25519.pub
# Output: ssh-ed25519 AAAA...long string... your.email@example.com
```

Then on GitHub:
```
1. Go to: github.com → Profile photo → Settings
2. Left sidebar: "SSH and GPG keys"
3. Click: "New SSH key"
4. Title: Give it a name (e.g., "Windows Laptop" or "Work PC")
5. Key type: Authentication Key
6. Key: Paste your public key
7. Click: "Add SSH key"
```

For GitLab:
```
1. Go to: gitlab.com → User Settings → SSH Keys
2. Paste your public key and set an expiry date
3. Click "Add key"
```

---

### Step 4 — Test Your Connection

```bash
# Test GitHub connection
ssh -T git@github.com
# Expected: Hi shahriarhasib! You've successfully authenticated, but GitHub
#           does not provide shell access.

# Test GitLab connection
ssh -T git@gitlab.com
# Expected: Welcome to GitLab, @username!

# Verbose test (shows exactly what's happening — useful for debugging)
ssh -vT git@github.com
```

---

### Step 5 — Use SSH URLs for Git Operations

```bash
# ✅ SSH URL format
git clone git@github.com:shahriarhasib/LinuxCheatSheets.git

# ❌ HTTPS URL format (needs token/password)
git clone https://github.com/shahriarhasib/LinuxCheatSheets.git

# Switch an existing repo from HTTPS to SSH
git remote set-url origin git@github.com:shahriarhasib/LinuxCheatSheets.git

# Verify the change
git remote -v
# Output:
# origin  git@github.com:shahriarhasib/LinuxCheatSheets.git (fetch)
# origin  git@github.com:shahriarhasib/LinuxCheatSheets.git (push)
```

---

### Multiple SSH Keys (Multiple GitHub Accounts)

If you have multiple GitHub accounts (e.g., personal + work):

```bash
# Step 1: Generate a second key with a different filename
ssh-keygen -t ed25519 -C "work@company.com" -f ~/.ssh/id_ed25519_work

# Step 2: Create/edit ~/.ssh/config
```

```
# ~/.ssh/config

# Personal GitHub account
Host github.com
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_ed25519

# Work GitHub account
Host github-work
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_ed25519_work
```

```bash
# Step 3: Use the alias in clone/remote URLs
git clone git@github-work:company/project.git

# Or update an existing remote
git remote set-url origin git@github-work:company/project.git
```

---

### Verify SSH Setup — Full Checklist

```bash
# ✅ 1. Keys exist
ls -la ~/.ssh/
# Should see: id_ed25519  id_ed25519.pub

# ✅ 2. Agent is running and key is loaded
ssh-add -l

# ✅ 3. Public key is on GitHub (check in browser)

# ✅ 4. Connection works
ssh -T git@github.com

# ✅ 5. Remote URL uses SSH (not HTTPS)
git remote -v
```

---

## 5. 📦 Create a New Git Repository

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

## 6. 📂 Create a New Folder Under a Repo

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

## 7. 🌿 Create a New Branch

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

## 8. ➕ Add, Commit, Push & Pull

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

## 9. 🔀 Working Across Branches and Folders

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

## 10. 📥 Cloning a Repository

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

## 11. 🔁 Fresh Clone — Replace an Existing Local Copy

Sometimes your local repo is out of sync, corrupted, or just messy and you want a clean restart from the remote.

### Option A: Delete & Re-clone (Cleanest Method)

```bash
# Step 1: Navigate to parent folder (one level ABOVE your repo)
cd ~/projects

# Step 2: Fully delete the old local copy
rm -rf LinuxCheatSheets           # Linux/macOS/Git Bash on Windows
# Windows CMD:
# rmdir /s /q LinuxCheatSheets

# Step 3: Clone fresh
git clone git@github.com:shahriarhasib/LinuxCheatSheets.git

# Step 4: Navigate in and verify
cd LinuxCheatSheets
git log --oneline -5
git status
```

### Option B: Hard Reset Without Deleting (Keeps Git history)

```bash
cd LinuxCheatSheets

# Fetch all latest from remote
git fetch --all

# Hard reset your branch to match remote exactly
git reset --hard origin/main

# Remove any untracked files and folders
git clean -fd

# Verify — should say "nothing to commit, working tree clean"
git status
```

### Option C: Re-clone With Submodules

If your repo has submodules, include them in the fresh clone:

```bash
# Delete old copy
rm -rf LinuxCheatSheets

# Clone and immediately init + update all submodules
git clone --recurse-submodules git@github.com:shahriarhasib/LinuxCheatSheets.git

# Verify submodules were populated
cd LinuxCheatSheets
git submodule status
```

### When to Use Each Option

| Situation | Best Option |
|-----------|-------------|
| Repo is corrupt / .git folder broken | Option A (delete & re-clone) |
| Too many uncommitted changes to untangle | Option A |
| You just want to sync to remote HEAD | Option B (hard reset) |
| You have submodules | Option C |

---

## 12. 🔄 Syncing & Updating After Changes

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

## 13. 🔀 Merging & Resolving Conflicts

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

## 14. ↩️ Undoing Mistakes

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

## 15. 🔍 Viewing History & Status

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

## 16. 🗂️ See All Repos, Submodules & Folder Structure

### List All Local Git Repositories on Your Machine

```bash
# Find every git repo under your home folder
find ~ -name ".git" -type d 2>/dev/null

# More readable — show only the parent folder of each .git
find ~ -name ".git" -type d -prune 2>/dev/null | sed 's|/.git||'

# Find repos only 2 levels deep (faster for large systems)
find ~ -maxdepth 3 -name ".git" -type d -prune 2>/dev/null | sed 's|/.git||'
```

### List All Submodules in the Current Repo

```bash
# Show all registered submodules with their status
git submodule status

# Output explained:
#  abc1234 tools/logger (v1.2.0)   ← ✅ Up to date
# -abc1234 tools/logger            ← ❌ Not initialized yet
# +abc1234 tools/logger (v1.2.0)   ← ⚠️ Has local changes

# Show submodule paths from .gitmodules config file
cat .gitmodules

# List submodule names only
git config --file .gitmodules --get-regexp path | awk '{ print $2 }'
```

### See Folder & File Tree Structure

```bash
# Simple tree view using find (works on all systems)
find . -not -path "./.git/*" | sort | sed 's|[^/]*/|  |g'

# Using the 'tree' command (install separately if needed)
# Install on Ubuntu/Debian:
sudo apt install tree

# Install on Windows via Git Bash / Choco:
choco install tree

# Basic tree
tree

# Tree ignoring node_modules and .git
tree -I "node_modules|.git"

# Show only directories (no files)
tree -d

# Show 2 levels deep only
tree -L 2

# Show hidden files too
tree -a -I ".git"

# Show file sizes
tree -sh
```

### See What's Inside a Repo at a Glance

```bash
# Current branch, staged/unstaged summary
git status

# All tracked files in the repo
git ls-files

# All tracked files including submodule files
git ls-files --recurse-submodules

# See all remote branches
git branch -r

# See all local + remote branches
git branch -a
```

### Verify Everything Is Clean

```bash
# Full health check — run these in sequence:
git status                    # Should say: nothing to commit
git submodule status          # No leading - or + signs
git remote -v                 # Correct remote URLs
git log --oneline -3          # Recent commit history looks right
git fetch --dry-run           # See if remote has anything new
```

---

## 17. ✏️ Rename a Repository

### Rename on GitHub (Remote)

```
1. Go to: github.com/shahriarhasib/old-repo-name
2. Click "Settings" tab (top of repo page)
3. Under "Repository name", type the new name
4. Click "Rename"
```

> ⚠️ GitHub will automatically redirect old URLs, but you should still update your local remote URL.

### Update Your Local Remote URL After Renaming

```bash
# Check current remote URL
git remote -v
# Output: origin  git@github.com:shahriarhasib/old-repo-name.git (fetch)

# Update to new name
git remote set-url origin git@github.com:shahriarhasib/new-repo-name.git

# Verify
git remote -v
# Output: origin  git@github.com:shahriarhasib/new-repo-name.git (fetch)

# Test that it still works
git fetch origin
```

### Rename the Local Folder to Match

```bash
# Navigate to parent folder
cd ~/projects

# Rename the local folder
mv old-repo-name new-repo-name

# Navigate in and verify
cd new-repo-name
git remote -v
```

---

## 18. 📝 Rename a File or Folder

### Rename a File (Git-Tracked)

```bash
# ✅ Correct way — Git tracks this as a rename (preserves history)
git mv old-filename.txt new-filename.txt

# Stage and commit
git commit -m "Rename old-filename.txt to new-filename.txt"
```

```bash
# ⚠️ If you rename via file explorer or 'mv' without git:
mv old-filename.txt new-filename.txt
# Git sees this as: deleted old-filename.txt + new untracked new-filename.txt

# Fix by staging both changes
git add -A
git commit -m "Rename file"
# Git is smart enough to detect it as a rename if >50% content matches
```

### Rename a Folder

```bash
# Rename a folder with Git
git mv old-folder-name/ new-folder-name/
git commit -m "Rename folder old-folder-name to new-folder-name"

# Rename a deeply nested folder
git mv src/components/oldname/ src/components/newname/
git commit -m "Rename component folder"
```

### Rename a Branch

```bash
# Rename current branch
git branch -m new-branch-name

# Rename a different branch (while on another)
git branch -m old-branch-name new-branch-name

# Rename on remote too:
# Step 1: Delete old remote branch
git push origin --delete old-branch-name

# Step 2: Push renamed branch with tracking
git push -u origin new-branch-name
```

### Verify a Rename Was Tracked Correctly

```bash
# See Git detected it as a rename (not delete+add)
git log --diff-filter=R --summary --oneline

# Check history of the renamed file (follow renames)
git log --follow new-filename.txt
```

---

## 19. 🧩 Git Submodules — Complete Guide

A **submodule** is a Git repo embedded inside another Git repo. The parent repo stores a pointer to a specific commit of the child repo — not the child's actual files.

```
parent-repo/
├── .git/
├── .gitmodules        ← Config file listing all submodules
├── README.md
└── tools/
    └── logger/        ← This is a submodule (separate git repo!)
        ├── .git       ← Submodule has its own .git
        └── src/
```

### Add an Existing Repo as a Submodule

```bash
# Navigate to parent repo
cd parent-repo

# Add a submodule at a specific path
git submodule add git@github.com:shahriarhasib/logger.git tools/logger

# This creates/updates .gitmodules and stages changes
cat .gitmodules
# Output:
# [submodule "tools/logger"]
#     path = tools/logger
#     url = git@github.com:shahriarhasib/logger.git

# Commit the addition
git add .gitmodules tools/logger
git commit -m "Add logger as submodule at tools/logger"
git push origin main
```

### Clone a Repo That Has Submodules

```bash
# Method 1: Clone and init submodules in one shot
git clone --recurse-submodules git@github.com:shahriarhasib/parent-repo.git

# Method 2: Clone first, then init
git clone git@github.com:shahriarhasib/parent-repo.git
cd parent-repo
git submodule init
git submodule update

# Shorthand for init+update
git submodule update --init

# Init + update including nested submodules (submodules of submodules)
git submodule update --init --recursive
```

### Update Submodules to Latest

```bash
# Update all submodules to the commit the parent points to
git submodule update

# Update all submodules to their latest remote commit
git submodule update --remote

# Update a specific submodule only
git submodule update --remote tools/logger

# Pull latest in all submodules (runs git pull in each)
git submodule foreach git pull origin main
```

### Work Inside a Submodule

```bash
# Navigate into submodule
cd tools/logger

# Submodules start in "detached HEAD" state — attach to a branch first
git checkout main

# Make changes, commit as normal
echo "fix" >> src/logger.js
git add .
git commit -m "Fix logger output"
git push origin main

# Navigate back to parent
cd ../..

# The parent now sees the submodule has moved ahead — stage and commit
git add tools/logger
git commit -m "Update logger submodule to latest"
git push origin main
```

### Remove a Submodule

```bash
# Step 1: Deinit the submodule
git submodule deinit -f tools/logger

# Step 2: Remove from Git index
git rm -f tools/logger

# Step 3: Clean up the .git/modules cache
rm -rf .git/modules/tools/logger

# Step 4: Commit the removal
git commit -m "Remove logger submodule"
git push origin main
```

### Copy / Move a Repo INTO Another Repo as a Submodule

```bash
# Scenario: You want 'my-utils' repo to become a submodule of 'main-app'

# Step 1: Navigate to main-app
cd main-app

# Step 2: Add my-utils as a submodule
git submodule add git@github.com:shahriarhasib/my-utils.git src/my-utils

# Step 3: Commit
git add .gitmodules src/my-utils
git commit -m "Add my-utils as submodule at src/my-utils"
git push origin main

# Step 4: Verify
git submodule status
# Output:  abc1234 src/my-utils (main)
```

### Change the Path of an Existing Submodule

```bash
# Move submodule from tools/logger → libs/logger

# Step 1: Edit .gitmodules
nano .gitmodules
# Change: path = tools/logger
# To:     path = libs/logger

# Step 2: Move the actual folder
git mv tools/logger libs/logger

# Step 3: Sync and update
git submodule sync
git submodule update --init

# Step 4: Commit
git add .gitmodules
git commit -m "Move logger submodule from tools/ to libs/"
```

---

## 20. 📦 Move a Repo into Another Repo as a Normal Folder

Sometimes you want to **merge** a repo's files directly into another repo — without keeping it as a separate submodule. All commits and history can be preserved.

### Method A: Simple Copy (No History Preserved)

```bash
# Step 1: Clone the repo you want to absorb
git clone git@github.com:shahriarhasib/my-utils.git /tmp/my-utils

# Step 2: Copy its files into your main repo
cp -r /tmp/my-utils/src/* main-app/src/utils/

# Step 3: Remove the .git folder from copied files (it's not a submodule)
# (The cp above won't copy .git since it's a hidden special folder)

# Step 4: Stage and commit
cd main-app
git add src/utils/
git commit -m "Import my-utils source files into src/utils"
git push origin main
```

### Method B: Merge with Full History Preserved (Advanced)

```bash
cd main-app

# Step 1: Add the other repo as a temporary remote
git remote add utils-remote git@github.com:shahriarhasib/my-utils.git

# Step 2: Fetch its history
git fetch utils-remote

# Step 3: Merge it in (allowing unrelated histories)
git merge --allow-unrelated-histories utils-remote/main

# Step 4: Move its files into a subfolder (optional)
mkdir -p src/utils
git mv *.js src/utils/    # Move all root .js files to subfolder
git commit -m "Reorganize imported utils into src/utils"

# Step 5: Remove the temporary remote
git remote remove utils-remote

# Step 6: Push
git push origin main
```

### Move Files INTO a Submodule Folder

```bash
# Move a regular folder's files into an existing submodule path

# Step 1: Make sure submodule is initialized
git submodule update --init

# Step 2: Copy files into submodule
cp -r my-local-module/* tools/my-submodule/

# Step 3: Commit inside the submodule
cd tools/my-submodule
git add .
git commit -m "Add imported files"
git push origin main

# Step 4: Update parent to point to new submodule commit
cd ../..
git add tools/my-submodule
git commit -m "Update submodule pointer after import"
git push origin main
```

---

## 21. 🔀 Switch Context — Repo / Branch / Folder / Submodule

A clear reference for navigating between everything in Git.

### Switch Between Local Repositories

```bash
# Simply change directory
cd ~/projects/repo-a
cd ~/projects/repo-b

# Quick check: confirm which repo you're in
git remote get-url origin
# or
git rev-parse --show-toplevel    # Shows root path of current repo
```

### Switch Between Branches

```bash
# See all branches
git branch -a

# Switch to an existing branch
git switch main
git switch feature/login
# Old syntax (still works):
git checkout main

# Switch and create a new branch
git switch -c new-feature
git checkout -b new-feature

# Return to the previous branch (like cd -)
git switch -
git checkout -
```

### Switch Between Folders

```bash
# Move into a subfolder within your repo
cd src/components

# Go back to repo root
cd $(git rev-parse --show-toplevel)

# Alias for "go to repo root"
alias groot='cd $(git rev-parse --show-toplevel)'
# Then just type: groot
```

### Switch Into a Submodule

```bash
# Navigate into a submodule
cd tools/logger

# Check which commit it's on (may be detached HEAD)
git status
git log --oneline -3

# Attach to a branch to make commits
git checkout main
# or
git switch main

# Go back to parent repo
cd ../..
# or use:
cd $(git rev-parse --show-toplevel)
```

### Check Exactly Where You Are

```bash
# What repo?
git rev-parse --show-toplevel

# What branch?
git branch --show-current

# What commit?
git log --oneline -1

# Are you in a submodule?
git rev-parse --show-superproject-working-tree
# Empty output = you're in the parent repo
# A path = you're inside a submodule (shows parent repo path)

# Full context at a glance
echo "Repo:   $(git rev-parse --show-toplevel)"
echo "Branch: $(git branch --show-current)"
echo "Commit: $(git log --oneline -1)"
echo "Status: $(git status -s | wc -l) changed files"
```

---

## 22. 🚫 Global .gitignore — Ignore .ini Files Everywhere

A **global `.gitignore`** applies to ALL your repos on your machine — perfect for system files, editor configs, and patterns you never want to commit anywhere.

### Set Up Global .gitignore

```bash
# Step 1: Create the global ignore file
touch ~/.gitignore_global

# Step 2: Tell Git to use it
git config --global core.excludesFile ~/.gitignore_global

# Verify it's set
git config --global core.excludesFile
# Output: /home/youruser/.gitignore_global
```

### Add .ini Pattern to Global .gitignore

```bash
# Open and add patterns
nano ~/.gitignore_global
```

Add these lines:

```gitignore
# ── Windows INI / Config files ──────────────────────────────
# Ignore ALL .ini files in any folder, subfolder, or submodule
*.ini
**/*.ini

# Common Windows system files (good to add too)
Thumbs.db
Desktop.ini
desktop.ini
$RECYCLE.BIN/

# macOS system files
.DS_Store
.AppleDouble
.LSOverride

# Editor temp files
*.swp
*~
.vscode/settings.json
.idea/

# Environment secrets (never commit these!)
.env
.env.local
.env.*.local
```

> 💡 `*.ini` catches `.ini` files in any folder. `**/*.ini` ensures it catches them in deeply nested submodule paths too. Both together = complete coverage.

### Verify Global Ignore Is Working

```bash
# Create a test .ini file
touch /tmp/test-repo/config.ini

# Check if Git would ignore it
cd /tmp/test-repo
git init
git check-ignore -v config.ini
# Output: /home/user/.gitignore_global:2:*.ini  config.ini
# (Shows which rule in which file is causing the ignore)

# Check multiple files at once
git check-ignore -v *.ini **/*.ini

# See all ignored files in current repo
git status --ignored
```

### Per-Repo .gitignore vs Global .gitignore

| | Per-Repo `.gitignore` | Global `~/.gitignore_global` |
|-|-----------------------|------------------------------|
| Location | Inside each repo | Your home folder |
| Committed to repo? | ✅ Yes (shared with team) | ❌ No (personal only) |
| Best For | Project-specific ignores | Personal/machine-specific ignores |
| Example | `node_modules/`, `dist/` | `.DS_Store`, `*.ini`, `.vscode/` |

### Force-Remove an Already-Tracked .ini File

If a `.ini` file was committed before you added the ignore rule:

```bash
# Remove it from Git tracking (but keep the file on disk)
git rm --cached config.ini
git rm --cached "**/*.ini"   # Remove all tracked .ini files recursively

# Commit the removal
git commit -m "Stop tracking .ini files (add to .gitignore)"
git push origin main
```

---

## 23. 🏷️ Tags & Releases

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

## 24. 💡 Tips, Tricks & Aliases

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

## 25. 🌊 Git Workflows

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

## 26. 📋 Quick Reference Card
```
╔════════════════════════════════════════════════════════════════════╗
║                     GIT QUICK REFERENCE                            ║
╠═══════════════╦════════════════════════════════════════════════════╣
║ SETUP         ║ git config --global user.name "Name"               ║
║               ║ git config --global user.email "email"             ║
╠═══════════════╬════════════════════════════════════════════════════╣
║ SSH           ║ ssh-keygen -t ed25519 -C "email"   (generate)      ║
║               ║ ssh-add ~/.ssh/id_ed25519           (load key)     ║
║               ║ ssh -T git@github.com               (test)         ║
╠═══════════════╬════════════════════════════════════════════════════╣
║ START         ║ git init                   (new repo)              ║
║               ║ git clone <url>            (copy repo)             ║
║               ║ git clone --recurse-submodules <url>               ║
╠═══════════════╬════════════════════════════════════════════════════╣
║ SNAPSHOT      ║ git status                 (check state)           ║
║               ║ git add .                  (stage all)             ║
║               ║ git add <file>             (stage file)            ║
║               ║ git commit -m "msg"        (save snapshot)         ║
╠═══════════════╬════════════════════════════════════════════════════╣
║ SYNC          ║ git push origin main       (upload)                ║
║               ║ git pull origin main       (download+merge)        ║
║               ║ git fetch                  (download only)         ║
╠═══════════════╬════════════════════════════════════════════════════╣
║ FRESH CLONE   ║ rm -rf <repo> && git clone <url>   (full reset)    ║
║               ║ git reset --hard origin/main       (hard reset)    ║
║               ║ git clean -fd                      (remove junk)   ║
╠═══════════════╬════════════════════════════════════════════════════╣
║ BRANCHES      ║ git branch -a              (list all)              ║
║               ║ git switch -c <name>       (create+switch)         ║
║               ║ git switch <name>          (switch)                ║
║               ║ git switch -               (previous branch)       ║
║               ║ git merge <branch>         (merge into current)    ║
║               ║ git branch -d <name>       (delete local)          ║
╠═══════════════╬════════════════════════════════════════════════════╣
║ RENAME        ║ git mv old.txt new.txt     (rename file)           ║
║               ║ git branch -m new-name     (rename branch)         ║
║               ║ git remote set-url origin <new-url>                ║
╠═══════════════╬════════════════════════════════════════════════════╣
║ SUBMODULES    ║ git submodule status       (list submodules)       ║
║               ║ git submodule add <url> <path>                     ║
║               ║ git submodule update --init --recursive            ║
║               ║ git submodule update --remote  (pull latest)       ║
║               ║ git submodule deinit -f <path> (remove)            ║
╠═══════════════╬════════════════════════════════════════════════════╣
║ NAVIGATE      ║ cd $(git rev-parse --show-toplevel)   (root)       ║
║               ║ git branch --show-current  (current branch)        ║
║               ║ git rev-parse --show-toplevel (repo path)          ║
╠═══════════════╬════════════════════════════════════════════════════╣
║ STRUCTURE     ║ tree -I ".git|node_modules" (folder tree)          ║
║               ║ git ls-files --recurse-submodules                  ║
║               ║ find ~ -name ".git" -prune  (find all repos)       ║
╠═══════════════╬════════════════════════════════════════════════════╣
║ HISTORY       ║ git log --oneline          (compact log)           ║
║               ║ git diff                   (show changes)          ║
║               ║ git show <hash>            (show commit)           ║
╠═══════════════╬════════════════════════════════════════════════════╣
║ UNDO          ║ git restore <file>         (discard changes)       ║
║               ║ git restore --staged <f>   (unstage)               ║
║               ║ git revert HEAD            (safe undo)             ║
║               ║ git reset --soft HEAD~1    (undo commit, keep)     ║
║               ║ git reset --hard HEAD~1    (undo commit, delete)   ║
╠═══════════════╬════════════════════════════════════════════════════╣
║ STASH         ║ git stash                  (save temporarily)      ║
║               ║ git stash pop              (restore)               ║
║               ║ git stash list             (see all)               ║
╠═══════════════╬════════════════════════════════════════════════════╣
║ IGNORE        ║ core.excludesFile ~/.gitignore_global  (global)    ║
║               ║ git check-ignore -v <file> (test ignore rule)      ║
║               ║ git rm --cached <file>     (untrack tracked file)  ║
╠═══════════════╬════════════════════════════════════════════════════╣
║ REMOTE        ║ git remote -v              (show remotes)          ║
║               ║ git remote add origin <url> (add remote)           ║
╚═══════════════╩════════════════════════════════════════════════════╝
```


---

<div align="center">

📖 Back to [README.md](./README.md) | ⭐ Star the repo if this helped!

Made with ❤️ by [Shahriar Hasib](https://github.com/shahriarhasib)

</div>
