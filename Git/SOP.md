# 📋 Git SOP — Standard Operating Procedures for Beginners

> **Simple, numbered steps for the most common Git tasks. No jargon. Just follow the steps.**  
> 📁 Part of the [LinuxCheatSheets](https://github.com/shahriarhasib/LinuxCheatSheets) collection  
> 📖 For full explanations, see [GitCheatSheet.md](./GitCheatSheet.md)

---

## 📚 Table of Contents

| # | Task | When to Use |
|---|------|-------------|
| [SOP-01](#sop-01--one-time-setup-do-this-once-ever) | One-Time Setup | First time only |
| [SOP-02](#sop-02--push-a-new-project-to-github) | Push a New Project to GitHub | You have local code, want it on GitHub |
| [SOP-03](#sop-03--clone-an-existing-repo-from-github) | Clone a Repo from GitHub | Get someone else's (or your own) repo |
| [SOP-04](#sop-04--daily-push-routine-save-your-work) | Daily Push Routine | Every time you finish working |
| [SOP-05](#sop-05--pull-get-the-latest-changes) | Pull Latest Changes | Before you start working each day |
| [SOP-06](#sop-06--create-and-work-on-a-new-branch) | Create & Work on a Branch | For new features or fixes |
| [SOP-07](#sop-07--add-a-submodule-to-your-repo) | Add a Submodule | Embed another repo inside yours |
| [SOP-08](#sop-08--clone-a-repo-that-has-submodules) | Clone Repo with Submodules | Get a repo that contains submodules |
| [SOP-09](#sop-09--fresh-re-clone-replace-local-copy) | Fresh Re-Clone | When your local copy is broken/messy |
| [SOP-10](#sop-10--check-whats-going-on-verify) | Check & Verify Status | When something feels wrong |

---

## SOP-01 · One-Time Setup *(Do this once, ever)*

> ✅ **When:** The very first time you install Git on a machine.

```
Step 1 — Tell Git your name
────────────────────────────────────────────────────────────
  git config --global user.name "Your Full Name"

Step 2 — Tell Git your email (must match your GitHub account)
────────────────────────────────────────────────────────────
  git config --global user.email "you@example.com"

Step 3 — Set default branch name to "main"
────────────────────────────────────────────────────────────
  git config --global init.defaultBranch main

Step 4 — Generate your SSH key
────────────────────────────────────────────────────────────
  ssh-keygen -t ed25519 -C "you@example.com"
  → Press Enter for all prompts

Step 5 — Load the SSH key into your session
────────────────────────────────────────────────────────────
  eval "$(ssh-agent -s)"
  ssh-add ~/.ssh/id_ed25519

Step 6 — Copy your public key
────────────────────────────────────────────────────────────
  cat ~/.ssh/id_ed25519.pub
  → Select ALL the output text and copy it

Step 7 — Add key to GitHub
────────────────────────────────────────────────────────────
  → Go to: github.com
  → Click your profile photo → Settings
  → Left menu: "SSH and GPG keys"
  → Click: "New SSH key"
  → Title: name your computer (e.g. "My Laptop")
  → Paste the key → Click "Add SSH key"

Step 8 — Test the connection
────────────────────────────────────────────────────────────
  ssh -T git@github.com
  → You should see: "Hi [username]! You've successfully authenticated"

✅ DONE — You never need to do this again on this machine.
```

---

## SOP-02 · Push a New Project to GitHub

> ✅ **When:** You have a folder of code on your computer and want to put it on GitHub for the first time.

### Before you start:
Create an **empty** repo on GitHub first:
```
→ Go to: github.com → Click "+" → "New repository"
→ Repository name: your-project-name
→ Leave it EMPTY (no README, no .gitignore)
→ Click "Create repository"
→ Copy the SSH URL shown: git@github.com:username/your-project-name.git
```

### Then in your terminal:

```
Step 1 — Open your project folder
────────────────────────────────────────────────────────────
  cd path/to/your-project

  Example (Windows Git Bash):  cd /c/Users/YourName/projects/my-app
  Example (Linux):              cd ~/projects/my-app

Step 2 — Initialize Git in the folder
────────────────────────────────────────────────────────────
  git init

Step 3 — Stage all your files
────────────────────────────────────────────────────────────
  git add .

Step 4 — Make your first commit
────────────────────────────────────────────────────────────
  git commit -m "Initial commit"

Step 5 — Connect to your GitHub repo
────────────────────────────────────────────────────────────
  git remote add origin git@github.com:USERNAME/REPO-NAME.git
  
  ⚠️ Replace USERNAME and REPO-NAME with yours

Step 6 — Push your code to GitHub
────────────────────────────────────────────────────────────
  git push -u origin main

Step 7 — Verify
────────────────────────────────────────────────────────────
  → Go to your GitHub repo in the browser
  → Refresh — your files should now be there ✅

✅ DONE — Your project is now on GitHub!
```

---

## SOP-03 · Clone an Existing Repo from GitHub

> ✅ **When:** You want to download a repo from GitHub to work on it locally.

```
Step 1 — Get the SSH URL from GitHub
────────────────────────────────────────────────────────────
  → Go to the repo on GitHub
  → Click the green "Code" button
  → Click "SSH" tab
  → Copy the URL: git@github.com:username/repo-name.git

Step 2 — Navigate to where you want it saved
────────────────────────────────────────────────────────────
  cd ~/projects
  (Or wherever you keep your code)

Step 3 — Clone the repo
────────────────────────────────────────────────────────────
  git clone git@github.com:username/repo-name.git

  If the repo has submodules, use this instead:
  git clone --recurse-submodules git@github.com:username/repo-name.git

Step 4 — Enter the repo folder
────────────────────────────────────────────────────────────
  cd repo-name

Step 5 — Verify it worked
────────────────────────────────────────────────────────────
  git status
  → Should say: "On branch main, nothing to commit, working tree clean"
  
  git log --oneline -3
  → Should show recent commit history

✅ DONE — The repo is now on your computer and ready to use!
```

---

## SOP-04 · Daily Push Routine *(Save Your Work)*

> ✅ **When:** You've finished working for the day, or completed a feature/fix.

```
Step 1 — Check what has changed
────────────────────────────────────────────────────────────
  git status
  
  You'll see files listed as:
    Modified  → files you changed
    New file  → files you created
    Deleted   → files you removed

Step 2 — Stage your changes
────────────────────────────────────────────────────────────
  git add .
  
  (Stages ALL changes at once)
  
  OR stage specific files only:
  git add filename.txt

Step 3 — Double-check what you're about to commit
────────────────────────────────────────────────────────────
  git status
  → All files should now be listed under "Changes to be committed"

Step 4 — Commit with a meaningful message
────────────────────────────────────────────────────────────
  git commit -m "Describe what you did"
  
  ✅ Good examples:
     git commit -m "Add login form to homepage"
     git commit -m "Fix typo in README"
     git commit -m "Update config for production"
  
  ❌ Bad examples:
     git commit -m "stuff"
     git commit -m "fix"
     git commit -m "asdfgh"

Step 5 — Push to GitHub
────────────────────────────────────────────────────────────
  git push
  
  (If this is the first push of a new branch):
  git push -u origin your-branch-name

Step 6 — Verify
────────────────────────────────────────────────────────────
  git status
  → Should say: "nothing to commit, working tree clean"
  
  → Check GitHub in browser — your files should be updated ✅

✅ DONE — Your work is saved and backed up on GitHub!
```

---

## SOP-05 · Pull — Get the Latest Changes

> ✅ **When:** Before you start working each day, or someone else has pushed changes you need.

```
Step 1 — Make sure you have no uncommitted work
────────────────────────────────────────────────────────────
  git status
  
  If you have uncommitted changes, either:
    a) Commit them first (follow SOP-04 Steps 1-4)
    b) Stash them:  git stash

Step 2 — Switch to the main branch (if not already)
────────────────────────────────────────────────────────────
  git switch main

Step 3 — Pull the latest changes
────────────────────────────────────────────────────────────
  git pull

Step 4 — If you were working on a feature branch, update it too
────────────────────────────────────────────────────────────
  git switch feature/your-branch-name
  git merge main
  
  (This brings the latest main changes into your branch)

Step 5 — Restore stashed work (if you stashed in Step 1)
────────────────────────────────────────────────────────────
  git stash pop

✅ DONE — You're now working with the latest code!
```

---

## SOP-06 · Create and Work on a New Branch

> ✅ **When:** You want to add a new feature or fix a bug without touching the main branch.

```
Step 1 — Start from main and get latest
────────────────────────────────────────────────────────────
  git switch main
  git pull

Step 2 — Create a new branch and switch to it
────────────────────────────────────────────────────────────
  git switch -c feature/your-feature-name
  
  ✅ Good branch name examples:
     feature/user-login
     fix/broken-button
     update/readme-docs
     hotfix/payment-crash

Step 3 — Do your work
────────────────────────────────────────────────────────────
  → Edit, create, or delete files as needed

Step 4 — Stage and commit your work
────────────────────────────────────────────────────────────
  git add .
  git commit -m "Add user login feature"

Step 5 — Push your branch to GitHub
────────────────────────────────────────────────────────────
  git push -u origin feature/your-feature-name

Step 6 — (Optional) Merge back to main when done
────────────────────────────────────────────────────────────
  git switch main
  git merge feature/your-feature-name
  git push

Step 7 — (Optional) Delete the branch after merging
────────────────────────────────────────────────────────────
  git branch -d feature/your-feature-name          ← local
  git push origin --delete feature/your-feature-name  ← remote

✅ DONE — Feature developed safely, merged, and cleaned up!
```

---

## SOP-07 · Add a Submodule to Your Repo

> ✅ **When:** You want to embed another Git repo inside your repo (e.g., a shared library or tool).

```
Step 1 — Navigate to your main repo
────────────────────────────────────────────────────────────
  cd ~/projects/my-main-repo

Step 2 — Add the other repo as a submodule
────────────────────────────────────────────────────────────
  git submodule add git@github.com:username/other-repo.git path/inside/your/repo
  
  Example:
  git submodule add git@github.com:shahriarhasib/logger.git tools/logger

Step 3 — Check what was created
────────────────────────────────────────────────────────────
  cat .gitmodules
  → You'll see the submodule path and URL listed
  
  ls tools/logger
  → The submodule files are now inside your repo

Step 4 — Commit the submodule addition
────────────────────────────────────────────────────────────
  git add .gitmodules tools/logger
  git commit -m "Add logger as submodule at tools/logger"

Step 5 — Push to GitHub
────────────────────────────────────────────────────────────
  git push origin main

Step 6 — Verify on GitHub
────────────────────────────────────────────────────────────
  → Open your repo on GitHub
  → You should see the submodule folder with a special icon (📁 with a link) ✅

✅ DONE — Submodule added and pushed!
```

---

## SOP-08 · Clone a Repo That Has Submodules

> ✅ **When:** You clone a repo and the submodule folders are empty.

```
Step 1 — Clone with submodules in one command (best method)
────────────────────────────────────────────────────────────
  git clone --recurse-submodules git@github.com:username/repo.git
  cd repo

  → All submodule folders will be fully populated ✅

  ─────────────────────────────────
  OR if you already cloned without --recurse-submodules:
  ─────────────────────────────────

Step 1b — Initialize and download submodules after cloning
────────────────────────────────────────────────────────────
  cd repo-you-already-cloned
  git submodule update --init --recursive

Step 2 — Verify submodules are populated
────────────────────────────────────────────────────────────
  git submodule status
  
  ✅ Good output (no leading symbols):
     abc1234 tools/logger (v1.2)
  
  ❌ Bad output (dash means not initialized):
     -abc1234 tools/logger
  
  If you see dashes, run: git submodule update --init --recursive

Step 3 — Keep submodules up to date
────────────────────────────────────────────────────────────
  git submodule update --remote
  git add .
  git commit -m "Update submodules to latest"

✅ DONE — All submodule contents are loaded and ready!
```

---

## SOP-09 · Fresh Re-Clone *(Replace Your Local Copy)*

> ✅ **When:** Your local repo is broken, too messy, or out of sync and you want a clean start.

```
⚠️  WARNING: This deletes your local folder entirely.
    Make sure you've pushed any work you want to keep FIRST.
    
    Check with: git status
    Push with:  git push

Step 1 — Go to the parent folder (one level above your repo)
────────────────────────────────────────────────────────────
  cd ~/projects
  (NOT inside the repo — one level up)

Step 2 — Delete the old local copy
────────────────────────────────────────────────────────────
  On Linux / Git Bash:
  rm -rf repo-name

  On Windows CMD:
  rmdir /s /q repo-name

Step 3 — Clone fresh
────────────────────────────────────────────────────────────
  git clone git@github.com:username/repo-name.git
  
  With submodules:
  git clone --recurse-submodules git@github.com:username/repo-name.git

Step 4 — Enter the repo
────────────────────────────────────────────────────────────
  cd repo-name

Step 5 — Verify
────────────────────────────────────────────────────────────
  git status
  → "nothing to commit, working tree clean" ✅
  
  git log --oneline -3
  → Recent commits visible ✅

✅ DONE — Fresh, clean copy ready to work with!
```

---

## SOP-10 · Check & Verify *(When Something Feels Wrong)*

> ✅ **When:** Something seems off and you want to check the state of everything.

```
RUN THESE COMMANDS IN ORDER:

Check 1 — What branch am I on?
────────────────────────────────────────────────────────────
  git branch --show-current

Check 2 — Any uncommitted changes?
────────────────────────────────────────────────────────────
  git status
  
  ✅ Healthy: "nothing to commit, working tree clean"
  ⚠️  Has changes: files listed under modified/staged

Check 3 — What does recent history look like?
────────────────────────────────────────────────────────────
  git log --oneline -5

Check 4 — Is my remote URL correct?
────────────────────────────────────────────────────────────
  git remote -v
  
  Should show:
  origin  git@github.com:username/repo-name.git (fetch)
  origin  git@github.com:username/repo-name.git (push)

Check 5 — Am I in sync with GitHub?
────────────────────────────────────────────────────────────
  git fetch
  git status
  
  ✅ "Your branch is up to date with 'origin/main'"
  ⚠️  "Your branch is behind" → run: git pull
  ⚠️  "Your branch is ahead"  → run: git push

Check 6 — Are submodules OK? (only if repo has them)
────────────────────────────────────────────────────────────
  git submodule status
  
  ✅ No leading symbols → all good
  ❌ Leading dash (-)  → run: git submodule update --init --recursive
  ⚠️  Leading plus (+) → submodule has local changes

Check 7 — Is my SSH key still working?
────────────────────────────────────────────────────────────
  ssh -T git@github.com
  
  ✅ "Hi username! You've successfully authenticated"
  ❌ Permission denied → re-run SOP-01 Steps 4–8

✅ DONE — If all checks pass, you're in good shape!
```

---

## 🗺️ Decision Guide — Which SOP Do I Need?

```
┌─────────────────────────────────────────────────────────────────┐
│                  What do you want to do?                        │
└──────────────────────────┬──────────────────────────────────────┘
                           │
        ┌──────────────────┼──────────────────────┐
        ▼                  ▼                       ▼
  First time ever    Have local code          Want GitHub code
  on this machine    to put on GitHub         on my computer
        │                  │                       │
   [SOP-01]           [SOP-02]               [SOP-03]
  One-Time Setup     Push New Project         Clone Repo
                                                   │
                           ┌───────────────────────┘
                           ▼
              ┌─────────────────────────────┐
              │   Day-to-day working:        │
              │                             │
              │  Starting work? → [SOP-05]  │
              │  Saving work?  → [SOP-04]   │
              │  New feature?  → [SOP-06]   │
              └──────────────┬──────────────┘
                             │
              ┌──────────────┼──────────────┐
              ▼              ▼              ▼
        Adding a       Repo has         Local copy
        submodule?    submodules?       is broken?
              │              │              │
         [SOP-07]       [SOP-08]       [SOP-09]
       Add Submodule   Clone with     Fresh Re-Clone
                       Submodules
```

---

## 💡 Golden Rules for Beginners

```
┌─────────────────────────────────────────────────────────────────┐
│                    ALWAYS REMEMBER                              │
├─────────────────────────────────────────────────────────────────┤
│  1. Pull before you push                                        │
│     → git pull  (before starting work each day)                │
│                                                                 │
│  2. Commit often, with clear messages                           │
│     → Don't save 3 days of work in one commit                  │
│                                                                 │
│  3. Never work directly on main                                 │
│     → Create a branch for every change                         │
│                                                                 │
│  4. When in doubt, check status                                 │
│     → git status  (run this whenever confused)                 │
│                                                                 │
│  5. Never force push to shared branches                         │
│     → Avoid git push --force on main                           │
│                                                                 │
│  6. Before deleting anything locally, make sure it's on GitHub │
│     → git status  then  git push                               │
└─────────────────────────────────────────────────────────────────┘
```

---

<div align="center">

📖 Back to [README.md](./README.md) | 🧰 Full commands in [GitCheatSheet.md](./GitCheatSheet.md)

Made with ❤️ by [Shahriar Hasib](https://github.com/shahriarhasib)  
⭐ **Star this repo if it helped you!** ⭐

</div>
