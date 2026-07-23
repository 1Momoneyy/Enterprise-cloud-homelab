# Ticket 008 – Enterprise File Collaboration & Secure File Permissions

## Objective

Configure an enterprise-style Linux file server that supports secure collaboration between department members by implementing Role-Based Access Control (RBAC), SGID, least privilege permissions, and secure default file creation using `umask`.

---

## Business Scenario

The Red Foundation has begun using its Linux file server for daily operations. Multiple employees within each department need to collaborate on shared files while ensuring sensitive data remains secure.

As the Linux Systems Administrator, my responsibility was to configure the file system so that:

- Department members can collaborate on shared files.
- Files inherit the correct department ownership.
- Default permissions follow the Principle of Least Privilege.
- New files are created securely without requiring manual permission changes.

---

## Environment

- **Platform:** Microsoft Azure
- **Operating System:** Ubuntu Linux
- **Server Role:** Enterprise Department File Server

---

# Phase 1 – Investigating Default File Ownership

Logged in as the Finance administrator and created a test file.

```bash
su - financeadmin
cd /RedFoundation/Finance
touch Budget2027.xlsx
ls -l
```

### Initial Result

```
Owner: financeadmin
Group: financeadmin
```

### Discovery

Linux assigns:

- The **owner** as the user creating the file.
- The **group** as the user's primary group.

This created a collaboration issue because files were not automatically assigned to the shared Finance department group.

---

# Phase 2 – Configuring SGID

Enabled the Set Group ID (SGID) bit on the Finance directory.

```bash
sudo chmod g+s /RedFoundation/Finance
```

Verified the configuration:

```bash
ls -ld /RedFoundation/Finance
```

Output:

```
drwxrws---
```

The **s** indicates that SGID is enabled.

### Result

Any new file created inside the Finance directory automatically inherits the **Finance** group instead of the creator's primary group.

---

# Phase 3 – Testing SGID

Created another file after enabling SGID.

```bash
touch Budget2029.xlsx
ls -l
```

Result:

```
Owner: financeadmin
Group: Finance
```

This confirmed that shared departmental files now inherit the correct group automatically.

---

# Phase 4 – Applying Least Privilege

Updated file permissions to restrict access.

```bash
chmod 660 Budget2029.xlsx
```

Verified:

```bash
ls -l Budget2029.xlsx
```

Result:

```
-rw-rw----
```

Permission Breakdown

| User | Permission |
|------|------------|
| Owner | Read / Write |
| Finance Group | Read / Write |
| Others | No Access |

This follows the Principle of Least Privilege by granting only the permissions required for collaboration.

---

# Phase 5 – Multi-User Collaboration

Created a second Finance employee.

```bash
sudo adduser financeassistant
sudo usermod -aG Finance financeassistant
```

Verified group membership:

```bash
groups financeassistant
```

Logged in as the new user.

```bash
su - financeassistant
cd /RedFoundation/Finance
```

Successfully modified the shared Finance document.

```bash
echo "Reviewed by Finance Assistant" >> Budget2029.xlsx
```

Verified:

```bash
cat Budget2029.xlsx
```

The modification succeeded without changing ownership or permissions.

---

# Phase 6 – Understanding umask

Learned that Linux applies default permissions to all newly created files and directories.

Default permissions:

Files

```
666
```

Directories

```
777
```

The **umask** removes permissions from these defaults.

Examples:

| Default | umask | Result |
|----------|--------|--------|
| 666 | 022 | 644 |
| 666 | 007 | 660 |
| 777 | 002 | 775 |

---

# Phase 7 – Configuring umask

Checked the current umask.

```bash
umask
```

Configured a more secure default.

```bash
umask 007
```

Verified:

```bash
umask
```

Created a new file and confirmed it inherited secure permissions by default.

Result:

```
660
```

This eliminates the need to manually run `chmod` after every file creation.

---

# Skills Demonstrated

- Linux File Ownership
- Linux Group Management
- Role-Based Access Control (RBAC)
- SGID Configuration
- Linux File Permissions
- Numeric Permissions
- Principle of Least Privilege
- Multi-User File Collaboration
- Linux `umask`
- Linux Security Administration
- Bash Command Line

---

# Commands Used

```bash
su
cd
touch
ls -l
ls -ld
chmod
groups
cat
echo
usermod
adduser
umask
```

---

# Key Takeaways

- Implemented enterprise Role-Based Access Control using Linux groups.
- Configured SGID so shared files automatically inherit the department group.
- Applied least privilege permissions using `chmod`.
- Validated secure collaboration between multiple department users.
- Configured `umask` to ensure newly created files follow secure default permissions.
- Built a production-style Linux departmental file server that mirrors enterprise administration practices.