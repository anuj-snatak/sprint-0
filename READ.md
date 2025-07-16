📘 Standard Operating Procedure (SOP)
Managing Services in Ubuntu using systemctl
✅ Table of Contents
Objective

Scope

Prerequisites

Understanding Services in Ubuntu

Basic systemctl Commands

Example Use Cases

How to Validate Services

Troubleshooting Tips

Config File Locations (Ubuntu Specific)

Automation via Shell and Ansible

Version History

1️⃣ Objective
This SOP aims to provide a clear and standardized method to manage services on a Ubuntu Linux system using the systemctl command.
It ensures users can easily start, stop, enable, disable, and monitor services for smoother operations in development, testing, and production environments.

2️⃣ Scope
This SOP applies to all services (daemons) managed on Ubuntu OS using systemd.
It is especially useful for:

System Administrators

DevOps Engineers

Students working on DevOps/Linux practicals

Anyone managing system services on Ubuntu

3️⃣ Prerequisites
Before managing services, ensure the following:

OS: Ubuntu 20.04 or 22.04 LTS (systemd-enabled)

Terminal or SSH access

Sudo or root privileges

Target service should be installed (e.g., nginx, mysql)

4️⃣ Understanding Services in Ubuntu
In Linux, services are background programs (also called daemons). Examples:

nginx – Web server

mysql – Database

docker – Container runtime

jenkins – CI/CD automation

cron – Scheduler

ssh – Remote login

These services are managed using systemd, and the tool used is systemctl.

5️⃣ Basic systemctl Commands
Action	Command	Explanation
Start a service	sudo systemctl start <service>	Runs the service immediately
Stop a service	sudo systemctl stop <service>	Stops the running service
Restart a service	sudo systemctl restart <service>	Stops and starts again
Reload config	sudo systemctl reload <service>	Reloads config without restarting
Enable service	sudo systemctl enable <service>	Starts the service automatically at system boot
Disable service	sudo systemctl disable <service>	Prevents service from starting at boot
Status check	systemctl status <service>	Shows active/inactive status with logs
Is enabled?	systemctl is-enabled <service>	Shows whether service will start at boot
View logs	journalctl -u <service>	Shows log output of the service

🔁 Replace <service> with actual name, e.g. nginx, docker, mysql.

6️⃣ Example Use Cases
bash
Copy
Edit
sudo systemctl start nginx              # Start web server
sudo systemctl enable mysql            # Enable DB service on boot
sudo systemctl restart docker          # Restart Docker engine
sudo systemctl stop jenkins            # Stop Jenkins
systemctl status nginx                 # Check nginx status
7️⃣ How to Validate Services
Check	Command	Expected Output
Is service running?	systemctl status nginx	active (running)
Is service auto-starting?	systemctl is-enabled mysql	enabled
View latest logs	journalctl -u docker --since "10 min ago"	Logs from last 10 min
Is config valid? (nginx)	sudo nginx -t	syntax is ok

8️⃣ Troubleshooting Tips
Issue	Solution
Service failed to start	Check logs: journalctl -xe
Port already in use	Find conflict: sudo lsof -i :80 or `ss -tuln
Permission denied	Add sudo before command
Error in config file	Use validation: nginx -t, mysqld --verbose
Service not starting on boot	Enable it: sudo systemctl enable <service>

9️⃣ Important Config Files (Ubuntu Specific)
Service	Configuration File Path
Nginx	/etc/nginx/nginx.conf
MySQL	/etc/mysql/mysql.conf.d/mysqld.cnf
Docker	/etc/docker/daemon.json
Jenkins	/etc/default/jenkins
UFW Firewall	/etc/ufw/ufw.conf

🔟 Automation Tip
✅ Shell Script Example
bash
Copy
Edit
#!/bin/bash
SERVICE=$1
ACTION=$2
sudo systemctl $ACTION $SERVICE
Usage: ./service.sh nginx restart

✅ Ansible Example
yaml
Copy
Edit
- name: Ensure nginx is running
  service:
    name: nginx
    state: started
    enabled: yes
🔁 11. Version History
Version	Date	Author	Remarks
1.0	16-July-2025	Anuj Jain	Initial version for Ubuntu systemctl SOP

✅ Conclusion
This documentation gives a clear step-by-step understanding of managing services on Ubuntu Linux using systemctl.
It is extremely important for DevOps, production, and educational environments.
Mastering these commands gives you confidence in managing Linux systems efficiently.

