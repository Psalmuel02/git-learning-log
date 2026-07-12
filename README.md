Hi, I am Samuel👋.

# Git Learning Log & Fundamentals Practice

A structured repository and learning sandbox designed to build and practice foundational version control skills. This project follows a hands-on journey from local configuration to resolving complex branching workflows and publishing code on GitHub.

## Project Overview

The goal of this project is to master **Git** and **GitHub** workflows by maintaining a real-time learning log. Throughout this repository's history, I practiced local development tracking, parallel branching, conflict resolution, and remote synchronization.

---

## Repository Structure

- `learning-log.md` - The primary markdown log containing lesson summaries, goals, and reflections.
- `README.md` - Documentation describing the project, architecture, and commands used.

---

## Key Skills & Concepts Covered

1. **Git Configuration**:
   - Initialising global user identity (name, email) for proper commit authorship tracking.
2. **Local Version Control Workflow**:
   - Initialising a local repository (`git init`).
   - Tracking files using staging (`git add`) and commits (`git commit`).
3. **Branching & Parallel Changes**:
   - Developing features isolated from the main line using `git branch` and `git checkout`.
   - Managing parallel workstreams simultaneously.
4. **Merge Conflict Resolution**:
   - Simulating conflicting changes across branches.
   - Diagnosing, locating, and resolving merge conflicts manually.
5. **GitHub Integration**:
   - Connecting local repositories to remote servers (`git remote add`).
   - Pushing local history to public GitHub repositories (`git push`).

---

## Essential Commands Practised

Here is a quick reference guide of the commands used in this project:

### Repository Initialization & Identity Setup
```bash
# Configure identity globally (run in Git Bash or integrated terminal)
git config --global user.name "Your Name"
git config --global user.email "your-email@example.com"

# Check global configuration
git config --global --list

# Initialise a new Git repository
git init
```

### Staging & Committing
```bash
# Check repository status
git status

# Stage a file for commit
git add learning-log.md

# Commit staged changes with a descriptive message
git commit -m "Initial commit: Add learning-log.md"

# View commit history
git log --oneline
```

### Branching & Merging
```bash
# Create and switch to a new branch
git checkout -b feature-branch

# List all local branches
git branch

# Merge a branch into the current active branch
git merge feature-branch

# Delete a branch once merged
git branch -d feature-branch
```

### Working with Remote Repositories
```bash
# Add a remote GitHub repository
git remote add origin https://github.com/your-username/git-learning-log.git

# Push changes to GitHub (setting upstream tracking)
git push -u origin main
```

---

## What I Learned: Merging & Conflicts

One of the most valuable lessons in this project was understanding how Git handles **merge conflicts**. 

- **The Cause**: Occurs when two separate branches edit the same line(s) of a file, and Git does not know which version to keep.
- **The Solution**: 
  1. Run `git merge` and observe the conflict warning.
  2. Open the affected file (e.g., `learning-log.md`) and locate conflict markers: `<<<<<<<`, `=======`, and `>>>>>>>`.
  3. Manually select the desired content (or combine both).
  4. Remove the conflict markers and save the file.
  5. Stage and commit the resolved changes using `git add` and `git commit` to finalise the merge.


