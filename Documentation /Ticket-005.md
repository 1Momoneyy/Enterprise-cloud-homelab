# Ticket 005 - Initial Linux Configuration & System Updates

**Project:** Azure Linux Administration & Security Homelab  
**Status:** ✅ Completed  
**Date:** July 13, 2026

---

# Objective

Establish secure SSH connectivity to the Azure Ubuntu Server virtual machine from the Windows administration workstation and perform the initial operating system update to ensure the server is running the latest security patches before beginning system hardening.

---

# Environment

| Component | Value |
|-----------|-------|
| Cloud Provider | Microsoft Azure |
| VM Name | vm-linux-management-01 |
| Operating System | Ubuntu Server 24.04 LTS |
| Region | East US 2 |
| Authentication | ED25519 SSH Key |
| Local Administration Workstation | Windows 11 |
| SSH Client | OpenSSH (PowerShell) |

---

# Tasks Completed

## 1. Verified SSH Key

Confirmed the ED25519 private key was successfully copied to the Windows workstation.

Location:

```text
C:\Users\Mohamed\.ssh\Linux-management-key.pem
```

---

## 2. Connected to the Linux Server

Successfully authenticated to the Ubuntu VM using SSH key authentication.

Command:

```bash
ssh -i "$HOME\.ssh\Linux-management-key.pem" Mohamed@20.10.42.142
```

Successful login displayed the Ubuntu welcome screen and command prompt.

---

## 3. Updated Package Repository

Refreshed the package database.

```bash
sudo apt update
```

Purpose:

- Download latest package metadata
- Check for available updates
- Verify internet connectivity

---

## 4. Installed System Updates

Installed all available package updates.

```bash
sudo apt upgrade -y
```

Purpose:

- Apply security patches
- Install bug fixes
- Update installed software
- Prepare the server for production hardening

---

## 5. Verified Remote Administration

Successfully connected from both:

- macOS
- Windows 11

This confirms:

- SSH connectivity
- Public IP accessibility
- Azure Network Security Group configuration
- SSH key authentication

---

# Commands Executed

```bash
ssh -i "$HOME\.ssh\Linux-management-key.pem" Mohamed@20.10.42.142

sudo apt update

sudo apt upgrade -y
```

---

# Skills Demonstrated

- Microsoft Azure
- Ubuntu Linux
- Linux Administration
- Secure Shell (SSH)
- ED25519 Key Authentication
- Package Management (APT)
- Remote Server Administration
- Cloud Infrastructure
- Security Patch Management

---

# Lessons Learned

- Linux servers should always be updated immediately after deployment.
- SSH key authentication is more secure than password authentication.
- `apt update` refreshes repository metadata.
- `apt upgrade` installs the latest available software packages.
- Administrative Linux commands require the `sudo` command.
- Stopping an Azure VM immediately terminates active SSH sessions.

---

# Outcome

The Ubuntu Server was successfully updated and verified to accept secure SSH connections from the Windows administration workstation.

The VM is now ready for security hardening and continued system administration tasks.

---

# Next Ticket

## Ticket 006 - Linux Hardening

Planned objectives:

- Create a dedicated administrative account
- Configure sudo permissions
- Harden SSH configuration
- Configure UFW firewall
- Install and configure Fail2Ban
- Verify secure remote administration

**Status:** Ready to begin.