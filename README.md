# SOP: Managing Services in Ubuntu Using systemctl

> **Document Type**: SOP (Standard Operating Procedure)  
> **Applicable OS**: Ubuntu 20.04 / 22.04 LTS  
> **Author**: Anuj Jain  
> **Reviewer**: Prashant  
> **Created On**: 2025-07-17  
> **Version**: 1.0

---

## Table of Contents

1. [Objective](#objective)  
2. [Scope](#scope)  
3. [Prerequisites](#prerequisites)  
4. [Services Covered](#services-covered)  
5. [Systemctl Usage](#systemctl-usage)  
6. [Validation](#validation)  
7. [Troubleshooting](#troubleshooting)  
8. [Service Config Paths](#service-config-paths)  
9. [References](#references)

---

## Objective

This SOP provides standard commands and practices to manage system services (daemons) in Ubuntu using the `systemctl` utility.

---

## Scope

Applies to managing services like `nginx`, `mysql`, `docker`, `jenkins`, `ufw`, and `ssh` on Ubuntu 20.04 / 22.04 LTS systems.

---

## Prerequisites

- Ubuntu with systemd
- Sudo or root access
- Terminal or SSH access

---

## Services Covered

| Service   | Description                    |
|-----------|--------------------------------|
| nginx     | Web server & reverse proxy     |
| mysql     | Relational database            |
| docker    | Container engine               |
| jenkins   | CI/CD automation server        |
| ssh       | Remote shell access            |
| ufw       | Firewall management            |

---

## Systemctl Usage

| Action     | Command                                |
|------------|----------------------------------------|
| Start      | `sudo systemctl start <service>`       |
| Stop       | `sudo systemctl stop <service>`        |
| Restart    | `sudo systemctl restart <service>`     |
| Reload     | `sudo systemctl reload <service>`      |
| Enable     | `sudo systemctl enable <service>`      |
| Disable    | `sudo systemctl disable <service>`     |
| Status     | `systemctl status <service>`           |
| Is Enabled | `systemctl is-enabled <service>`       |
| Logs       | `journalctl -u <service>`              |

---

## Validation

| Step                  | Command                              | Expected Output        |
|-----------------------|--------------------------------------|------------------------|
| Check if running      | `systemctl status <service>`         | `active (running)`     |
| Check if enabled      | `systemctl is-enabled <service>`     | `enabled`              |
| Validate nginx config | `sudo nginx -t`                      | Syntax OK              |

---

## Troubleshooting

| Problem                | Command to Run                                  |
|------------------------|--------------------------------------------------|
| Service won't start     | `journalctl -xe`                                 |
| Port already in use     | `sudo lsof -i :<port>` or `ss -tuln | grep :<port>` |
| Invalid config (nginx)  | `sudo nginx -t`                                  |
| Not starting on boot    | `sudo systemctl enable <service>`               |

---

## Service Config Paths

| Service  | Config File Path                |
|----------|---------------------------------|
| nginx    | `/etc/nginx/nginx.conf`         |
| mysql    | `/etc/mysql/mysql.conf.d/`      |
| docker   | `/etc/docker/daemon.json`       |
| jenkins  | `/etc/default/jenkins`          |
| ufw      | `/etc/ufw/ufw.conf`             |

---

## References

- [systemctl man page](https://man7.org/linux/man-pages/man1/systemctl.1.html)  
- [journalctl man page](https://man7.org/linux/man-pages/man1/journalctl.1.html)  
- [Nginx Documentation](https://nginx.org/en/docs/)  
- [Docker systemd Integration](https://docs.docker.com/config/daemon/systemd/)

---

📎 **PR Instruction**:  
Attach this file in your repo under:
