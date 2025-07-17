# SOP for Managing Services in Ubuntu using `systemctl`

This document provides a complete Standard Operating Procedure (SOP) for managing system services (daemons) on Ubuntu using `systemctl`. It includes viewing, starting, stopping, enabling, disabling, and troubleshooting services — essential for DevOps engineers, system administrators, and students.

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
 Section: Troubleshooting
markdown
Copy
Edit
## Troubleshooting

| Issue                        | Cause / Fix                                              |
|------------------------------|----------------------------------------------------------|
| Service fails to start       | Run `journalctl -xe` to check logs                      |
| Port already in use          | Use `sudo lsof -i :<port>` or `ss -tuln | grep :<port>`  |
| Invalid config (e.g. nginx)  | Run `sudo nginx -t` to test config                      |
| Not starting on boot         | Run `sudo systemctl enable <service>`                   |
 Section: Config File Paths
markdown
Copy
Edit
## Config File Paths

| Service     | Configuration File Path             |
|-------------|--------------------------------------|
| nginx       | `/etc/nginx/nginx.conf`             |
| mysql       | `/etc/mysql/mysql.conf.d/`          |
| docker      | `/etc/docker/daemon.json`           |
| jenkins     | `/etc/default/jenkins`              |
| ufw         | `/etc/ufw/ufw.conf`                 |


## Version History

| Author          | Created on | Version   | Last updated by | Internal Reviewer | L0     | L1      | L2     |
|-----------------|------------|-----------|------------------|--------------------|--------|---------|--------|
| Anuj Jain       | 17-04-25   | version 1 | N/A              | Priyanshu          | Khushi | Rishabh | Piyush |





---

## References

- Ubuntu Systemd Documentation: https://www.freedesktop.org/wiki/Software/systemd/
- systemctl Manual: https://man7.org/linux/man-pages/man1/systemctl.1.html
- journalctl Manual: https://man7.org/linux/man-pages/man1/journalctl.1.html
- Ansible Service Module: https://docs.ansible.com/ansible/latest/collections/ansible/builtin/service_module.html
- Nginx Official Docs: https://nginx.org/en/docs/
- Docker Systemd Integration: https://docs.docker.com/config/daemon/systemd/

