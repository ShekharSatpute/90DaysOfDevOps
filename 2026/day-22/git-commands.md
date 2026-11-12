# Git Commands Cheat Sheet

## 1. Git Setup & Configuration

| Command | Purpose | Example |
|---|---|---|
| `git --version` | Check Git version | `git --version` |
| `git config --global user.name "Your Name"` | Set username | `git config --global user.name "John"` |
| `git config --global user.email "your@email.com"` | Set email | `git config --global user.email "john@example.com"` |
| `git config --global --list` | View global configuration | `git config --global --list` |

## 2. Repository Management

| Command | Purpose | Example |
|---|---|---|
| `git init` | Initialize a new repository | `git init` |
| `git clone <url>` | Clone an existing repository | `git clone https://github.com/user/repo.git` |

## 3. Basic Git Workflow

| Command | Purpose | Example |
|---|---|---|
| `git status` | Check working tree status | `git status` |
| `git add <file>` | Stage a specific file | `git add demo.txt` |
| `git add .` | Stage changes in the current directory | `git add .` |
| `git commit -m "message"` | Commit staged changes | `git commit -m "Initial commit"` |

## 4. Viewing Changes & Commit History

| Command | Purpose | Example |
|---|---|---|
| `git diff` | View unstaged changes | `git diff` |
| `git diff --staged` | View staged changes | `git diff --staged` |
| `git log` | View commit history | `git log` |
| `git log --oneline` | View compact commit history | `git log --oneline` |
| `git log --oneline --graph --all` | Visualize branch history | `git log --oneline --graph --all` |
| `git show <commit>` | Display commit details | `git show HEAD` |

## 5. Branching & Switching

| Command | Purpose | Example |
|---|---|---|
| `git branch` | List local branches | `git branch` |
| `git branch -a` | List local and remote-tracking branches | `git branch -a` |
| `git branch <name>` | Create a new branch | `git branch feature` |
| `git switch <branch>` | Switch to another branch | `git switch feature` |
| `git switch -c <branch>` | Create and switch to a new branch | `git switch -c feature` |
| `git branch -d <branch>` | Delete a merged branch | `git branch -d feature` |

## 6. Remote Repository (GitHub)

| Command | Purpose | Example |
|---|---|---|
| `git remote -v` | View configured remote repositories | `git remote -v` |
| `git remote add <name> <url>` | Add a remote repository | `git remote add origin https://github.com/user/repo.git` |
| `git fetch` | Download remote updates without integrating them | `git fetch` |
| `git pull <remote> <branch>` | Fetch and integrate remote changes | `git pull origin main` |
| `git push <remote> <branch>` | Upload local commits to a remote | `git push origin main` |

## 7. Merge & Rebase

| Command | Purpose | Example |
|---|---|---|
| `git merge <branch>` | Merge another branch into the current branch | `git merge feature-login` |
| `git merge --no-ff <branch>` | Create a merge commit even when fast-forward is possible | `git merge --no-ff feature-settings` |
| `git merge --squash <branch>` | Combine another branch's changes into the staging area | `git merge --squash feature-profile` |
| `git rebase <branch>` | Replay current branch commits on top of another branch | `git rebase main` |

## 8. Stash (Temporarily Save Changes)

| Command | Purpose | Example |
|---|---|---|
| `git stash` | Temporarily save tracked-file changes | `git stash` |
| `git stash push -m "message"` | Save changes with a description | `git stash push -m "Work in progress"` |
| `git stash list` | List saved stashes | `git stash list` |
| `git stash apply` | Apply the latest stash without removing it | `git stash apply` |
| `git stash apply stash@{0}` | Apply a specific stash | `git stash apply stash@{0}` |
| `git stash pop` | Apply and remove a stash if successful | `git stash pop` |
| `git stash drop stash@{0}` | Remove a specific stash | `git stash drop stash@{0}` |
| `git stash clear` | Remove all stash entries | `git stash clear` |

## 9. Cherry-Pick

| Command | Purpose | Example |
|---|---|---|
| `git cherry-pick <commit>` | Apply a specific commit to the current branch | `git cherry-pick abc1234` |

## 10. Undo Changes (Restore)

| Command | Purpose | Example |
|---|---|---|
| `git restore <file>` | Discard unstaged changes in a file | `git restore demo.txt` |
| `git restore --staged <file>` | Unstage a file while keeping its changes | `git restore --staged demo.txt` |

## 11. Reset & Revert

| Command | Purpose | Example |
|---|---|---|
| `git reset --soft HEAD~1` | Undo the latest commit but keep changes staged | `git reset --soft HEAD~1` |
| `git reset --mixed HEAD~1` | Undo the latest commit and keep changes unstaged | `git reset --mixed HEAD~1` |
| `git reset --hard HEAD~1` | Undo the latest commit and discard tracked changes from the index and working tree | `git reset --hard HEAD~1` |
| `git revert <commit>` | Create a new commit that reverses an earlier commit | `git revert abc1234` |
| `git reflog` | View recent movements of HEAD and branch references | `git reflog` |

## 12. Tags

| Command | Purpose | Example |
|---|---|---|
| `git tag` | List existing tags | `git tag` |
| `git tag <name>` | Create a lightweight tag | `git tag v1.0` |

---

## Important Notes

- **Working directory:** Where you modify files.
- **Staging area:** Where you prepare changes before committing.
- **Repository:** Where Git stores commits and project history.
- **Fetch vs Pull:** `fetch` downloads remote updates; `pull` fetches and integrates them.
- **Merge vs Rebase:** Merge combines branch histories; rebase replays commits on a new base.
- **Reset vs Revert:** Reset moves a branch reference; revert creates a new commit that reverses changes.
- **Stash:** Useful for temporarily saving work without committing it.

**Warning:** `git reset --hard` can permanently discard uncommitted tracked-file changes. Avoid rewriting shared branch history without coordinating with your team.