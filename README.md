# **Standard Operating Procedure (SOP) for Managing Services in Ubuntu using `systemctl`**  
**Document Version:** 2.0  
**Last Updated:** 18-07-25  
**Author:** Anuj Jain  
**Reviewer:** Prashnat  

---

## **1. Document Control**  

### **1.1 Version History**  

| Version | Date       | Author      | Changes Made                          | Reviewed By |
|---------|------------|-------------|---------------------------------------|-------------|
| 1.0     | 17-07-25   | Anuj Jain   | Initial draft                         | Prashnat    |

### **1.2 Approval**  

| Role              | Name        | Signature  | Date       |
|-------------------|-------------|------------|------------|
| Reviewer          | Prashnat    | [Signature]| 17-07-25   |

---

## **2. Introduction**  

### **2.1 Objective**  
This SOP provides a standardized approach to managing system services (daemons) on **Ubuntu (20.04/22.04 LTS)** using `systemctl`. It ensures **consistency, reliability, and security** in service management for DevOps engineers, sysadmins, and students.  

### **2.2 Scope**  
- Applies to **Ubuntu (systemd-based systems)**.  
- Covers **common services** (`nginx`, `mysql`, `docker`, `jenkins`, `ssh`, `ufw`).  
- Includes **startup control, status checks, troubleshooting, and security hardening**.  

---

## **3. Prerequisites**  

 **System Requirements:**  
- Ubuntu 20.04/22.04 LTS (systemd-based).  
- `sudo` or root access.  
- Services must be installed (e.g., `nginx`, `docker`).  

 **Knowledge Requirements:**  
- Basic Linux terminal commands.  
- Understanding of service dependencies.  

---

## **4. Understanding Services & `systemctl`**  

### **4.1 What is a Service (Daemon)?**  
A **service** is a background process that runs continuously, handling tasks like web serving (`nginx`), databases (`mysql`), or automation (`jenkins`).  

### **4.2 Key `systemctl` Concepts**  
| Term          | Description |
|--------------|------------|
| **Unit File** | Config file (`.service`) defining how a service runs. Location: `/etc/systemd/system/` |
| **Enable** | Starts service at boot. |
| **Disable** | Prevents auto-start. |
| **Mask** | Completely blocks service (even manual start). |

---

## **5. `systemctl` Command Reference**  

### **5.1 Basic Service Management**  

| **Action**       | **Command** | **Example** | **Notes** |
|------------------|------------|------------|-----------|
| **Start**        | `sudo systemctl start <service>` | `sudo systemctl start nginx` | Begins service immediately. |
| **Stop**         | `sudo systemctl stop <service>` | `sudo systemctl stop mysql` | Gracefully shuts down service. |
| **Restart**      | `sudo systemctl restart <service>` | `sudo systemctl restart docker` | Stops & starts again. |
| **Reload**       | `sudo systemctl reload <service>` | `sudo systemctl reload ssh` | Reloads config **without** full restart. |
| **Enable**       | `sudo systemctl enable <service>` | `sudo systemctl enable jenkins` | Starts at boot. |
| **Disable**      | `sudo systemctl disable <service>` | `sudo systemctl disable ufw` | Won’t start at boot. |
| **Mask**         | `sudo systemctl mask <service>` | `sudo systemctl mask apache2` | **Blocks** service entirely. |
| **Unmask**       | `sudo systemctl unmask <service>` | `sudo systemctl unmask apache2` | Reverses `mask`. |

### **5.2 Service Status & Logs**  

| **Action**       | **Command** | **Example** | **Notes** |
|------------------|------------|------------|-----------|
| **Check Status** | `systemctl status <service>` | `systemctl status nginx` | Shows if running, logs, errors. |
| **Is Enabled?**  | `systemctl is-enabled <service>` | `systemctl is-enabled ssh` | Returns `enabled`/`disabled`. |
| **View Logs**    | `journalctl -u <service>` | `journalctl -u docker` | Debug issues. |
| **Follow Logs**  | `journalctl -u <service> -f` | `journalctl -u nginx -f` | Real-time monitoring. |

---

## **6. Best Practices & Security**  

### **6.1 Security Hardening**  
 **Do:**  
- Use `mask` for unnecessary services (e.g., `sudo systemctl mask telnet`).  
- Always `disable` unused services (e.g., `sudo systemctl disable apache2` if using `nginx`).  
- Restrict service permissions (e.g., `User=www-data` in `nginx.service`).  

### **6.2 Performance & Stability**  
 **Do:**  
- Use `reload` instead of `restart` where possible (avoids downtime).  
- Check dependencies with `systemctl list-dependencies <service>`.  

---

## **7. Troubleshooting Guide**  

### **7.1 Common Issues & Fixes**  

| **Issue** | **Diagnosis Command** | **Solution** |
|-----------|----------------------|--------------|
| **Service fails to start** | `journalctl -xe` | Check logs for errors. |
| **Port conflict** | `sudo ss -tulnp \| grep :80` | Kill conflicting process or change port. |
| **Config error (e.g., nginx)** | `sudo nginx -t` | Fix syntax errors in config. |
| **Service stuck in "activating"** | `systemctl status <service>` | Check dependencies (`systemctl list-dependencies`). |

### **7.2 Emergency Recovery**  
 **If a critical service (e.g., `ssh`) fails:**  
1. **Check logs:** `journalctl -u ssh --no-pager -n 50`  
2. **Force-restart:** `sudo systemctl reset-failed ssh && sudo systemctl restart ssh`  
3. **Fallback:** Use a backup config (`cp /etc/ssh/sshd_config.bak /etc/ssh/sshd_config`).  

---

## **8. Appendix**  

### **8.1 Common Service Config Paths**  

| **Service** | **Config File** | **Notes** |
|------------|----------------|-----------|
| `nginx`    | `/etc/nginx/nginx.conf` | Test with `nginx -t`. |
| `mysql`    | `/etc/mysql/mysql.conf.d/mysqld.cnf` | Requires restart. |
| `docker`   | `/etc/docker/daemon.json` | Edit for storage, proxies. |
| `jenkins`  | `/etc/default/jenkins` | Java args, ports. |
| `ufw`      | `/etc/ufw/ufw.conf` | Controls firewall. |

### **8.2 Quick Reference Cheat Sheet**  
 **One-liners:**  
- **List all services:** `systemctl list-units --type=service`  
- **Find failed services:** `systemctl --failed`  
- **Reload systemd after config changes:** `sudo systemctl daemon-reload`  

---

## **9. References**  
- [Official systemd Documentation](https://www.freedesktop.org/wiki/Software/systemd/)  
- [Ubuntu Manpages: systemctl](https://manpages.ubuntu.com/manpages/jammy/en/man1/systemctl.1.html)  
- [Nginx Troubleshooting](https://nginx.org/en/docs/beginners_guide.html#troubleshooting)  

---

## **10. Feedback & Revisions**  
📩 **Contact:**  
- **Author:** Anuj Jain (`anuj.jain@mygurukulam.co`)  

