# Ticket 012 – Enterprise Linux Security Hardening

## Objective

Harden an enterprise Ubuntu Linux server by implementing security best practices including user auditing, SSH hardening, firewall configuration, brute-force protection, and security validation.

---

# Business Scenario

The Red Foundation is preparing for an annual security audit.

As the Linux Systems Administrator, my responsibility was to secure the production server before the compliance assessment by reducing the attack surface, enforcing least privilege, and implementing multiple layers of defense.

---

# Environment

- Platform: Microsoft Azure
- Operating System: Ubuntu Server 24.04 LTS
- Security Tools:
  - UFW
  - Fail2Ban
  - OpenSSH

---

# Phase 1 – User Audit

Reviewed all local user accounts.

```bash
cat /etc/passwd
```

Identified project-created administrative and departmental accounts while distinguishing them from Linux system accounts.

### Accounts Identified

- Mohamed
- financeadmin
- financeassistant
- hrmanager
- volunteerlead
- leadershipadmin
- itadmin

---

# Phase 2 – Administrative Privilege Audit

Verified members of the sudo group.

```bash
getent group sudo
```

Result:

Only the Linux administrator account possessed administrative privileges.

### Security Principle

Implemented **Least Privilege**, ensuring users receive only the permissions required to perform their job functions.

---

# Phase 3 – SSH Security Review

Reviewed SSH daemon configuration.

```bash
sudo nano /etc/ssh/sshd_config
```

Inspected:

- PermitRootLogin
- PasswordAuthentication
- PubkeyAuthentication

Learned that lines beginning with:

```text
#
```

are comments and are ignored by SSH.

---

# Phase 4 – SSH Hardening

Configured SSH to reduce attack surface.

Implemented:

```text
PermitRootLogin no
PasswordAuthentication no
PubkeyAuthentication yes
```

### Security Improvements

- Disabled direct root login.
- Disabled password authentication.
- Enforced SSH key authentication.

---

# Enterprise Concepts Learned

## SSH Key Authentication

Public-key authentication significantly reduces brute-force attacks because users authenticate with a private key rather than a password.

---

## Root Account Protection

Administrators authenticate using individual user accounts before elevating privileges with:

```bash
sudo
```

Benefits:

- Accountability
- Auditing
- Reduced attack surface

---

# Phase 5 – Linux Firewall

Verified firewall status.

```bash
sudo ufw status verbose
```

Result:

Firewall inactive.

Allowed SSH access.

```bash
sudo ufw allow OpenSSH
```

Enabled firewall.

```bash
sudo ufw enable
```

Verified configuration.

```bash
sudo ufw status verbose
```

Result:

- Firewall Active
- Logging Enabled
- Default Incoming Policy: Deny
- Default Outgoing Policy: Allow

---

# Enterprise Concepts Learned

## Defense in Depth

Implemented multiple security layers.

```text
Internet
      │
Azure NSG
      │
Ubuntu UFW
      │
SSH
```

Even if one layer fails, another layer continues protecting the server.

---

## Default Deny

Configured the firewall to deny all inbound traffic except explicitly permitted services.

This follows enterprise security best practices.

---

# Phase 6 – Fail2Ban

Installed Fail2Ban.

```bash
sudo apt install fail2ban
```

Verified service status.

```bash
sudo systemctl status fail2ban
```

Result:

```text
active (running)
enabled
```

Verified active jails.

```bash
sudo fail2ban-client status
```

Reviewed SSH jail.

```bash
sudo fail2ban-client status sshd
```

Verified:

- Failed Logins
- Banned IPs
- Active Protection

---

# Enterprise Concepts Learned

## Brute Force Protection

Fail2Ban continuously monitors authentication logs.

Repeated failed login attempts automatically trigger temporary IP bans.

---

# Security Layers Implemented

- User Auditing
- Least Privilege
- SSH Hardening
- Root Login Disabled
- Password Authentication Disabled
- SSH Key Authentication
- UFW Firewall
- Default Deny Policy
- Fail2Ban
- Defense in Depth

---

# Skills Demonstrated

- Linux Security Hardening
- SSH Configuration
- SSH Key Authentication
- User Auditing
- Least Privilege
- UFW Firewall
- Fail2Ban
- Defense in Depth
- Linux Security
- Enterprise System Administration

---

# Commands Used

```bash
cat /etc/passwd
getent group sudo
nano /etc/ssh/sshd_config
ufw status
ufw allow OpenSSH
ufw enable
systemctl status fail2ban
fail2ban-client status
fail2ban-client status sshd
```

---

# Key Takeaways

- Audited enterprise user accounts.
- Enforced least privilege.
- Hardened SSH.
- Disabled root login.
- Enforced SSH key authentication.
- Configured Linux firewall.
- Implemented defense in depth.
- Protected SSH against brute-force attacks using Fail2Ban.
- Prepared the server for enterprise security auditing.