Yeh raha tumhaara **SOP Markdown**, jiska font styling aur visual appearance simple aur clean banaya gaya hai (no emojis, no bold overload, minimal clutter) — GitHub, GitLab, or any Markdown viewer ke liye perfect:

---

````markdown
# SOP for Managing Services in Ubuntu using `systemctl`

This document provides a complete Standard Operating Procedure (SOP) for managing system services (daemons) on Ubuntu using `systemctl`. It includes viewing, starting, stopping, enabling, disabling, and troubleshooting services — essential for DevOps engineers, system administrators, and students.

## Version History

| Author      | Created on | Version   | Last updated by | Internal Reviewer |
|-------------|------------|-----------|------------------|--------------------|
| Anuj Jain   | 17-07-25   | version 1 | N/A              | Prashnat           |

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

In Linux, services (daemons) are background processes that typically start automatically at boot or run when triggered. These services handle essential system or application-level tasks without direct user interaction.

### Common Linux Services

| Service   | Description |
|-----------|-------------|
| nginx     | A lightweight, fast web server used to host websites, act as a reverse proxy, or handle load balancing. |
| mysql     | A relational database service that stores and manages data for web applications and software. |
| docker    | A container engine that runs applications inside containers, ensuring they run the same across different environments. |
| ssh       | A secure shell service that enables remote login and command execution over encrypted connections. |
| jenkins   | A CI/CD automation server used to build, test, and deploy code automatically in DevOps pipelines. |

---

## systemctl Command Reference

| Action            | Command                             | Description                          |
|-------------------|--------------------------------------|--------------------------------------|
| Start             | `sudo systemctl start <service>`     | Start the service immediately        |
| Stop              | `sudo systemctl stop <service>`      | Stop the running service             |
| Restart           | `sudo systemctl restart <service>`   | Restart the service                  |
| Reload            | `sudo systemctl reload <service>`    | Reload service config without restart |
| Enable            | `sudo systemctl enable <service>`    | Enable service to start on boot      |
| Disable           | `sudo systemctl disable <service>`   | Disable service from auto-start      |
| Check Status      | `systemctl status <service>`         | Show current status of the service   |
| Check if Enabled  | `systemctl is-enabled <service>`     | Show if service is enabled on boot   |
| View Logs         | `journalctl -u <service>`            | View logs for the service            |

---

## How to Use `systemctl` Commands

### Start a Service

```bash
sudo systemctl start <service>
````

Example:

```bash
sudo systemctl start nginx
```

### Stop a Service

```bash
sudo systemctl stop <service>
```

Example:

```bash
sudo systemctl stop mysql
```

### Restart a Service

```bash
sudo systemctl restart <service>
```

Example:

```bash
sudo systemctl restart ssh
```

### Reload a Service (Without Restart)

```bash
sudo systemctl reload <service>
```

Example:

```bash
sudo systemctl reload apache2
```

### Enable a Service on Boot

```bash
sudo systemctl enable <service>
```

Example:

```bash
sudo systemctl enable docker
```

### Disable a Service from Auto-Starting

```bash
sudo systemctl disable <service>
```

Example:

```bash
sudo systemctl disable jenkins
```

### Check Status of a Service

```bash
systemctl status <service>
```

Example:

```bash
systemctl status ssh
```

### Check if a Service is Enabled

```bash
systemctl is-enabled <service>
```

Example:

```bash
systemctl is-enabled mysql
```

### View Service Logs

```bash
journalctl -u <service>
```

Example:

```bash
journalctl -u nginx
```

---

## Common Examples

| Command                          | Description                   |
| -------------------------------- | ----------------------------- |
| `sudo systemctl start docker`    | Start Docker service          |
| `sudo systemctl enable mysql`    | Enable MySQL to start on boot |
| `sudo systemctl restart ssh`     | Restart SSH service           |
| `sudo systemctl disable jenkins` | Disable Jenkins auto-start    |
| `systemctl status nginx`         | Check status of Nginx         |

---

## Service Validation Checklist

| Validation Step       | Command                          | Expected Output  |
| --------------------- | -------------------------------- | ---------------- |
| Is service running?   | `systemctl status <service>`     | active (running) |
| Is service enabled?   | `systemctl is-enabled <service>` | enabled          |
| View service logs     | `journalctl -u <service>`        | Logs appear      |
| Validate nginx config | `sudo nginx -t`                  | Syntax is OK     |

---

## Troubleshooting

| Issue                       | Cause / Fix                              |                |
| --------------------------- | ---------------------------------------- | -------------- |
| Service fails to start      | Run `journalctl -xe` to view logs        |                |
| Port already in use         | Use `sudo lsof -i :<port>` or \`ss -tuln | grep :<port>\` |
| Invalid config (e.g. nginx) | Run `sudo nginx -t` to check config      |                |
| Not starting on boot        | Run `sudo systemctl enable <service>`    |                |

---

## Config File Paths

| Service | Configuration File Path    |
| ------- | -------------------------- |
| nginx   | `/etc/nginx/nginx.conf`    |
| mysql   | `/etc/mysql/mysql.conf.d/` |
| docker  | `/etc/docker/daemon.json`  |
| jenkins | `/etc/default/jenkins`     |
| ufw     | `/etc/ufw/ufw.conf`        |

---

## Contact Information

| Name      | Email Address                                               |
| --------- | ----------------------------------------------------------- |
| Anuj Jain | [anuj.jain@mygurukulam.co](mailto:anuj.jain@mygurukulam.co) |

---

## References

* Ubuntu Systemd: [https://www.freedesktop.org/wiki/Software/systemd/](https://www.freedesktop.org/wiki/Software/systemd/)
* systemctl Manual: [https://man7.org/linux/man-pages/man1/systemctl.1.html](https://man7.org/linux/man-pages/man1/systemctl.1.html)
* journalctl Manual: [https://man7.org/linux/man-pages/man1/journalctl.1.html](https://man7.org/linux/man-pages/man1/journalctl.1.html)
* Nginx Docs: [https://nginx.org/en/docs/](https://nginx.org/en/docs/)
* Docker and systemd: [https://docs.docker.com/config/daemon/systemd/](https://docs.docker.com/config/daemon/systemd/)

```
