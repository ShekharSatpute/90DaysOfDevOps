# Day 22 – Introduction to Git: Your First Repository

## Objective

Understand Git basics, create a local repository, practice staging and committing changes, and build a personal Git commands reference.

---

# Task 1 – Install and Configure Git
1. Verify Git is installed on your machine

2. Set up your Git identity — name and email

3. Verify your configuration

## 1. Verify Git Installation

```bash
git --version
```

This displays the installed Git version.

## 2. Configure Git Identity

```bash
git config --global user.name "Your Name"
git config --global user.email "your-email@example.com"
```

Replace these values with your name and email.

## 3. Verify Configuration

```bash
git config --global --list
```

This displays your global Git configuration.

---

# Task 2 – Create Your Git Project

## 1. Create a Project Directory

```bash
mkdir devops-git-practice
cd devops-git-practice
```

## 2. Initialize Git

```bash
git init
```

This initializes a new Git repository in the current directory.

## 3. Check Repository Status

```bash
git status
```

Initially, Git reports that there are no commits yet.

## 4. Explore the `.git` Directory

```bash
ls -la .git
```

The `.git` directory stores repository information, configuration, objects, references, and commit history.

---

# Task 3 – Create Git Commands Reference

1. Create a file called `git-commands.md` inside the repository

2. Add the Git commands you've used so far, organized by category:

   - Setup & Config
   - Basic Workflow
   - Viewing Changes

3. For each command, write:

   - What it does (1 line)
   - An example of how to use it

---

# Task 4 – Stage and Commit

## 1. Check Status

```bash
git status
```

## 2. Stage the File

```bash
git add git-commands.md
```

## 3. Check Staged Changes

```bash
git diff --staged
```

## 4. Commit Changes

```bash
git commit -m "Add Git commands reference"
```

## 5. View Commit History

```bash
git log
```

A commit saves the staged changes into the repository history.

---

# Task 5 – Make More Changes and Build History

1. Edit `git-commands.md` — add more commands as you discover them

2. Check what changed since your last commit

3. Stage and commit again with a different, descriptive message

4. Repeat this process at least 3 times so you have multiple commits in your history

5. View the full history in a compact format

```bash
git log --oneline
```

**Output:**

```text
77b91bd Added merge command
8dcfc2e Added checkout command
2d5dd7f Added branch commands
45f52c9 Added git commands reference
```
---

# Task 6 – Understand the Git Workflow

### 1. What is the difference between `git add` and `git commit`?

- `git add` moves selected changes into the staging area.
- `git commit` saves staged changes into the repository history with a commit message.

**Example:**
```bash
git add git-commands.md
git commit -m "update git commands"
```

### 2. What does the staging area do?

The staging area allows me to select which changes should be included in the next commit. It gives me control over what I save instead of committing every change in the working directory.

### 3. What information does `git log` show?

- `git log` shows commit history.
- It displays commit ID, author, date and commit message.

### 4. What is the `.git/` folder?

- `.git/` stores repository history, branches,commits, tags and configuration files.
- If i delete it , Git tracking and commit history are lost.

### 5. Difference Between Working Directory, Staging Area, and Repository

| Area | Meaning |
|---|---|
| Working Directory | Where I create and edit files |
| Staging Area | Where I prepare changes for the next commit |
| Repository | Stores commits, branches and complete project history. |

### Git Workflow

```text
Working Directory
       |
       | git add
       v
Staging Area
       |
       | git commit
       v
Git Repository
```

---

# What I Learned

1. Git tracks changes and maintains the history of a project through commits.
2. The staging area helps select exactly which changes should be included in a commit.
3. Meaningful commit messages and a clean commit history make project changes easier to understand and maintain.

---
