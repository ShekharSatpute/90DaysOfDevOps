# Day 08 – Cloud Server Setup: Docker, Nginx & Web Deployment

## Objective

Deploy a Linux server on AWS, connect to it using SSH, install and configure Nginx, make the web server accessible over the internet, and collect Nginx logs.

---


# Part 1 – Launch Cloud Instance & SSH Access

## Connect to the Server

### Command

```bash
ssh -i "devops.pem" ubuntu@ec2-13-233-163-150.ap-south-1.compute.amazonaws.com
```

Successfully connected to the EC2 instance using SSH.

![login SSH](Images/login%20SSH.png)

---

# Part 2 – Update the Server

## Update Package List

```bash
sudo apt update
```
Updated package information from Ubuntu repositories.

---

## Upgrade Installed Packages

```bash
sudo apt upgrade -y
```

Installed the available package updates.

---

# Part 3 – Install Nginx

## Install Nginx

```bash
sudo apt install nginx -y
```
Installed the Nginx web server successfully.

## Verify Nginx Service

```bash
sudo systemctl status nginx
```
Verified that the Nginx service was running.

![check status](Images/check%20status.png)

## Enable Nginx at Boot

```bash
sudo systemctl enable nginx
```
Nginx will automatically start after every reboot.

---

# Part 4 – Configure Security Group

Allowed the following inbound rule in the EC2 Security Group:

| Port | Protocol | Purpose |
|------|----------|---------|
| 80 | HTTP | Web server |



![Configure Security Group](Images/Configure%20Security%20Group.png)

---

# Part 5 – Verify Web Server

## Test Nginx from Browser

```bash
http://13.233.163.150
```

![nginx default page](Images/nginx%20default%20page.png)

### Observation
The default Nginx page was successfully accessible through the public IP.

---

### Create Custom Web Page

```bash
cd /var/www/html
vim index.nginx-debian.html
```

Modified the default Nginx page with my custom content.

![Custom Web Page](Images/Custom%20Web%20Page.png)

---

# Part 6 – View Nginx Logs

## Method 1:View Ngnix logs using cat /var/log 

```bash
cat /var/log/nginx/access.log
```

Displayed HTTP requests received by the server.

## Method 2: View Ngnix logs using journctl 

```bash
sudo journalctl -u nginx -n 20
```

Viewed the latest 20 Nginx log entries.

![View Ngnix logs](Images/View%20Ngnix%20logs.png)
---

# Part 7 – Save Logs

## Save Access Log

```bash
cp /var/log/nginx/access.log ~/nginx-logs.txt
```
Copied the Nginx access log into my home directory.
### Save Logs

```bash
sudo journalctl -u nginx -n 20 > ~/nginx-logs.txt
```
Saved the latest Nginx service logs into a file.

### Verify Log File

```bash
ls -l
cat nginx-logs.txt
```

Verified that the log file was created and checked its contents.

![Verify Log](Images/View%20Ngnix%20logs.png)

---

# Part 8 – Download Log File

Run on your local machine:

```bash
scp -i "devops.pem" ubuntu@ubuntu@ec2-13-233-163-150.ap-south-1.compute.amazonaws.com:~/nginx-logs.txt .
```

### Observation

Downloaded the Nginx log file from the EC2 instance to the local machine.

![Download Log File](Images/Download%20Log%20File.png)
---


## Challenges Faced

- SCP initially failed because the PEM file was not in my current directory.
- I initially tried to create the web page in the wrong directory.
- The web page file was owned by root, so I could not edit it directly as the ubuntu user.

### Solution

- Navigated to the Downloads folder where the PEM file was stored.
- I moved to the Nginx web root:`/var/www/html` and then modified the required file.
- I changed the file ownership so that the ubuntu user could edit it: `sudo chown ubuntu:ubuntu index.nginx-debian.html`. After changing the ownership, I was able to edit and update the web page.


## What I Learned

- How to connect to an AWS EC2 instance using SSH.
- Installed and managed Nginx using systemctl.
- How AWS Security Groups control inbound traffic.
- How to view service logs using `cat /var/log/` & `journalctl`.
- How to transfer files securely using `scp`.
- Understood how Linux file ownership can affect application configuration and editing.
