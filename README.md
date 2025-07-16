# SOP for Managing Services in Ubuntu using `systemctl`

This document provides a complete Standard Operating Procedure (SOP) for managing system services (daemons) on Ubuntu using `systemctl`. It includes viewing, starting, stopping, enabling, disabling, and troubleshooting services — essential for DevOps engineers, system administrators, and students.

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

In Linux, services (also called daemons) are background processes that start on boot or when required. Examples include:

| Service     | Purpose              |
|-------------|----------------------|
| nginx       | Web Server           |
| mysql       | Database Server      |
| docker      | Container Engine     |
| ssh         | Remote Access        |
| jenkins     | CI/CD Automation     |

---

## systemctl Command Reference

| Action              | Command                                 | Description                           |
|---------------------|------------------------------------------|----------------------------------------|
| Start               | `sudo systemctl start <service>`        | Start the service immediately          |
| Stop                | `sudo systemctl stop <service>`         | Stop the running service               |
| Restart             | `sudo systemctl restart <service>`      | Restart the service                    |
| Reload              | `sudo systemctl reload <service>`       | Reload service config without restart  |
| Enable              | `sudo systemctl enable <service>`       | Enable service to start on boot        |
| Disable             | `sudo systemctl disable <service>`      | Disable service from auto-start        |
| Check Status        | `systemctl status <service>`            | Show current status of the service     |
| Check if Enabled    | `systemctl is-enabled <service>`        | Show if service is enabled on boot     |
| View Logs           | `journalctl -u <service>`               | View logs for the service              |

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
Check if running	systemctl status <service>	active (running)
Check if enabled on boot	systemctl is-enabled <service>	enabled
View service logs	journalctl -u <service>	Logs should appear
Validate nginx config	sudo nginx -t	syntax is ok

Troubleshooting
Problem	Suggested Solution
Service fails to start	Use journalctl -xe to see detailed logs
Port already in use	Run sudo lsof -i :<port> or `ss -tuln
Invalid configuration	Test config (e.g., sudo nginx -t)
Not auto-starting on boot	Run sudo systemctl enable <service>

Config File Paths
Service	Configuration File Path
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

yaml
Copy
Edit
