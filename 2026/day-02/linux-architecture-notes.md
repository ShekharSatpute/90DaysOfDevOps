# Linux Architecture, Processes & systemd

## Linux Architecture

Linux can be divided into three main parts:

* **Hardware**: Physical components such as CPU, RAM, Disk and Network devices.
* **Kernel:** It is the core component of Linux that manages hardware, memory, processes and system resources.
* **User Space**: Area where users and applications run.
* **Shell**: Command-line interface used to communicate with the kernel.
* **systemd**: First process (PID 1) responsible for managing services and system startup.

---

## Processes

A **process** is a running instance of a program. Each process has a unique **PID**.

Examples: nginx, sshd, docker

### Process States

* **Running (R):** Process is currently executing or is ready to execute.
* **Sleeping (S):** Process is waiting for an event or resource.
* **Stopped (T):** Process execution is paused,usually by a user or debugger.
* **Zombie (Z):** Process has finished but its parent has not collected its exit status.

---

## systemd

systemd is the default init system in most Linux distributions.

### Responsibilities
- Boots the system
- Starts and stops services
- Restarts failed services
- Handles dependencies
- Manages logs (journalctl)

### Why it matters for DevOps
- Restart crashed applications
- Enable services at boot
- Check service status
- Troubleshoot production servers quickly

---

## 5 Commands I Use Daily

| Command      | Purpose                   |
| ------------ | ------------------------- |
| `ps`         | Check running processes   |
| `top`        | Monitor CPU and memory    |
| `systemctl`  | Manage services           |
| `df-h`       | Check disk usage          |
| `free -h`    | Check memoru usage.       |

---

# Key Takeaways

- Kernel controls hardware and system resources.
- User Space is where applications run.
- systemd manages services and system startup.
- Every running program is a process with a unique PID.
- Knowing process states and systemd helps in troubleshooting Linux servers.