# Ticket 009 – Enterprise Backup Automation with Bash & Cron

## Objective

Design and implement an automated backup solution for the Finance department by creating a production-style Bash script, compressing backups into timestamped archives, and scheduling automatic execution using Cron.

---

## Business Scenario

The Finance department stores critical organizational data on the enterprise Linux file server. Manual backups are unreliable because they depend on users remembering to perform them. As the Linux Systems Administrator, my responsibility was to automate the backup process to ensure Finance data is backed up consistently without human intervention.

---

## Environment

- **Platform:** Microsoft Azure
- **Operating System:** Ubuntu Linux
- **Department:** Finance
- **Backup Location:** `/Redfoundation/Backups/Finance`

---

# Phase 1 – Backup Design

Created a centralized backup location instead of storing backups inside an individual user's home directory.

Created the backup directory:

```bash
sudo mkdir -p /Redfoundation/Backups/Finance
```

### Why?

A centralized backup location:

- Prevents backups from being tied to a specific employee.
- Supports enterprise scalability.
- Keeps organizational data separate from user home directories.
- Simplifies future backup management.

---

# Phase 2 – Creating the Backup Script

Created an administrative scripts directory.

```bash
sudo mkdir -p /Redfoundation/IT/Scripts
```

Created the backup script.

```bash
nano finance_backup.sh
```

Script contents:

```bash
#!/bin/bash

SOURCE="/Redfoundation/Finance"
DESTINATION="/Redfoundation/Backups/Finance"
DATE=$(date +%Y-%m-%d_%H-%M-%S)

mkdir -p "$DESTINATION"

tar -czf "$DESTINATION/Finance_Backup_$DATE.tar.gz" "$SOURCE"
```

Made the script executable.

```bash
chmod 750 finance_backup.sh
```

---

# Phase 3 – Understanding the Script

## Shebang

```bash
#!/bin/bash
```

Specifies that the script should execute using the Bash interpreter.

---

## Variables

Defined reusable variables.

```bash
SOURCE="/Redfoundation/Finance"
```

Directory being backed up.

```bash
DESTINATION="/Redfoundation/Backups/Finance"
```

Location where backups are stored.

```bash
DATE=$(date +%Y-%m-%d_%H-%M-%S)
```

Generates a timestamp used to create unique backup filenames.

Example:

```
2026-07-18_17-51-17
```

---

# Phase 4 – Creating Timestamped Backups

Used:

```bash
tar -czf
```

### Command Breakdown

| Option | Purpose |
|----------|---------|
| c | Create archive |
| z | Compress using gzip |
| f | Output to a file |

Generated backup filenames similar to:

```
Finance_Backup_2026-07-18_17-51-17.tar.gz
```

Benefits:

- Prevents overwriting previous backups.
- Maintains backup history.
- Enables point-in-time recovery.

---

# Phase 5 – Idempotent Directory Creation

Included:

```bash
mkdir -p "$DESTINATION"
```

Purpose:

- Creates the backup directory if it does not exist.
- Does nothing if the directory already exists.
- Allows the script to run repeatedly without failure.

This demonstrates **idempotent scripting**, an important automation principle.

---

# Phase 6 – Troubleshooting

Encountered several issues while testing.

### Relative vs Absolute Paths

Initially used:

```bash
Redfoundation/Finance
```

Corrected to:

```bash
/Redfoundation/Finance
```

Learned the difference between:

- Relative paths
- Absolute paths

---

### Variable Expansion

Initially used:

```bash
mkdir -p "DESTINATION"
```

Corrected to:

```bash
mkdir -p "$DESTINATION"
```

Learned that:

- `$` expands a variable.
- Without `$`, Bash interprets the text literally.

---

### Linux Permissions

Encountered:

```
Permission denied
```

Determined the Finance directory was protected by Role-Based Access Control.

Instead of weakening permissions, executed the backup script using:

```bash
sudo /Redfoundation/IT/Scripts/finance_backup.sh
```

This follows enterprise best practices because backup jobs typically run with elevated privileges.

---

# Phase 7 – Verifying Backups

Executed:

```bash
sudo /Redfoundation/IT/Scripts/finance_backup.sh
```

Verified backup creation:

```bash
sudo ls -lh /Redfoundation/Backups/Finance
```

Successfully created multiple compressed backup archives.

Example:

```
Finance_Backup_2026-07-18_17-32-45.tar.gz
Finance_Backup_2026-07-18_17-51-17.tar.gz
```

---

# Phase 8 – Automating with Cron

Configured a scheduled task using:

```bash
sudo crontab -e
```

Added:

```cron
0 2 * * * /Redfoundation/IT/Scripts/finance_backup.sh
```

### Cron Breakdown

| Field | Meaning |
|---------|---------|
| 0 | Minute |
| 2 | Hour (2 AM) |
| * | Every day of month |
| * | Every month |
| * | Every day of week |

Result:

The backup executes automatically every day at **2:00 AM**.

---

# Additional Cron Examples Learned

Daily at 2 AM

```cron
0 2 * * *
```

Weekdays at 6:30 PM

```cron
30 18 * * 1-5
```

Every 6 hours

```cron
0 */6 * * *
```

Every Sunday at 3 AM

```cron
0 3 * * 0
```

---

# Skills Demonstrated

- Bash Scripting
- Linux Automation
- Shell Variables
- Command Substitution
- Bash Shebang
- Linux Backup Administration
- `tar`
- `gzip`
- Linux File Compression
- Timestamped Backups
- Idempotent Scripting
- Absolute vs Relative Paths
- Variable Expansion
- Linux Permissions
- Privilege Escalation using `sudo`
- Cron Scheduling
- Enterprise Backup Strategy
- Troubleshooting Bash Scripts

---

# Commands Used

```bash
mkdir -p
nano
chmod
tar
date
sudo
ls
ls -lh
crontab -e
cat
```

---

# Key Takeaways

- Built an enterprise backup solution using Bash.
- Created reusable variables for maintainable scripts.
- Generated timestamped compressed backups using `tar`.
- Applied idempotent scripting practices with `mkdir -p`.
- Troubleshot path, variable expansion, and permission issues.
- Implemented automated scheduling with Cron.
- Designed a backup workflow that reflects real-world Linux systems administration and enterprise operational practices.