# 🛠️ SOP: Viewing, Applying & Persisting Kernel Parameter Changes (`sysctl`)

## 📌 Objective
Provide a streamlined approach for viewing, applying (temporarily), and persisting Linux kernel parameter changes using **sysctl**, enhancing performance and security on live systems.

---

## 🗂️ Contents
1. [Why Modify Kernel Parameters?](#why-modify-kernel-parameters)  
2. [Methods of Changing Kernel Tunables](#methods-of-changing-kernel-tunables)  
3. [1. Viewing Kernel Parameters](#1-viewing-kernel-parameters)  
4. [2. Applying Changes Temporarily](#2-applying-changes-temporarily)  
5. [3. Persisting Changes Permanently](#3-persisting-changes-permanently)  
6. [4. Performance Tuning Examples](#4-performance-tuning-examples)  
7. [5. Security Hardening Examples](#5-security-hardening-examples)  
8. [6. Best Practices](#6-best-practices)  
9. [References & Further Reading](#references--further-reading)

---

## Why Modify Kernel Parameters?
Kernel parameters (sysctl) control low-level OS behaviors like networking limits, memory management, and file descriptors. Adjusting them helps you:

- **Improve performance** (e.g., reduce swap, raise open-file limits)  
- **Harden security** (e.g., prevent IP forwarding, disable redirects)

---

## Methods of Changing Kernel Tunables
1. **sysctl command** – temporary, in-memory change  
2. **Edit `/etc/sysctl.conf`** – persistent via central file  
3. **Add files in `/etc/sysctl.d/`** – recommended modular persistence

---

### 1. Viewing Kernel Parameters
- Show all current values:
  ```bash
  sysctl -a
View specific parameter:

bash
Copy
Edit
sysctl net.ipv4.ip_forward
List only parameter names:

bash
Copy
Edit
sysctl -a -N
2. Applying Changes Temporarily
Run-time change (lost upon reboot):

bash
Copy
Edit
sudo sysctl -w net.ipv4.ip_forward=1
sysctl net.ipv4.ip_forward
3. Persisting Changes Permanently
A. /etc/sysctl.conf Method:
Edit file:

bash
Copy
Edit
sudo vi /etc/sysctl.conf
Add your parameter:

ini
Copy
Edit
net.ipv4.ip_forward = 1
Apply changes:

bash
Copy
Edit
sudo sysctl -p /etc/sysctl.conf
B. /etc/sysctl.d/ Method (Recommended):
Create:

bash
Copy
Edit
sudo vim /etc/sysctl.d/99-custom.conf
Add parameters:

ini
Copy
Edit
net.ipv4.ip_forward = 1
Apply all settings:

bash
Copy
Edit
sudo sysctl --system
4. Performance Tuning Examples
Parameter	Description	Typical Value	Effect Summary
vm.swappiness	Swap vs RAM usage threshold	10	Lower → less swapping
vm.dirty_ratio	Write buffer limit to disk	15	Lower → more frequent writes
fs.file-max	Maximum open-file handles	2097152	Higher → supports high-connections
net.core.somaxconn	TCP backlog queue size	1024	Higher → handles more incoming traffic

5. Security Hardening Examples
Parameter	Purpose	Recommended
net.ipv4.ip_forward	Prevent host from acting as a router	0
net.ipv4.tcp_syncookies	Mitigate SYN flood attacks	1
net.ipv4.conf.all.accept_redirects	Avoid ICMP redirect spoofing	0
fs.suid_dumpable	Prevent memory dump from setuid executables	0

6. Best Practices
Test changes temporarily before making permanent

Modularize configs with /etc/sysctl.d/

Document rationale behind every tuning

Beware of side effects: some tunables impact stability or compatibility

📚 References & Further Reading
man sysctl

Kernel Documentation - sysctl

This improved format includes a clear structure, table of contents, action tables, and explanations—making it more user-friendly and professional than the original! 
stackoverflow.com
