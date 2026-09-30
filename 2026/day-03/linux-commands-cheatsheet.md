# Linux Commands Cheat Sheet

## 1. Process Management

| Command         | Usage                           |
| --------------- | ------------------------------- |
| `ps aux`        | List running processes          |
| `top`           | Monitor CPU and memory usage    |
| `htop`          | Interactive process monitor     |
| `pgrep name`    | Find a process by name          |
| `kill <PID>`    | Stop a process                  |
| `kill -9 <PID>` | Force stop a process            |
|`pkill name`     | Kill by process name            |   
|`pstree`         | Shows process hireachy          |

---

## 2. File System

| Command               | Usage                                  |
| --------------------- | -------------------------------------- |
| `pwd`                 | Show current directory                 |
| `ls -la`              | List all files, including hidden files |
| `cd <dir>`            | Change directory                       |
| `mkdir <dir>`         | Create a directory                     |
| `touch file`          | Create an empty file                   |
| `cp file1 file2`      | Copy a file                            |
| `mv file1 file2`      | Move or rename a file                  |
| `rm file`             | Remove a file                          |
| `cat file`            |   Display file contents                |
| `head file`           | Display the first 10 lines of a file.  |
| `tail file`           | Display the last 10 lines of a file.   |
| `grep "<text>" <file>` | Search for text inside a file.        |
| `find <path> -name "<file>"` | Search for files by name.       |
| `df -h`               | Check disk space                       |
| `du -sh <dir>`        | Display the size of a directory        |
| `free -h`             | Display amount of free and used memory in the system |


---

## 3. Logs & Services

| Command                       | Usage                               |
| ----------------------------- | ----------------------------------- |
| `systemctl status <service>`  | Check service status                |
| `systemctl start <service>`   | Start a service                     |
| `systemctl stop <service>`    | Stop a service                      |
| `systemctl restart <service>` | Restart a service                   |
| `systemctl enable <service>`  | Start service automatically at boot |
| `journalctl -u <service>`     | View service logs                   |
| `journalctl -f`               | Follow live system logs             |

--- 


## 4. Networking

| Command                       | Usage                     |
| ----------------------------- | ------------------------- |
| `ping google.com`             | Test network connectivity |
| `ip addr`                     | Show IP addresses         |
| `ss -tuln`                    | Check listening ports     |
| `dig example.com`             | Check DNS information     |
| `curl -I https://example.com` | Check HTTP response       |
| `hostnamectl`                 | Display hostname and OS information|

---


