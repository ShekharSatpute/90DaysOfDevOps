# Git Commands Cheat Sheet

## 1. Git Setup & Configuration

| Command | Purpose | Example |
|---|---|---|
| `git --version` | Check Git version | `git --version` |
| `git config --global user.name` | Set username | `git config --global user.name "Your Name"` |
| `git config --global user.email` | Set email | `git config --global user.email "your@email.com"` |
| `git config --global --list` | View configuration | `git config --global --list` |

## 2. Repository Management

| Command | Purpose | Example |
|---|---|---|
| `git init` | Initialize repository | `git init` |
| `git clone <url>` | Clone repository | `git clone <url>` |

## 3. Basic Git Workflow

| Command | Purpose | Example |
|---|---|---|
| `git status` | Check working tree status | `git status` |
| `git add <file>` | Stage a file | `git add demo.txt` |
| `git add .` | Stage all changes | `git add .` |
| `git commit -m "message"` | Save changes | `git commit -m "Initial commit"` |

## 4. Viewing Changes & History

| Command | Purpose | Example |
|---|---|---|
| `git diff` | View unstaged changes | `git diff` |
| `git diff --staged` | View staged changes | `git diff --staged` |
| `git log` | View commit history | `git log` |
| `git log --oneline` | Compact commit history | `git log --oneline` |
| `git show HEAD` | View latest commit details | `git show HEAD` |

## 5. Branching & Merging

| Command | Purpose | Example |
|---|---|---|
| `git branch` | List branches | `git branch` |
| `git branch feature` | Create branch | `git branch feature` |
| `git switch feature` | Switch branch | `git switch feature` |
| `git switch -c feature` | Create and switch branch | `git switch -c feature` |
| `git merge feature` | Merge branch | `git merge feature` |

## 6. Remote Repository (GitHub)

| Command | Purpose | Example |
|---|---|---|
| `git remote -v` | View remote repositories | `git remote -v` |
| `git push origin main` | Push changes | `git push origin main` |
| `git pull origin main` | Pull latest changes | `git pull origin main` |
| `git fetch` | Download remote changes | `git fetch` |

## 7. Undo & Stash Changes

| Command | Purpose | Example |
|---|---|---|
| `git restore <file>` | Discard unstaged changes | `git restore demo.txt` |
| `git restore --staged <file>` | Unstage a file | `git restore --staged demo.txt` |
| `git revert <commit-id>` | Undo a commit safely | `git revert abc123` |
| `git stash` | Temporarily save changes | `git stash` |
| `git stash pop` | Restore stashed changes | `git stash pop` |

## 8. Tags

| Command | Purpose | Example |
|---|---|---|
| `git tag` | List tags | `git tag` |
| `git tag v1.0` | Create a tag | `git tag v1.0` |