Hi, I am Samuel👋.

# Git Mastery: Fundamentals, Undo, Recovery & Debugging Log

A structured repository and comprehensive learning sandbox designed to build, practice, and master both foundational version control and advanced Git recovery/debugging workflows. This project tracks a hands-on journey from local configuration and basic branching to managing complex branch repairs, surgical cherry-picking, and binary search debugging.

## Project Overview

The goal of this project is to develop absolute confidence in the command line using **Git** and **GitHub**. This repository acts as a real-time record of two core phases:
1. **Core Fundamentals**: Establishing robust tracking workflows, parallel branching, conflict resolution, and remote synchronization.
2. **Advanced Recovery & Debugging**: Implementing safety nets to undo local/remote mistakes, restoring "permanently lost" commits, cherry-picking critical hotfixes, and locating bug-introducing commits using binary searches.

---

## Repository Structure

- `learning-log.md` - Technical logs containing foundational lesson summaries, goals, and reflections.
- `undo-practice.md` - A dedicated playground file used to practice resets, reverts, reflogs, cherry-picks, and bisects.
- `README.md` - Complete project documentation, core concept explanations, and command reference guides.

---

## Key Skills Gained & Practised

- **Version Control Mechanics**: Initializing repositories, staging edits, committing structured changes, and visualizing history with custom logs.
- **Advanced Branching & History Manipulation**: Creating local development lines, executing merges, rebasing, and running deep reset and revert mechanisms.
- **Surgical Code Isolation**: Restoring individual commits to clean states and extracting specific change-sets across parallel histories.
- **Automated Bug Hunting**: Implementing systematic search strategies directly into the version history to root out application issues.
- **Command Line Navigation**: Interacting directly with the Shell/Terminal environment and configuring global workspace preferences.

---

## Key Concepts Learned

### 1. Reset vs. Revert
- **Git Reset**: Rewrites history. It moves your branch pointer backward, effectively erasing commits as if they never happened. Used exclusively for local commits that have not yet been pushed to GitHub.
- **Git Revert**: Appends new history. It creates a brand-new commit that does the exact opposite of a targeted bad commit. It is the gold standard for shared or public branches because it keeps the history intact without disrupting your team's local copies.

### 2. The Reflog Safety Net
- **Reflog**: A local-only log that records every movement of `HEAD` (commits, checkouts, merges, resets). Because Git retains deleted commits in its object database for roughly 90 days before garbage collection, Reflog serves as the ultimate "delete-undo" mechanism.

### 3. Cherry-Picking for Hotfixes
- **Cherry-Pick**: The process of applying changes from a single commit elsewhere in your history directly onto your active branch. This allows developers to port critical bug fixes from testing or staging branches directly to production without merging unrelated, incomplete features.

### 4. Git Bisect Binary Search
- **Bisect**: A debugging wizard that uses a binary search algorithm to locate which commit introduced a bug. By declaring a known "good" commit and "bad" commit, Git checks out the middle commits for testing, reducing the search space exponentially.

---

## Lessons Learned

### 1. "Nothing is Ever Truly Lost in Git"
Even after executing a highly destructive `git reset --hard` command that wipes file modifications off the disk, the underlying commit still exists. Knowing how to leverage the repository's internal plumbing means you can recover from almost any local disaster.

### 2. The Importance of Clean Git History
Writing clear, descriptive commit messages and choosing the correct undo technique (reverting pushed work vs. resetting local work) keeps the collaborative commit history readable, logical, and safe for everyone on the development team.

### 3. Merge Conflict Empathy
Merge conflicts are not failures; they are Git safely asking for human guidance. When two branches edit the exact same lines of code, Git pauses rather than guessing, allowing developers to manually inspect and align overlapping features.

---

## Troubleshooting: Errors Faced & How I Fixed Them

### Error 1: Getting Trapped in the Vim Text Editor
- **The Issue**: During merges or reverts, Git automatically opened the command-line editor **Vim** to write commit messages. Unfamiliarity with Vim shortcuts led to being "stuck" in the terminal.
- **The Fix**: 
  1. Escaped Vim by typing `:wq` and pressing `Enter` to write the file and quit.
  2. Configured **nano** as the easier, default global terminal editor for all future Git operations using:
     ```bash
     git config --global core.editor "nano"
     ```

### Error 2: Deleting Valuable Work via an Accidental Hard Reset
- **The Issue**: Executed a `git reset --hard HEAD~1` to undo an experimental commit, only to realize the changes were actually needed. The files completely vanished from the editor.
- **The Fix**: 
  1. Ran `git reflog` to view the full history of the `HEAD` pointer.
  2. Identified the 7-character SHA hash of the "lost" commit before the reset took place.
  3. Created a recovery branch pointing directly at that SHA:
     ```bash
     git branch recover-branch 
     ```
  4. Merged the recovery branch back into `main` to restore the vanished files safely.

### Error 3: Push Rejected by GitHub
- **The Issue**: After performing local history cleanups and recoveries, running `git push` threw a "rejected/non-fast-forward" error because the local branch diverged from GitHub's remote history.
- **The Fix**: Prior to forcing changes or making manual overwrites, ran:
  ```bash
  git pull --rebase
  ```
  This safely pulled down remote updates, replayed the local commits on top of the remote history, and cleared the pathway for a successful, clean `git push`.

---

## Essential Command Reference

### Setup, Config & Tracking
```bash
# Set global identity
git config --global user.name "Your Name"
git config --global user.email "your-email@example.com"

# View status & history
git status
git log --oneline -5
```

### Local Branching & Merges
```bash
# Checkout a new branch
git checkout -b feature-branch

# Merge changes and delete feature branches
git merge feature-branch
git branch -d feature-branch
```

### Resetting & Reverting
```bash
# Soft Reset (retains staged files)
git reset --soft HEAD~1

# Revert (adds a safety inverse commit to history)
git revert HEAD
```

### Advanced Diagnostics
```bash
# Surgical cherry-pick
git cherry-pick 

# Bisect bug-finding wizard
git bisect start
git bisect bad
git bisect good 
# ... test code ...
git bisect reset
```