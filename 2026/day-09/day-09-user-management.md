# Day 09 - Linux User & Group Management Challenge

## Objective

Practice Linux user and group management by creating users, assigning groups, configuring shared directories, and verifying permissions.

---


# Task 1: Create Users

Created the following users:

- tokyo
- berlin
- professor

### Comands

```bash
sudo useradd -m tokyo
sudo useradd -m berlin
sudo useradd -m professor
```

### Verify Users

```bash
cat /etc/passwd | grep -E "tokyo|berlin|professor"
```

### Screenshot

![Users Created](images/1.%20Users%20Created.png)


### Verify Home Directories

```bash
ls -l /home
```

### Observation

- Successfully created three users.
- Home directories were created automatically.

---

# Task 2: Create Groups

Created the following groups:

- developers
- admins

### Comands 

```bash
sudo groupadd developers
sudo groupadd admins
```
### Verify Groups

```bash
cat /etc/group | grep -E "developers|admins"
```

### Screenshot

![Groups Created](images/2.%20Groups%20Created.png)

### Observation
- Both groups were created successfully.

---


# Task 3: Assign Users to Groups

### Commands

```bash
sudo usermod -aG developers tokyo

sudo usermod -aG developers,admins berlin

sudo usermod -aG admins professor
```

### Group Memberships

| Group | Members |
|---------|---------|
| developers | tokyo, berlin |
| admins | berlin, professor |


### Verify Groups

```bash
cat /etc/group | tail
```

### Screenshot

![Group Assignment](images/3.%20Group%20Assignment.png)

### Observation

- Tokyo belongs to **developers**
- Berlin belongs to **developers** and **admins**
- Professor belongs to **admins**

---

# Task 4: Create Shared Directory

### Create Directory

```bash
sudo mkdir -p /opt/dev-project
```

### Change Group Owner

```bash
sudo chgrp developers /opt/dev-project
```

### Set Permissions

```bash
sudo chmod 775 /opt/dev-project
```

### Verify Permissions

```bash
ls -ld /opt/dev-project
```

### Screenshot

![Directory Created](images/4.%20Directory%20Created.png)

### Observation

- Created a shared directory owned by the developers group with group write access.

---

# Task 5: Verify Home Directories

### Command

```bash
ls /home
```

### Screenshot

![Home Directories](images/5.%20Home%20Directories.png)

### Observation
- Verified that the created users have their respective home directories.

---

# Task 6: Test Shared Directory Access

As **tokyo**

```bash
sudo -u tokyo touch /opt/dev-project/tokyo.txt
```

As **berlin**

```bash
sudo -u berlin touch /opt/dev-project/berlin.txt
```

### Observation
- Both users were able to create files inside the shared developers directory.

---

# Task 7: Create Team Workspace

Create:

- User: nairobi
- Group: project-team
- Workspace: /opt/team-workspace

### Create User

```bash
sudo useradd -m nairobi
```

### Set Password

```bash
sudo passwd nairobi
```

### Create Group

```bash
sudo groupadd project-team
```

### Add Users

```bash
sudo usermod -aG project-team nairobi

sudo usermod -aG project-team tokyo
```

### Create Directory

```bash
sudo mkdir -p /opt/team-workspace
```

### Change Group Owner

```bash
sudo chgrp project-team /opt/team-workspace
```

### Set Permissions

```bash
sudo chmod 775 /opt/team-workspace
```

### Observation

- Created a separate workspace for the project-team group and gave the group permission to work inside the directory.

---

# Commands Used

| Command | Purpose |
|----------|----------|
| useradd -m username | Create user |
| passwd username | Set or change a user password |
| groupadd groupname | Create a new group |
| usermod -s /bin/bash username | Change shell |
| gpasswd -M user1,user2 groupname | Add user to group |
| mkdir -p directory | Create directory |
| chgrp group directory | Change group ownership |
| cat /etc/passwd | Verify users |
| cat /etc/group | Verify groups |

---

# Learning Outcome

- Learned how to create and manage Linux users.
- Practiced creating groups and assigning users to them.
- Understood how group ownership controls shared access.
- Practiced using chmod to manage directory permissions.
- Learned how to create shared directories for teams.
- Verified user home directories and group memberships.
- Understood how Linux users, groups, ownership, and permissions work together.
