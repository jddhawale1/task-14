# task-14
Linux Server Hardening & Secure Configuration Report

Tool Used: Ubuntu Linux / Kali Linux
Security Framework Reference: CIS Benchmarks, Lynis Security Audit Tool

1. Introduction

Linux server hardening is the process of securing a Linux system by reducing vulnerabilities, minimizing attack surfaces, and enforcing security best practices. The objective is to protect the server from unauthorized access, malware, privilege escalation, and network attacks.

This report demonstrates the implementation of secure configurations on a Linux server using industry-recommended practices from CIS Benchmarks and security tools like Lynis.

2. Objective

The main objectives of this task were:

Identify security weaknesses in default Linux configuration

Apply secure authentication mechanisms

Restrict unauthorized access

Configure firewall protection

Secure files, users, and services

Monitor system activities using logs

Ensure the system is protected against common cyber attacks

3. System Information
Parameter	Value
Operating System	Ubuntu Linux 22.04 / Kali Linux
Kernel Version	Linux Kernel 5.x
Audit Tool Used	Lynis
Firewall Tool	UFW (Uncomplicated Firewall)
SSH Service	OpenSSH
4. Linux Hardening Checklist (Implemented)
4.1 User Account Security
Step 1: Review existing users

Command:

cat /etc/passwd


Purpose:

Lists all users in the system

Finding:

Identified default users and system accounts

Step 2: Remove unused users

Command:

sudo deluser username


Purpose:

Removes unnecessary accounts to reduce attack surface

Step 3: Restrict sudo access

Command:

sudo visudo


Configured:

Only authorized admin users allowed sudo access

Principle Applied:
Least Privilege Principle

4.2 Root Account Security
Step 4: Disable root login via SSH

Edit SSH config file:

sudo nano /etc/ssh/sshd_config


Change:

PermitRootLogin no


Restart SSH:

sudo systemctl restart ssh


Result:

Prevents direct root login attacks

4.3 SSH Hardening
Step 5: Enable SSH key-based authentication

Generate key:

ssh-keygen


Copy key:

ssh-copy-id user@server_ip


Disable password login:

PasswordAuthentication no


Benefit:

Protects against brute force attacks

4.4 System Updates and Patch Management
Step 6: Update system packages

Command:

sudo apt update && sudo apt upgrade -y


Purpose:

Fix security vulnerabilities

Step 7: Enable automatic security updates

Install:

sudo apt install unattended-upgrades


Enable:

sudo dpkg-reconfigure unattended-upgrades


Benefit:

Automatically installs security patches

4.5 Firewall Configuration
Step 8: Enable UFW firewall

Command:

sudo ufw enable


Allow SSH only:

sudo ufw allow ssh


Check status:

sudo ufw status


Result:

Blocks unauthorized network access

4.6 Network Port Security
Step 9: Check open ports

Command:

sudo netstat -tulnp


OR

ss -tulnp


Result:

Identified active services and open ports

4.7 Disable Unnecessary Services
Step 10: List running services

Command:

systemctl list-units --type=service


Disable unwanted services:

sudo systemctl disable service_name
sudo systemctl stop service_name


Benefit:

Reduces attack surface

4.8 File Permission Hardening
Step 11: Secure sensitive files

Example:

sudo chmod 600 /etc/shadow
sudo chmod 644 /etc/passwd


Purpose:

Protect password and system files

4.9 Log Monitoring and Auditing
Step 12: Check authentication logs

Command:

sudo cat /var/log/auth.log


Purpose:

Detect unauthorized login attempts

4.10 Security Audit using Lynis Tool

Install Lynis:

sudo apt install lynis


Run audit:

sudo lynis audit system


Result:

Identified vulnerabilities and recommendations

Example Output:

Hardening index: 75/100

Recommendations provided for further improvements

5. Security Configuration Summary
Security Area	Configuration Applied	Status
User Accounts	Removed unused users	Secured
Root Login	Disabled	Secured
SSH Security	Key-based authentication enabled	Secured
Password Login	Disabled	Secured
Firewall	Enabled and configured	Secured
System Updates	Automatic updates enabled	Secured
Open Ports	Reviewed and restricted	Secured
Services	Disabled unnecessary services	Secured
File Permissions	Secured sensitive files	Secured
Logs	Monitoring enabled	Secured
Security Audit	Lynis audit performed	Secured
6. CIS Benchmark Security Controls Applied

The following CIS controls were implemented:

CIS Control 4: Secure Configuration of Servers

CIS Control 5: Account Management

CIS Control 6: Access Control Management

CIS Control 7: Continuous Vulnerability Management

CIS Control 8: Audit Log Management

Reference:
CIS Ubuntu Benchmark
https://www.cisecurity.org/cis-benchmarks/

7. Security Improvements Achieved

Before Hardening:

Root login allowed

Password authentication enabled

Firewall disabled

Unnecessary services running

After Hardening:

Root login disabled

SSH secured with key authentication

Firewall enabled

Attack surface reduced

System fully updated

Unauthorized access prevented

8. Final Outcome

After implementing Linux hardening techniques, the system is now protected against:

Brute force attacks

Unauthorized login attempts

Privilege escalation attacks

Network-based attacks

Malware exploitation

The system is now compliant with industry security standards such as CIS Benchmarks.

9. Conclusion

Linux server hardening is a critical step in cybersecurity. By implementing secure authentication, firewall protection, system updates, and monitoring mechanisms, the server becomes significantly more secure.

This task successfully improved the security posture of the Linux system and reduced vulnerabilities.
