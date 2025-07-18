Here's the complete, professionally formatted SOP document for managing services in Ubuntu using `systemctl`:

# **Standard Operating Procedure (SOP)**
## **Ubuntu Service Management with systemctl**  
**Document Version:** 3.0  
**Effective Date:** 25-Jul-2025  
**Author:** Anuj Jain  
**Approved By:** Prashnat  

---

### **1. Purpose**  
This SOP establishes standardized procedures for managing system services on Ubuntu Linux (20.04/22.04 LTS) using the `systemctl` command, ensuring consistent and reliable service operations.

---

### **2. Scope**  
Applies to:  
✔ All Ubuntu servers running systemd  
✔ Common services:  
   - Web: `nginx`, `apache2`  
   - Databases: `mysql`, `postgresql`  
   - DevOps: `docker`, `jenkins`  
   - Security: `ssh`, `ufw`  

---

### **3. Definitions**  
| Term | Meaning |
|------|---------|
| **Unit** | A systemd configuration file (.service, .socket) |
| **Daemon** | Background service process |
| **Journal** | System logging facility (`journalctl`) |

---

### **4. Service Management Procedures**  

#### **4.1 Basic Service Control**  
```bash
# Start service immediately
sudo systemctl start nginx

# Stop running service
sudo systemctl stop mysql

# Restart service (with downtime)
sudo systemctl restart docker

# Reload configuration (no downtime)
sudo systemctl reload ssh
```

#### **4.2 Boot Configuration**  
```bash
# Enable auto-start at boot
sudo systemctl enable jenkins

# Disable auto-start
sudo systemctl disable ufw

# Completely block service
sudo systemctl mask apache2

# Unblock service
sudo systemctl unmask apache2
```

---

### **5. Monitoring & Troubleshooting**  

#### **5.1 Status Checking**  
```bash
# Detailed service status
systemctl status nginx -l

# Verify auto-start configuration
systemctl is-enabled ssh

# Check active state
systemctl is-active docker
```

#### **5.2 Log Inspection**  
```bash
# View full service logs
journalctl -u mysql --no-pager -n 100

# Follow live logs (Ctrl+C to exit)
journalctl -u nginx -f

# Check for failures
journalctl -xe | grep -i error
```

#### **5.3 Common Issues Resolution**  

**Issue:** Service fails to start  
 **Solution:**  
```bash
1. Check logs: journalctl -u <service>
2. Test config: sudo nginx -t
3. Verify dependencies: systemctl list-dependencies <service>
```

**Issue:** Port conflict (Address already in use)  
 **Solution:**  
```bash
sudo ss -tulnp | grep :80
sudo kill -9 <PID>
```

---

### **6. Configuration Management**  

#### **6.1 Key Service Files**  
| Service | Configuration Path |
|---------|--------------------|
| nginx   | `/etc/nginx/nginx.conf` |
| mysql   | `/etc/mysql/mysql.conf.d/mysqld.cnf` |
| docker  | `/etc/docker/daemon.json` |

#### **6.2 Editing Service Units**  
```bash
# Edit service configuration
sudo systemctl edit --full nginx

# Apply changes
sudo systemctl daemon-reload
sudo systemctl restart nginx
```

---

### **7. Security Best Practices**  

✔ **Principle of Least Privilege:**  
```bash
sudo systemctl edit docker
[Service]
User=docker-user
```

✔ **Service Hardening:**  
```bash
# Disable unused services
sudo systemctl disable telnet

# Mask dangerous services
sudo systemctl mask rpcbind
```

---

### **8. Quick Reference Guide**  

| Task | Command |
|------|---------|
| List all services | `systemctl list-units --type=service` |
| Find failed services | `systemctl --failed` |
| Verify syntax | `sudo nginx -t` |
| Analyze boot time | `systemd-analyze blame` |

---

### **9. Document Control**  

**Review Cycle:** Quarterly  
**Next Review Date:** 25-Oct-2025  
**Contact:**  
- Author: anuj.jain@mygurukulam.co  
- Reviewer: prashnat@mygurukulam.co  

---

### **10. Appendices**  

**A. Service Dependencies**  
```bash
systemctl list-dependencies nginx
```

**B. Resource Monitoring**  
```bash
systemd-cgtop
```

**C. Official References**  
- [systemd Documentation](https://www.freedesktop.org/wiki/Software/systemd/)  
- [Ubuntu Man Pages](https://manpages.ubuntu.com/)  

---

### **Key Improvements in v3.0:**  
 **Clearer section organization** with numbered procedures  
 **Enhanced troubleshooting** with step-by-step solutions  
 **Added security hardening** guidelines  
 **Improved readability** with better formatting  
 **Practical examples** for every command  

This document now:  
✔ Looks professionally crafted (not AI-generated)  
✔ Contains actionable, step-by-step instructions  
✔ Includes real-world examples  
✔ Has proper version control  

Would you like me to add any specific service examples or modify any sections further?
