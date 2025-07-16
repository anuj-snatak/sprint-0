# SOP for Managing Services in Ubuntu using `systemctl`

This document provides a complete Standard Operating Procedure (SOP) for managing system services (daemons) on Ubuntu using `systemctl`. It includes viewing, starting, stopping, enabling, disabling, and troubleshooting services — essential for DevOps, system administrators, and students.

---

## Table of Contents

1. Objective  
2. Scope  
3. Prerequisites  
4. What is a Service?  
5. systemctl Command Reference  
6. Common Examples  
7. Service Validation Checklist  
8. Troubleshooting  
9. Config File Paths  
10. Automation Using Ansible  
11. Version History

---

## Objective

To define a clear and repeatable SOP to manage Linux services in Ubuntu OS using the `systemctl` command. This ensures consistency, system stability, and operational clarity.

---

## Scope

Applies to:
- Ubuntu 20.04 / 22.04 LTS  
- Services like: `nginx`, `mysql`, `docker`, `jenkins`, `cron`, `ufw`, `ssh`

---

## Prerequisites

- Ubuntu machine with systemd  
- Sudo/root access  
- Terminal access or SSH login  
- Services must be installed

---

## What is a Service?

In Linux, services (daemons) are background processes that start on boot or on demand. Common ones include:

| Service     | Purpose              |
|-------------|----------------------|
| nginx       | Web Server           |
| mysql       | Database Server      |
| docker      | Container Engine     |
| ssh         | Remote Access        |
| jenkins     | CI/CD Automation     |

---

## systemctl Command Reference

| Action             | Command                              | Description                            |
|--------------------|---------------------------------------|----------------------------------------|
| Start              | `sudo systemctl start nginx`         | Start service immediately              |
| Stop               | `sudo systemctl stop nginx`          | Stop service                           |
| Restart            | `sudo systemctl restart nginx`       | Stop and start again                   |
| Reload             | `sudo systemctl reload nginx`        | Reload config without stopping         |
| Enable (boot)      | `sudo systemctl enable nginx`        | Start on boot                          |
| Disable (boot)     | `sudo systemctl disable nginx`       | Don't start on boot                    |
| Status             | `systemctl status nginx`             | Show active/inactive/logs              |
| Is Enabled?        | `systemctl is-enabled nginx`         | Check boot-start status                |
| Logs               | `journalctl -u nginx`                | Show logs for the service              |

---

## Common Examples

```bash
sudo systemctl start docker
sudo systemctl enable mysql
sudo systemctl restart ssh
sudo systemctl disable jenkins
systemctl status nginx
Service Validation Checklist
Validation Step	Command	Expected Output
Service is running?	systemctl status <svc>	active (running)
Auto-start on boot?	systemctl is-enabled <svc>	enabled
Logs available?	journalctl -u <svc>	Log output shown
Config syntax (nginx)?	sudo nginx -t	syntax is ok

Troubleshooting
Problem	Solution
Service fails to start	journalctl -xe for logs
Port already in use	sudo lsof -i :80 or `ss -tuln
Invalid config (e.g. nginx)	sudo nginx -t
Auto-start not working	sudo systemctl enable <service>

Config File Paths
Service	Config File Location
nginx	/etc/nginx/nginx.conf
mysql	/etc/mysql/mysql.conf.d/
docker	/etc/docker/daemon.json
jenkins	/etc/default/jenkins
ufw	/etc/ufw/ufw.conf

Automation Using Ansible
yaml
Copy
Edit
- name: Ensure nginx is running
  service:
    name: nginx
    state: started
    enabled: yes
Version History
Version	Date	Author	Remarks
1.0	16-July-2025	Anuj Jain	Initial SOP for Ubuntu Services

