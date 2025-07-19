
# SOP for Managing Services in Ubuntu using `systemctl`

This document provides a complete Standard Operating Procedure (SOP) for managing system services (daemons) on Ubuntu using `systemctl`. It includes viewing, starting, stopping, enabling, disabling, and troubleshooting services — essential for DevOps engineers, system administrators, and students.


## Version History

| Author          | Created on | Version   | Last updated by | Internal Reviewer |
|-----------------|------------|-----------|------------------|--------------------|
| Anuj Jain       | 17-07-25   | version 1 | N/A              | Prashnat          |

---

## Table of Contents

1. [Objective](#objective)  
2. [Scope](#scope)  
3. [Prerequisites](#prerequisites)  
4. [What is a Service?](#what-is-a-service)  
5. [systemctl Command Reference](#systemctl-command-reference)  
6. [Common Examples](#common-examples)  
7. [Service Validation Checklist](#service-validation-checklist)  
8. [Troubleshooting](#troubleshooting)  
9. [Config File Paths](#config-file-paths)  
10. [Version History](#version-history)  
11. [References](#references)

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

In Linux, services (also called daemons) are background programs that start automatically when the system boots, or run when needed. They handle important tasks without user interaction.

Here are a few common ones:

nginx – A lightweight and fast web server used to host websites, act as a reverse proxy, or handle load balancing.

mysql – A database service that stores and manages data for web apps or software.

docker – Runs containers. It's used to package apps with their dependencies so they work the same on any system.

ssh – Lets you connect to another machine remotely and securely using the terminal.

jenkins – An automation server used for building, testing, and deploying code (CI/CD).



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

🔧 Systemctl Command Reference (Service Management in Ubuntu)
Here’s a cleaner and properly formatted version using collapsible sections (GitHub supports them), code blocks, and markdown best practices:

markdown
Copy
Edit
## 🔧 Systemctl Command Reference

<details>
<summary><strong>▶️ Start a Service</strong></summary>

```bash
sudo systemctl start <service>
Starts the specified service immediately.

</details> <details> <summary><strong>⛔ Stop a Service</strong></summary>
bash
Copy
Edit
sudo systemctl stop <service>
Stops the running service.

</details> <details> <summary><strong>🔁 Restart a Service</strong></summary>
bash
Copy
Edit
sudo systemctl restart <service>
Restarts the service (stop + start).

</details> <details> <summary><strong>🔃 Reload a Service</strong></summary>
bash
Copy
Edit
sudo systemctl reload <service>
Reloads the service configuration without restarting it.

</details> <details> <summary><strong>🚀 Enable Service on Boot</strong></summary>
bash
Copy
Edit
sudo systemctl enable <service>
Enables the service to start automatically at boot time.

</details> <details> <summary><strong>❌ Disable Service from Auto-start</strong></summary>
bash
Copy
Edit
sudo systemctl disable <service>
Disables the service from starting at boot.

</details> <details> <summary><strong>📊 Check Service Status</strong></summary>
bash
Copy
Edit
systemctl status <service>
Displays current service status.

</details> <details> <summary><strong>🔍 Check if Enabled</strong></summary>
bash
Copy
Edit
systemctl is-enabled <service>
Shows whether the service is set to auto-start.

</details> <details> <summary><strong>📝 View Service Logs</strong></summary>
bash
Copy
Edit
journalctl -u <service>
Displays logs for the specified service.

</details>


## Common Examples

| Command                                      | Description                       |
|----------------------------------------------|-----------------------------------|
| `sudo systemctl start docker`               | Start Docker service              |
| `sudo systemctl enable mysql`               | Enable MySQL to start on boot     |
| `sudo systemctl restart ssh`                | Restart SSH service               |
| `sudo systemctl disable jenkins`            | Disable Jenkins auto-start        |
| `systemctl status nginx`                    | Check status of Nginx             |

## Service Validation Checklist

| Validation Step              | Command                          | Expected Output         |
|------------------------------|----------------------------------|-------------------------|
| Check if service is running  | `systemctl status <service>`     | `active (running)`      |
| Check if service is enabled  | `systemctl is-enabled <service>` | `enabled`               |
| View service logs            | `journalctl -u <service>`        | Service logs appear     |
| Validate nginx config        | `sudo nginx -t`                  | Syntax is OK message    |

## Troubleshooting

| Issue                        | Cause / Fix                                              |
|------------------------------|----------------------------------------------------------|
| Service fails to start       | Run `journalctl -xe` to check logs                      |
| Port already in use          | Use `sudo lsof -i :<port>` or `ss -tuln | grep :<port>`  |
| Invalid config (e.g. nginx)  | Run `sudo nginx -t` to test config                      |
| Not starting on boot         | Run `sudo systemctl enable <service>`                   |

## Config File Paths

| Service     | Configuration File Path             |
|-------------|--------------------------------------|
| nginx       | `/etc/nginx/nginx.conf`             |
| mysql       | `/etc/mysql/mysql.conf.d/`          |
| docker      | `/etc/docker/daemon.json`           |
| jenkins     | `/etc/default/jenkins`              |
| ufw         | `/etc/ufw/ufw.conf`                 |



## Contact Information

| Name            | Email address |
|-----------------|---------------|
| Anuj Jain       | anuj.jain@mygurukulam.co      | 



---

## References

- Ubuntu Systemd Documentation: https://www.freedesktop.org/wiki/Software/systemd/
- systemctl Manual: https://man7.org/linux/man-pages/man1/systemctl.1.html
- journalctl Manual: https://man7.org/linux/man-pages/man1/journalctl.1.html
- Nginx Official Docs: https://nginx.org/en/docs/
- Docker Systemd Integration: https://docs.docker.com/config/daemon/systemd/
