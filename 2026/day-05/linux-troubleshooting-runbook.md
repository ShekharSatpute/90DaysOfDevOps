# Linux Troubleshooting Runbook

## Target Service

**Service:** Nginx (`nginx.service`)

---

# 1. Environment Basics

### 1.1 Check Kernel Information

### Command

```bash
uname -a
```

### Output

```text
Linux ip-172-31-9-236 7.0.0-1006-aws #6-Ubuntu SMP PREEMPT Thu Oct 01 16:04:34 UTC 2026 x86_64 GNU/Linux
```

### Observation 
The command shows the Linux kernel version, system architecture, and AWS kernel build information.

---

### 1.2 Check Operating System

### Command

```bash
cat /etc/os-release
```

### Output

```text
PRETTY_NAME="Ubuntu 26.04 LTS"
NAME="Ubuntu"
VERSION_ID="26.04"
VERSION="26.04 LTS (Resolute Raccoon)"
```

### Observation
The system is running Ubuntu 26.04 LTS.

---

# 2. Filesystem Sanity

### 2.1 Create a Practice Directory

### Command

```bash
mkdir /tmp/runbook-demo
```

### Output

```text
Directory created successfully.
```

### Observation
Created a temporary directory successfully for the troubleshooting practice.

---

### 2.2 Copy and Verify a File

### Command

```bash
cp /etc/hosts /tmp/runbook-demo/hosts-copy
ls -l /tmp/runbook-demo
```

### Output

```text
total 4
-rw-r--r-- 1 ubuntu ubuntu 226 Oct 1 16:10 hosts-copy
```

### Observation

The /etc/hosts file was copied successfully and verified using ls -l.

---

# 3. CPU & Memory Snapshot

### 3.1 Monitor System Resources

### Command

```bash
top
```
### Observation

Used `top` to check CPU usage, memory usage, and active processes.

---

### 3.2 Find High CPU Processes
### Command

 ```
 ps aux --sort=-%cpu | head`
```
### Observation:
No abnormal CPU-consuming process was observed during the check.

--- 

### 3.3 Find High Memory Processes
### Command

 ```
 ps aux --sort=-%mem | head
```
### Observation
Memory usage was within the observed normal range.

---

### 3.4 Check Memory Usage

### Command

```bash
free -h
```

### Output

```text
               total        used        free      shared  buff/cache   available
Mem:           908Mi       312Mi       172Mi       2.7Mi       334Mi       607Mi
Swap:             0B          0B          0B
```

### Observation
The system had available memory and no swap usage was reported.


---

# 4. Disk & I/O Snapshot

### 4.1 Check Disk Space

### Command

```bash
df -h
```

### Output

```text
Filesystem       Size  Used Avail Use% Mounted on
/dev/root        6.7G  2.1G  4.6G  31% /

```

### Observation
The root filesystem was using 31% of its available space, with sufficient free space remaining.

---

# 5. Network Snapshot

### 5.1 Check Listening Ports

### Command

```bash
ss -tulpn
```

### Output

```text
Netid       State        Recv-Q       Send-Q                    Local Address:Port               Peer Address:Port
udp         UNCONN       0            0                             127.0.0.54:53                     0.0.0.0:*
udp         UNCONN       0            0                         127.0.0.53%lo:53                      0.0.0.0:*
udp         UNCONN       0            0                                 [::1]:323                        [::]:*
tcp         LISTEN       0            4096                      127.0.0.53%lo:53                      0.0.0.0:*
tcp         LISTEN       0            4096                         127.0.0.54:53                      0.0.0.0:*
tcp         LISTEN       0            4096                               [::]:22                         [::]:*
```

### Observation
Port 22 was listening for TCP connections, and local DNS-related ports were also present.

---

### 5.2 Test Nginx Response

### Command

```bash
curl -I http://localhost
```

### Output

```text
HTTP/1.1 200 OK
  Server: nginx/1.28.3
```

### Observation
Nginx returned HTTP 200 OK, confirming that the local web server was responding successfully.


---

# 6. Logs Reviewed

### 6.1 View nginx Logs

### Command

```bash
journalctl -u nginx
```

### Output

```text
journalctl -u nginx
Oct 01 08:58:34 DESKTOP-6LC1IS9 systemd[1]: Stopping nginx.service - A high performance web server and a reverse proxy >
Oct 01 08:58:34 DESKTOP-6LC1IS9 systemd[1]: nginx.service: Deactivated successfully.
Oct 01 08:58:34 DESKTOP-6LC1IS9 systemd[1]: Stopped nginx.service - A high performance web server and a reverse proxy s>
-- Boot 2c668914c7394d18adc10aeb865fea27 --
Oct 01 09:05:30 DESKTOP-6LC1IS9 systemd[1]: Starting nginx.service - A high performance web server and a reverse proxy >
Oct 01 09:05:30 DESKTOP-6LC1IS9 systemd[1]: Started nginx.service - A high performance web server and a reverse proxy s>
-- Boot 47094ad4cd1843afb65f78cf34622376 --
Oct 01 10:51:04 DESKTOP-6LC1IS9 systemd[1]: Starting nginx.service - A high performance web server and a reverse proxy >
lines 1-12/12 (END)
```

### Observation
The access log showed successful HTTP requests with status 200 and some requests returning 404 for missing resources.


---

### 6.2  Check Nginx Access Logs

### Command

```bash
tail -n 50 /var/log/nginx/access.log
```

### Output

```text
::1 - - [10/Sep/2026:14:01:52 +0000] "GET / HTTP/1.1" 200 3522 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/152.0.0.0 Safari/537.36"
::1 - - [10/Sep/2026:14:02:08 +0000] "GET / HTTP/1.1" 200 10671 "-" "curl/8.5.0"
::1 - - [10/Sep/2026:14:03:35 +0000] "GET /icons/ubuntu-logo.png HTTP/1.1" 404 196 "http://localhost/" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/152.0.0.0 Safari/537.36"
```

### Observation
The access log showed successful HTTP requests with status 200 and some requests returning 404 for missing resources.

---

# 7. Configuration Validation

### Command 
```
sudo nginx -t
```
### Output:
  ```text
  nginx: configuration file syntax is ok
  nginx: configuration file test is successful
  ```

### Observation:
 The Nginx configuration syntax check was successful.

---
# Quick Findings
- The system is running Ubuntu 26.04 LTS.
- CPU and memory usage appeared normal during the checks.
- Nginx was responding successfully with HTTP 200 OK.
- Nginx configuration validation was successful.
- Nginx logs showed normal service activity and HTTP requests.
- Some requested resources returned 404, indicating that those resources were not found.

---

# Troubleshooting Flow
```
Check system information
        ↓
Check CPU & Memory
        ↓
Check Disk Space
        ↓
Check Listening Ports
        ↓
Test Nginx Response
        ↓
Check Nginx Service Logs
        ↓
Check Access Logs
        ↓
Validate Nginx Configuration
```
---

# If the Issue Gets Worse
If Nginx stops responding, I would:
1. Check the service status with systemctl status nginx.
2. Review recent logs using journalctl -u nginx.
3. Check listening ports with ss -tulpn.
4. Test the service using curl.
5. Validate the configuration using sudo nginx -t.
6. Check CPU, memory, and disk usage for system-level issues.


---
