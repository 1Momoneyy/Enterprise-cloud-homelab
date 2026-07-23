# Ticket 011 – Enterprise Disaster Recovery & Backup Restoration

## Objective

Validate the organization's backup strategy by simulating a production data loss event, restoring the Finance department from compressed backup archives, verifying data integrity, and safely returning the recovered data back into production.

---

## Business Scenario

The Finance department accidentally deleted its entire shared directory containing payroll, budgets, and financial records.

As the Linux Systems Administrator, my responsibility was to:

- Verify backups existed.
- Confirm backup integrity.
- Restore data into a recovery environment.
- Validate recovered files.
- Restore the department back into production.
- Minimize business downtime and data loss.

---

## Environment

- **Platform:** Microsoft Azure
- **Operating System:** Ubuntu Linux
- **Department:** Finance
- **Backup Location:** `/Redfoundation/Backups/Finance`

---

# Phase 1 – Backup Verification

Verified available backups before beginning recovery.

```bash
ls -lh /Redfoundation/Backups/Finance
```

Confirmed multiple backup archives existed.

Example:

```
Finance_Backup_2026-07-18_17-45-1784396730.tar.gz

Finance_Backup_2026-07-18_17-51-1784397069.tar.gz
```

### Key Concept

Never begin a recovery operation without first verifying that a valid backup exists.

---

# Phase 2 – Backup Inspection

Inspected the backup archive before restoring.

```bash
tar -tzf /Redfoundation/Backups/Finance/Finance_Backup_2026-07-18_17-51-1784397069.tar.gz
```

### Learned

`tar -t`

Displays the contents of an archive without extracting it.

Verified the archive contained:

```
Redfoundation/
Redfoundation/Finance/
Budget2027.xlsx
Budget2029.xlsx
Budget2030.xlsx
payroll2027.xlsx
```

### Key Concept

Enterprise administrators inspect backups before restoring them to ensure the correct files exist and the archive is valid.

---

# Phase 3 – Simulating Disaster

Verified the Finance directory existed.

```bash
ls -l /Redfoundation
```

Simulated a production disaster by deleting the Finance department.

```bash
sudo rm -rf /Redfoundation/Finance
```

### Key Concept

Linux's `rm -rf` permanently deletes data.

Unlike Windows, Linux does not move deleted files to a Recycle Bin.

Recovery depends entirely on backups.

---

# Phase 4 – Recovery Environment

Created a recovery environment.

```bash
sudo mkdir -p /Redfoundation/Recovery_Test
```

### Purpose

Never restore directly into production.

Always restore into a safe testing location first.

---

# Phase 5 – Backup Restoration

Extracted the archive into the recovery environment.

```bash
sudo tar -xzf /Redfoundation/Backups/Finance/Finance_Backup_2026-07-18_17-51-1784397069.tar.gz -C /Redfoundation/Recovery_Test
```

### New Flags Learned

| Flag | Purpose |
|-------|----------|
| x | Extract archive |
| C | Change directory before extracting |

---

# Phase 6 – Recovery Verification

Verified the restored files.

```bash
sudo ls -R /Redfoundation/Recovery_Test
```

Recovered directory structure:

```
Recovery_Test
└── Redfoundation
    └── Finance
        ├── Budget2027.xlsx
        ├── Budget2029.xlsx
        ├── Budget2030.xlsx
        └── payroll2027.xlsx
```

### Key Concept

Validate restored data before returning it to production.

---

# Phase 7 – Production Restoration

Restored the verified Finance directory back into production.

```bash
sudo cp -r /Redfoundation/Recovery_Test/Redfoundation/Finance /Redfoundation/
```

Verified successful restoration.

```bash
ls -R /Redfoundation/Finance
```

Confirmed all files were successfully restored.

---

# Recovery Strategy

The disaster recovery workflow followed enterprise best practices.

```
Verify Backup

↓

Inspect Archive

↓

Create Recovery Environment

↓

Restore Backup

↓

Verify Restored Files

↓

Restore to Production

↓

Verify Production Environment
```

---

# Recovery Objectives

## Recovery Time Objective (RTO)

Measures:

> How long it takes to restore business operations.

Example:

A complete Finance restoration completed within the organization's recovery window.

---

## Recovery Point Objective (RPO)

Measures:

> How much data can be lost between backups.

Example:

If backups occur daily at 2:00 AM and the disaster occurs at 5:00 PM:

Potential data loss:

```
Approximately 15 hours
```

Improving RPO:

- Increase backup frequency.
- Automate backups every hour or every few hours based on business requirements.
- Store older backups in Azure Blob Storage or other long-term storage solutions.

---

# Enterprise Concepts Learned

## Backup Validation

Verify backups before initiating recovery.

---

## Disaster Recovery

Recover deleted business data using verified backup archives.

---

## Recovery Testing

Restore into a recovery environment before modifying production systems.

---

## Data Integrity

Confirm recovered files match the original backup.

---

## Recovery Objectives

- Recovery Time Objective (RTO)
- Recovery Point Objective (RPO)

---

# Skills Demonstrated

- Enterprise Disaster Recovery
- Linux Backup Restoration
- Backup Validation
- Recovery Verification
- Data Integrity Verification
- Linux Archive Management
- `tar`
- Backup Inspection
- Disaster Recovery Planning
- Recovery Time Objective (RTO)
- Recovery Point Objective (RPO)
- Enterprise File Recovery
- Linux Administration

---

# Commands Used

```bash
ls -lh
tar -tzf
tar -xzf
mkdir -p
rm -rf
cp -r
ls -R
```

---

# Key Takeaways

- Successfully simulated a production data loss event.
- Validated backup archives before beginning recovery.
- Restored compressed backups into an isolated recovery environment.
- Verified recovered files before restoring production data.
- Successfully returned the Finance department back into production.
- Learned enterprise disaster recovery workflows and best practices.
- Developed an understanding of Recovery Time Objective (RTO) and Recovery Point Objective (RPO) for business continuity planning.
```