# Ticket 014 – Enterprise Infrastructure Integration

## Objective

Integrate all enterprise Linux services into a unified production environment by connecting cloud infrastructure, identity management, security, networking, automation, monitoring, backup, and disaster recovery into a cohesive enterprise architecture.

---

# Business Scenario

The Red Foundation has successfully deployed its Linux infrastructure.

Before transitioning the environment to the Operations Team, management requested complete infrastructure integration documentation demonstrating how every enterprise component works together.

As the Linux Systems Administrator, I integrated all previously implemented technologies into a single enterprise environment and documented the operational workflow.

---

# Environment

Platform

- Microsoft Azure

Operating System

- Ubuntu Server 24.04 LTS

Infrastructure Components

- Azure Virtual Machine
- Azure Network Security Group
- Ubuntu Linux
- SSH
- UFW
- Fail2Ban
- Cron
- Bash
- Lynis

---

# Enterprise Architecture

```text
                    Internet
                         │
                         ▼
          Azure Network Security Group
                         │
                         ▼
                Ubuntu Linux VM
                         │
     ┌───────────────────┼───────────────────┐
     ▼                   ▼                   ▼
 Authentication      Departments        System Services
     │                   │                   │
     ▼                   ▼                   ▼
 SSH Keys          Finance             SSH
 Fail2Ban          HR                  Cron
 UFW               Leadership          rsyslog
 RBAC              Volunteers          Monitoring
 ACLs              IT
                         │
                         ▼
                 Automated Backups
                         │
                         ▼
                 Disaster Recovery
                         │
                         ▼
                 Security Auditing
```

---

# Infrastructure Components

## Cloud Infrastructure

Deployed an Ubuntu Server virtual machine within Microsoft Azure.

Implemented:

- Azure Virtual Machine
- Azure Network Security Group
- Secure SSH Access

The Azure Network Security Group acts as the first layer of network security by filtering inbound traffic before it reaches the Linux server.

---

## Identity & Access Management

Implemented enterprise identity management through:

- Linux Users
- Linux Groups
- Role-Based Access Control (RBAC)
- Access Control Lists (ACLs)

Departments Created

- Finance
- HR
- Leadership
- Volunteers
- IT

Implemented Least Privilege by restricting access to only the resources required for each department.

---

## Department Resources

Created business departments representing a real enterprise environment.

### Finance

- Payroll
- Budgets
- Financial Reports

### HR

- Employee Records
- Benefits
- Recruiting
- Policies

### Leadership

- Executive
- Strategy
- Board Meetings
- Annual Reports

### Volunteers

- Applications
- Training
- Events
- Schedules

### IT

- Scripts
- Documentation
- Logs
- Monitoring

---

## Linux Administration

Performed enterprise administration tasks including:

- User Management
- Group Management
- Permissions
- ACL Management
- Process Monitoring
- Service Management
- System Monitoring
- Log Analysis

Tools Used

- systemctl
- ps
- htop
- journalctl
- ss
- ping
- traceroute

---

## Automation

Implemented administrative automation using:

- Bash Scripts
- Cron Jobs

Automated:

- Backup Operations
- Scheduled Administrative Tasks

---

## Backup Strategy

Implemented automated backup management.

Created compressed backup archives using:

```bash
tar
```

Stored backups in a dedicated repository.

Validated backup integrity before restoration.

---

## Disaster Recovery

Performed complete disaster recovery testing.

Recovery Workflow

```text
Backup

↓

Validate Archive

↓

Recovery Environment

↓

Verify Data

↓

Restore Production

↓

Validate Production
```

Business Continuity Concepts

- Recovery Time Objective (RTO)
- Recovery Point Objective (RPO)

---

## Security Hardening

Implemented multiple layers of security.

Configured

- SSH Hardening
- SSH Key Authentication
- Disabled Root Login
- Disabled Password Authentication
- UFW Firewall
- Fail2Ban

Security Architecture

```text
Internet

↓

Azure NSG

↓

Ubuntu Firewall

↓

SSH

↓

Fail2Ban

↓

Linux Authentication
```

Implemented Defense in Depth through layered security controls.

---

## Security Auditing

Performed enterprise security auditing using Lynis.

Workflow

```text
Audit

↓

Identify Findings

↓

Patch Vulnerabilities

↓

Re-Audit

↓

Validate Improvements
```

Successfully improved system hardening after vulnerability remediation.

---

# Enterprise Operational Workflow

```text
Deploy Infrastructure

↓

Configure Networking

↓

Create Users

↓

Implement RBAC

↓

Configure Storage

↓

Secure SSH

↓

Configure Firewall

↓

Implement Fail2Ban

↓

Automate Backups

↓

Test Disaster Recovery

↓

Perform Security Audit

↓

Patch Vulnerabilities

↓

Validate Improvements
```

---

# Technologies Used

## Cloud

- Microsoft Azure
- Azure Virtual Machine
- Azure Network Security Group

## Linux

- Ubuntu Server
- Users
- Groups
- RBAC
- ACLs
- Permissions

## Networking

- SSH
- TCP/IP
- DNS
- UFW

## Security

- Fail2Ban
- SSH Hardening
- Lynis
- Least Privilege

## Automation

- Bash
- Cron

## Backup & Recovery

- tar
- Disaster Recovery
- Backup Validation

---

# Skills Demonstrated

- Enterprise Linux Administration
- Microsoft Azure
- Cloud Infrastructure
- RBAC
- Access Control Lists
- Linux Security
- SSH Administration
- UFW Firewall
- Fail2Ban
- Bash Automation
- Cron Scheduling
- Backup Administration
- Disaster Recovery
- Vulnerability Management
- Infrastructure Integration
- Enterprise Documentation

---

# Commands Used

```bash
systemctl
journalctl
ss
tar
cron
bash
ufw
fail2ban-client
lynis
```

---

# Key Takeaways

- Integrated all Linux administration, networking, automation, backup, disaster recovery, and security components into a unified enterprise environment.
- Implemented layered security using Azure Network Security Groups, UFW, SSH hardening, Fail2Ban, RBAC, and ACLs.
- Connected enterprise departments through role-based access management and realistic business resources.
- Automated backup operations and validated disaster recovery procedures.
- Demonstrated a complete enterprise Linux infrastructure suitable for production deployment.