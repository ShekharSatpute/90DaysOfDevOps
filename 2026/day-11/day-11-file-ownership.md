# Day 11 – File Ownership Challenge (chown & chgrp)

## Objective

Learn how Linux file ownership works and practice changing file owners and groups using `chown` and `chgrp`.

---

## Setup – Users and Groups

The required users and groups were already created during the previous practice.

## Users Created
- tokyo
- berlin
- professor
- nairobi
  
![Users Created](images/2%20Users%20Created.png)

---

## Groups Created
- heist-team
- planners
- vault-team
- tech-team

![Groups Created](images/3%20Groups%20Created.png)

---

## Files & Directories Created

- devops-file.txt
- team-notes.txt
- project-config.yml
- app-logs/
- heist-project/
- heist-project/plans/strategy.conf
- heist-project/vault/gold.txt
- bank-heist/
- bank-heist/access-codes.txt
- bank-heist/blueprints.pdf
- bank-heist/escape-plan.txt

---

# Task 1 – Understanding Ownership

### Check file ownership:

```bash
ls -l
```

![list files](images/1%20list%20files.png)

### Observation

- **Owner** → User who owns the file.
- **Group** → Group associated with the file.
- Ownership controls who can access or manage the file based on permissions.

---

# Task 2 – Basic Chown Operations

### Create File

```bash
touch devops-file.txt
```

### Check Current Owner

```bash
ls -l devops-file.txt
```

### Change Owner to tokyo

```bash
sudo chown tokyo devops-file.txt
```

### Verify

```bash
ls -l devops-file.txt
```

### Change Owner to berlin

```bash
sudo chown berlin devops-file.txt
```

### Verify

```bash
ls -l devops-file.txt
```

![chown Operation](images/4%20chown%20devops%20file.png)

### Observation: 
The file owner was changed first to tokyo and then to berlin.

---

# Task 3 – Basic chgrp Operations

### Create File

```bash
touch team-notes.txt
```

### Check Current Group

```bash
ls -l team-notes.txt
```

### Change Group to heist-team

The heist-team group was already created during setup.

````bash
sudo chgrp heist-team team-notes.txt
````

### Verify

```bash
ls -l team-notes.txt
```

![Basic chgrp Operations](images/5%20team%20notes%20created.png)

### Observation

The group ownership of team-notes.txt was changed to heist-team.

---

# Task 4 – Change Owner and Group Together

Using chown, both owner and group can be changed in one command.

### Create File

```bash
touch project-config.yml
```

### Change Owner and Group

```bash
sudo chown professor:heist-team project-config.yml
```

### Verify

```bash
ls -l project-config.yml
```

### Create Directory

```bash
mkdir app-logs
```

### Change Owner and Group

```bash
sudo chown berlin:heist-team app-logs
```

### Verify

```bash
ls -ld app-logs
```

![owner grp](images/6%20project%20config%20yaml.png)

### Observation

The owner and group were updated together using chown owner:group.


---

# Task 5 – Recursive Ownership

### Create Directory Structure

```bash
mkdir -p heist-project/vault
mkdir -p heist-project/plans

touch heist-project/vault/gold.txt
touch heist-project/plans/strategy.conf
```

### Change Ownership Recursively

The planners group was already created during setup.

```bash
sudo chown -R professor:planners heist-project
```

### Verify

```bash
ls -lR heist-project
```
![Recursive Ownership](images/7%20heist%20project.png)

### Observation

Ownership was applied recursively to the heist-project directory, its subdirectories, and files.

- Owner → professor
- Group → planners

---

# Task 6: Practice Challenge

1. Create users: `tokyo`, `berlin`, `nairobi` (if not already created)
2. Create groups: `vault-team`, `tech-team`

## Create directory: 

```bash
mkdir bank-heist
```

## Create files:

```bash
touch bank-heist/access-codes.txt
touch bank-heist/blueprints.pdf
touch bank-heist/escape-plan.txt
```

## Set Ownership

### Access Codes

```bash
sudo chown tokyo:vault-team bank-heist/access-codes.txt
```

### Blueprints
```bash
sudo chown berlin:tech-team bank-heist/blueprints.pdf
```

### Escape Plan

```bash
sudo chown nairobi:vault-team bank-heist/escape-plan.txt
```

### Verify

```bash
ls -l bank-heist
```

![Practice Challenge](images/8%20bank%20heist%20dir.png)

---


## Commands Used

- View ownership : `ls -l filename`
- Change owner only : `sudo chown newowner filename`
- Change group only : `sudo chgrp newgroup filename`
- Change both owner and group : `sudo chown owner:group filename`
- Recursive change (directories) : `sudo chown -R owner:group directory/`
- Change only group with chown : `sudo chown :groupname filename`

---

## What I Learned

- Linux files have an owner and a group.
- `chown` changes file or directory ownership.
- `chgrp` changes the group ownership.
- `chown owner:group` changes both owner and group.
- `chown -R` applies ownership changes recursively.
- `ls -l` is used to verify ownership and permissions.
- Proper ownership is important for shared directories, applications, logs, and CI/CD environments.