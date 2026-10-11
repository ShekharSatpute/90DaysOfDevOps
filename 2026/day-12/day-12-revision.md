# Day 12 Revision (Days 01–11)

During the first 11 days of my #90DaysOfDevOps journey, I focused on building Linux fundamentals through hands-on practice. I worked with processes, services, file operations, permissions, users, groups, and ownership.

---

## 1. Processes & Services

When my system slows down, I can use these commands to investigate processes, check service status, and review logs.

- `ps aux` – Lists running processes and their resource usage.
- `top` – Monitors processes and system resource usage in real time.
- `systemctl status nginx` – Checks whether the Nginx service is active or has failed.
- `journalctl -u nginx -n 50` – Displays the latest 50 log entries for Nginx.
- `df -h` – Shows filesystem disk space usage.

These commands help me investigate service failures, resource usage, and common Linux issues.

---

## 2. File Operations & Permissions

I practiced creating files, reading content, changing permissions, and managing ownership.

- `touch devops.txt` – Creates an empty file.
- `echo "Practice" >> notes.txt` – Appends content to a file.
- `cat notes.txt` – Displays file content.
- `chmod 640 notes.txt` – Gives the owner read/write access, the group read access, and others no access.
- `ls -l` – Displays file permissions and ownership.
- `chown` – Changes file ownership.
- `chgrp` – Changes file group ownership.
- `chown -R` – Applies ownership changes recursively.

---

## 3. Important Commands for Troubleshooting

| Command | Purpose |
|---|---|
| `ps aux` | List running processes |
| `top` | Monitor CPU and memory usage |
| `systemctl status nginx` | Check Nginx service status |
| `journalctl -u nginx -n 50` | View recent Nginx logs |
| `df -h` | Check disk space |
| `free -h` | Check memory usage |
| `cat /var/log/nginx/error.log` | Read Nginx error logs |

The commands I use depend on the problem. For example, I can check memory with `free -h`, disk space with `df -h`, and service errors with `journalctl`.

---

## 4. Mini Self-Check

### 1. Which three commands save me the most time right now, and why?

- `ps aux` – Helps identify running processes.
- `systemctl status nginx` – Checks the service state.
- `journalctl -u nginx -n 50` – Helps investigate service errors through logs.

### 2. How do I check if a service is healthy?

```bash
systemctl status nginx
journalctl -u nginx -n 50
curl -I http://localhost
```

These commands check the service state, recent logs, and the local HTTP response. Additional application-specific checks may be needed to confirm complete health.

### 3. How do I safely change ownership and permissions?

Check the current state, make the required change, and verify the result.

Example:

```bash
ls -l notes.txt
chmod 640 notes.txt
ls -l notes.txt
```

### 4. What will I focus on improving in the next three days?

- Strengthen Linux networking fundamentals and understand how systems communicate.
- Learn Linux storage basics, including partitions, mount points, and LVM.
- Continue practicing user/group management, permissions, and ownership.
- Improve Git and GitHub workflows through hands-on practice.
- Revise AWS fundamentals and perform more EC2 exercises.
- Practice Linux troubleshooting and log analysis.

---

## 5. Key Takeaways

- `ps` and `top` help investigate processes and resource usage.
- `systemctl` checks service status, while `journalctl` helps investigate service issues.
- File permissions control read, write, and execute access.
- `chown` and `chgrp` manage file ownership.
- Verifying changes helps catch mistakes early.
- Regular practice improves confidence with Linux administration commands.