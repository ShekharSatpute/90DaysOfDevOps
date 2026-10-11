# Day 15 – Networking Concepts: DNS, IP, Subnets & Ports

## Objective

Understand DNS resolution, IP addressing, CIDR notation, subnetting, and common network ports used in DevOps.

---

# Task 1 – DNS: How Names Become IPs

## 1. What happens when you type `google.com` in a browser?

- When I enter `google.com` in a browser, the system looks for its IP address.
- The DNS resolver checks its cache and queries DNS servers if needed.
- DNS returns an IP address for the domain.
- The browser uses that IP to connect to the server and request the webpage.

## 2. What are Common DNS Record Types? 

- **A** – Maps a domain name to an IPv4 address.
- **AAAA** – Maps a domain name to an IPv6 address.
- **CNAME** – Creates an alias pointing to another domain name.
- **MX** – Specifies which mail server receives emails for a domain.
- **NS** – Identifies the DNS servers responsible for a domain.

## DNS Lookup

```bash
dig google.com
```
![dig output](images/01-dig.png)

- **A Record** – Returns the IPv4 address: `142.250.189.142`
- **TTL (Time To Live)** – `236 seconds`

---

# Task 2 – IP Addressing

## 1. What Is an IPv4 Address? How is it structured?

An IPv4 address is a 32-bit address written as four decimal numbers separated by dots.

Example: `192.168.1.10`

Each number represents 8 bits and ranges from 0 to 255.

## 2. Difference between public and private IPs

| Feature | Public IP | Private IP |
|---|---|---|
| **Purpose** | Used for communication over the internet | Used for communication within a private network |
| **Internet Access** | Routable over the public internet | Not directly routable over the public internet |
| **Assignment** | Usually assigned by an ISP | Usually assigned by a router or DHCP server |
| **Examples** | `8.8.8.8` | `192.168.1.10` |
| **Common Usage** | Public-facing servers, websites, and internet gateways | Home networks, office networks, and internal servers |

## 3. What are the private IP ranges?

| Range | CIDR |
|---|---|
| `10.0.0.0 – 10.255.255.255` | `10.0.0.0/8` |
| `172.16.0.0 – 172.31.255.255` | `172.16.0.0/12` |
| `192.168.0.0 – 192.168.255.255` | `192.168.0.0/16` |

**Common Uses**

- `10.0.0.0 - 10.255.255.255` - Typically used in large enterprise networks.

- `172.16.0.0 - 172.31.255.255` - Commonly used in medium-sized networks.

- `192.168.0.0 - 192.168.255.255` - Commonly used in home and small office networks.

## 4. Run: `ip addr show` — Identify Private and Special IP Addresses

```bash
ip addr show
```

**Observation:** Identify the IP address assigned to your network interface and check whether it belongs to a private range.

---

# Task 3 – CIDR & Subnetting

## 1. What does `/24` mean in `192.168.1.0/24`?

In `192.168.1.0/24`, `/24` means the first 24 bits represent the network portion of the address. The remaining 8 bits are available for host addresses.

- Network: `192.168.1.0`
- IP Range: `192.168.1.0 - 192.168.1.255`
- Total IPs: `256`
- Usable Hosts: `254`

##  How many usable hosts in a `/24`? A `/16`? A `/28`?

| CIDR |  Usable Hosts |
|---|---|
| `/24` |  254 |
| `/16` |65,534 |
| `/28` | 14 |

## 3. Why Do We Subnet?

- Subnetting divides a larger network into smaller networks.
- It helps organize IP addresses, control traffic, and separate systems by function or security requirements.
- In AWS, subnets help organize resources within a VPC and can be designed for different routing and access needs.

## 4. Quick exercise — fill in:

| CIDR | Subnet Mask | Total IPs | Usable Hosts |
|------|------------|------------|-------------|
| /24 | 255.255.255.0 | 256 | 254 |
| /16 | 255.255.0.0 | 65,536 | 65,534 |
| /28 | 255.255.255.240 | 16 | 14 |
---

# Task 4 – Ports: The Doors to Services

## 1. What is a port? Why do we need them?

A port is a number used by TCP or UDP to identify a service or application endpoint on a device. IP addresses identify hosts, while ports help direct traffic to the appropriate service.

## 2. Document these common ports:

| Port | Service | Typical Use |
|---:|---|---|
| 22 | SSH | Remote server access |
| 80 | HTTP | Web traffic |
| 443 | HTTPS | Encrypted web traffic |
| 53 | DNS | Domain name resolution |
| 3306 | MySQL | Database connections |
| 6379 | Redis | In-memory data store |
| 27017 | MongoDB | Database connections |

## Run `ss -tulpn` — match at least 2 listening ports to their services

```bash
ss -tulpn
```
- Port 22 : Service SSH

```bash
sudo ss -tulpn | grep 22
```

Output:

```text
tcp LISTEN 0 4096 0.0.0.0:22
tcp LISTEN 0 4096 [::]:22
```

**Observation:**
- Port `22` is in the **LISTEN** state.
- The service associated with this port is **SSH (sshd)**.
- The output shows SSH is listening on both **IPv4 (`0.0.0.0:22`)** and **IPv6 (`[::]:22`)** addresses.

```bash
nc -zv localhost 22
```

**Output:**

```bash
Connection to localhost (127.0.0.1) 22 port [tcp/ssh] succeeded!
```

---

# Task 5 – Putting It Together

## Scenario 1: Accessing `http://myapp.com:8080`

- DNS resolves `myapp.com` to an IP address.
- The client connects to port `8080` using TCP and sends an HTTP request.
- Routing, firewall rules, and the application's listening state determine whether the request reaches the service.

## Scenario 2. Your app can't reach a database at `10.0.1.50:3306` — what would you check first?

- `ss -tulpn | grep 3306` - Check if MySQL is listening on port 3306.
- `systemctl status mysql` - Verify the MySQL service is running.
- `nc -zv 10.0.1.50 3306` - Test connectivity to the database server.
- `journalctl -u mysql` - Review MySQL logs for errors.

---

# What I Learned

- DNS translates domain names into IP addresses using different record types.
- CIDR notation defines network sizes and helps plan IP addressing.
- Ports identify services, and connectivity depends on routing, firewall rules, and the service listening on the expected port.

---

