# Ticket 007 - Red Foundation Enterprise File Server

## Objective

Design and implement an enterprise Linux file server for the Red Foundation that uses Role-Based Access Control (RBAC) through Linux users, groups, ownership, and permissions. The goal was to simulate how an organization manages secure access to shared departmental resources.

---

# Environment

- Microsoft Azure Virtual Machine
- Ubuntu Server 24.04 LTS
- Bash
- SSH
- GitHub
- VS Code

---

# Business Scenario

The Red Foundation has expanded into multiple departments. Each department requires a dedicated workspace that is accessible only to authorized personnel while allowing leadership to oversee all departments.

Departments:

- IT
- HR
- Finance
- Volunteers
- Leadership

---

# Phase 1 - Enterprise Directory Structure

Created the enterprise directory structure under the Linux root filesystem.

```bash
sudo mkdir -p /RedFoundation/{IT,HR,Finance,Volunteers,Leadership}
```

Why:

The file server belongs to the organization rather than an individual user's home directory.

---

# Phase 2 - Department Groups

Created Linux security groups for each department.

Commands used:

```bash
sudo groupadd IT
sudo groupadd HR
sudo groupadd Finance
sudo groupadd Volunteers
sudo groupadd Leadership
```

Verified group creation using:

```bash
getent group
```

---

# Phase 3 - Department Users

Created department administrator accounts.

Users created:

- itadmin
- hrmanager
- financeadmin
- volunteerlead
- leadershipadmin

Commands used:

```bash
sudo adduser
```

Each user automatically received:

- Home directory
- Private group
- User ID (UID)

---

# Phase 4 - Department Membership

Assigned users to their department groups.

Commands used:

```bash
sudo usermod -aG
```

Examples:

```bash
sudo usermod -aG IT itadmin
sudo usermod -aG HR hrmanager
sudo usermod -aG Finance financeadmin
sudo usermod -aG Volunteers volunteerlead
sudo usermod -aG Leadership leadershipadmin
```

Verified membership using:

```bash
groups username
```

---

# Phase 5 - Department Folder Ownership

Assigned each department folder to the corresponding Linux group.

Commands used:

```bash
sudo chgrp
```

Examples:

```bash
sudo chgrp IT /RedFoundation/IT
sudo chgrp HR /RedFoundation/HR
sudo chgrp Finance /RedFoundation/Finance
sudo chgrp Volunteers /RedFoundation/Volunteers
sudo chgrp Leadership /RedFoundation/Leadership
```

Owner remained:

```text
root
```

Department access was controlled through group ownership.

---

# Phase 6 - Department Permissions

Configured least-privilege permissions.

Permissions applied:

```bash
sudo chmod 770
```

Permission Breakdown

```text
770

Owner
rwx

Group
rwx

Others
---
```

Result:

- Department members have full access.
- Unauthorized users have no access.

---

# Phase 7 - Leadership Access

Business Requirement:

Leadership requires access to every department without weakening security.

Solution:

Added the leadership administrator to every department group.

Command:

```bash
sudo usermod -aG IT,HR,Finance,Volunteers,Leadership leadershipadmin
```

Reason:

Using Linux group membership follows enterprise Role-Based Access Control (RBAC) principles and avoids modifying permissions on every directory.

---

# Phase 8 - Department Structure

Created realistic departmental folders.

IT

- Scripts
- Documentation
- Backups

HR

- Employee-Records
- Hiring
- Policies

Finance

- Budgets
- Donations
- Payroll

Volunteers

- Event-Plans
- Schedules
- Training

Leadership

- Board-Meetings
- Strategy
- Annual-Reports

Commands:

```bash
sudo mkdir -p
```

Applied permissions recursively using:

```bash
sudo chgrp -R
sudo chmod -R
```

---

# Phase 9 - Access Validation

Validated department isolation.

Testing completed:

✅ HR accessed HR directory

✅ HR denied access to Finance

✅ Finance accessed Finance directory

✅ Finance denied access to HR

✅ Leadership successfully accessed all departments

Verified using:

```bash
whoami
groups
cd
touch
rm
```

---

# Linux Commands Practiced

```bash
mkdir
mkdir -p
groupadd
adduser
usermod
groups
whoami
chgrp
chmod
find
touch
rm
su
```

---

# Linux Concepts Learned

- Enterprise directory structure
- Linux users
- Linux groups
- Role-Based Access Control (RBAC)
- Least Privilege
- Recursive permissions
- Shared departmental resources
- User verification
- Permission validation
- Group-based authorization

---

# Challenges Encountered

- Corrected `chgrp` command syntax.
- Learned the difference between `chown` and `chgrp`.
- Corrected `usermod` syntax for multiple groups.
- Understood recursive (`-R`) permission changes.
- Interpreted "Permission denied" as successful enforcement of access controls rather than an error.

---

# Outcome

Successfully designed and implemented an enterprise Linux departmental file server that enforces role-based access control using Linux users, groups, ownership, and permissions. Verified secure separation between departments while providing leadership with organization-wide access through group membership.

---

# Skills Demonstrated

- Linux System Administration
- Ubuntu Server
- User & Group Administration
- Linux File Permissions
- Role-Based Access Control (RBAC)
- Enterprise File Server Design
- Bash
- SSH
- Azure Virtual Machines
- Identity & Access Management (IAM)
- Principle of Least Privilege