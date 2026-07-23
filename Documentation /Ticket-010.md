# Ticket 010 – Enterprise Linux Monitoring & Troubleshooting

## Objective

Learn how to monitor the health of an enterprise Linux server, investigate performance issues, troubleshoot services, analyze logs, monitor processes, and diagnose network connectivity using standard Linux administration tools.

---

## Business Scenario

The Red Foundation's Linux server is now running in production. Employees depend on the server daily to access files, automate backups, and perform organizational tasks.

As the Linux Systems Administrator, my responsibility is to proactively monitor the server and investigate issues before making changes.

---

## Environment

- **Platform:** Microsoft Azure
- **Operating System:** Ubuntu Linux
- **Server Role:** Enterprise File Server

---

# Phase 1 – System Health Monitoring

## Checking Server Uptime

Command:

```bash
uptime
```

Learned how to interpret:

- Current system time
- Server uptime
- Number of logged-in users
- Load average

### Key Concept

The load average represents how much work the CPU is handling over the last:

- 1 minute
- 5 minutes
- 15 minutes

A consistently high load average may indicate CPU bottlenecks or excessive workload.

---

## Monitoring Memory

Command:

```bash
free -h
```

Learned the difference between:

| Field | Purpose |
|--------|----------|
| Total | Installed RAM |
| Used | RAM currently in use |
| Free | Completely unused RAM |
| Available | RAM immediately available for applications |
| Swap | Emergency memory stored on disk |

### Key Concept

Linux intentionally uses RAM for caching.

Low **Free** memory is not necessarily a problem.

Administrators monitor **Available** memory rather than Free memory.

---

## Monitoring Disk Usage

Command:

```bash
df -h
```

Learned:

- Total disk capacity
- Used storage
- Available storage
- Disk utilization percentage

### Key Concept

High disk usage should trigger investigation rather than immediate file deletion.

---

## Finding Large Directories

Command:

```bash
du -sh /Redfoundation/*
```

Learned:

- `du` = Disk Usage
- `-s` = Summary
- `-h` = Human-readable

Used to identify which directories consume the most storage.

---

# Phase 2 – Service Management

Learned how Linux services are managed using **systemctl**.

Checked service status:

```bash
systemctl status ssh
```

Started services:

```bash
sudo systemctl start <service>
```

Restarted services:

```bash
sudo systemctl restart <service>
```

Enabled services during boot:

```bash
sudo systemctl enable <service>
```

### Services Discussed

- SSH
- Cron
- XRDP

---

# Phase 3 – Log Investigation

Learned to use the Linux journal.

View logs:

```bash
journalctl
```

View recent logs:

```bash
journalctl -n 20
```

View service-specific logs:

```bash
journalctl -u ssh
```

```bash
journalctl -u cron
```

### Key Concept

Logs should be filtered to investigate only the service related to the reported issue.

Examples:

- SSH issue → SSH logs
- Backup issue → Cron logs

---

# Phase 4 – Process Monitoring

Installed:

```bash
sudo apt install htop -y
```

Launched:

```bash
htop
```

Learned to monitor:

- CPU Usage
- RAM Usage
- Swap Usage
- Running Processes

### Key Concept

`htop` serves as Linux's equivalent to Windows Task Manager.

---

# Phase 5 – Process Management

Listed running processes:

```bash
ps
```

Detailed process listing:

```bash
ps -ef
```

Learned important columns:

| Column | Meaning |
|----------|----------|
| UID | User |
| PID | Process ID |
| PPID | Parent Process ID |
| STIME | Start Time |
| CMD | Executed Command |

---

## Finding Processes

Command:

```bash
pgrep ssh
```

Learned:

- `pgrep` = Process Grep
- Used to locate Process IDs by process name.

---

## Stopping Processes

Graceful termination:

```bash
kill PID
```

Force termination:

```bash
kill -9 PID
```

### Key Concept

Normal `kill` sends **SIGTERM**, allowing applications to shut down gracefully.

`kill -9` sends **SIGKILL**, immediately terminating the process without cleanup.

---

# Phase 6 – Network Diagnostics

## Viewing Network Interfaces

Command:

```bash
ip addr
```

Used to identify the server's IP address.

---

## Viewing Routing Table

Command:

```bash
ip route
```

Learned how Linux determines where network traffic is sent.

---

## Connectivity Testing

Command:

```bash
ping google.com
```

Verified outbound network connectivity.

Confirmed the VM currently has internet access.

---

## Viewing Listening Ports

Command:

```bash
ss -tuln
```

Later expanded to:

```bash
sudo ss -tulpn
```

Learned to identify:

- Listening ports
- Associated processes
- Process IDs
- Owning users

Observed services including:

- SSH (Port 22)
- XRDP (Port 3389)
- DNS (Port 53)
- CUPS Printing (Port 631)
- XRDP Session Manager (`xrdp-sesman`)

---

# Enterprise Troubleshooting Workflow

Developed a structured troubleshooting methodology:

```
Problem Reported

↓

Gather Information

↓

Check System Health

↓

Check Services

↓

Review Logs

↓

Investigate Processes

↓

Investigate Network

↓

Determine Root Cause

↓

Implement Fix

↓

Verify Resolution
```

---

# Enterprise Concepts Learned

## System Monitoring

- CPU Monitoring
- Memory Monitoring
- Swap Monitoring
- Disk Monitoring

---

## Service Management

- SSH
- Cron
- XRDP
- Service Status
- Restarting Services

---

## Logging

- Linux Journal
- Filtering Logs
- Service-specific Logs

---

## Process Management

- Process IDs
- Parent Processes
- Graceful Termination
- Forced Termination

---

## Networking

- IP Addressing
- Routing
- Connectivity Testing
- Listening Ports
- Service Verification

---

# Skills Demonstrated

- Linux System Administration
- Linux Monitoring
- Enterprise Troubleshooting
- Service Management
- Process Management
- Log Analysis
- Network Diagnostics
- Performance Investigation
- Memory Analysis
- Disk Analysis
- CPU Monitoring
- PID Management
- Bash Command Line

---

# Commands Used

```bash
uptime
free -h
df -h
du -sh
systemctl
journalctl
journalctl -u
journalctl -n
htop
ps
ps -ef
pgrep
kill
kill -9
ip addr
ip route
ping
ss -tuln
ss -tulpn
```

---

# Key Takeaways

- Learned how to monitor overall Linux server health.
- Developed a structured troubleshooting methodology before making system changes.
- Investigated services using `systemctl`.
- Filtered system logs using `journalctl`.
- Monitored running processes with `htop`.
- Managed Linux processes using `ps`, `pgrep`, and `kill`.
- Diagnosed network connectivity using `ip`, `ping`, and `ss`.
- Connected Linux monitoring concepts with Azure networking, including NSGs, SSH (Port 22), and RDP (Port 3389).
- Built practical enterprise troubleshooting skills that mirror real-world Linux Systems Administration.