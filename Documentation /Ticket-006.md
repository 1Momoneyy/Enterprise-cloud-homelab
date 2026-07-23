# Ticket 006 - Linux Administration Fundamentals

## Objective

Develop foundational Linux system administration skills by configuring and managing an Ubuntu Server virtual machine hosted in Microsoft Azure. This ticket focused on understanding Linux file systems, user management, permissions, ownership, and enterprise access control concepts.

---

# Environment

- Microsoft Azure Virtual Machine
- Ubuntu Server 24.04 LTS
- SSH
- Bash
- VS Code
- GitHub

---

# Tasks Completed

## Filesystem Navigation

Practiced navigating the Linux filesystem using:

```bash
pwd
ls
ls -l
cd
```

Learned:

- Root directory (`/`)
- Home directory (`~`)
- Current directory (`.`)
- Parent directory (`..`)
- Absolute vs Relative paths

---

## File & Directory Management

Created and managed files and directories using:

```bash
mkdir
touch
nano
cat
rm
rmdir
```

Created a Linux administration lab containing scripts and documentation for future automation exercises.

---

## User Management

Created a new administrative user:

```text
itadmin
```

Learned:

```bash
whoami
groups
adduser
su
su -
```

Verified user sessions and compared the behavior of `su` and `su -`.

---

## Linux Permissions

Learned symbolic permissions:

```text
r = Read
w = Write
x = Execute
```

Modified permissions using:

```bash
chmod
```

Examples:

```bash
chmod u+x backup.sh
chmod g+w /shared-it
```

---

## Numeric Permissions

Learned how Linux calculates permissions.

| Permission | Value |
|------------|------:|
| Read | 4 |
| Write | 2 |
| Execute | 1 |

Examples:

| Number | Permissions |
|---------|-------------|
| 755 | rwxr-xr-x |
| 750 | rwxr-x--- |
| 644 | rw-r--r-- |

---

## Ownership

Learned Linux ownership concepts.

Commands used:

```bash
chown
chgrp
```

Practiced transferring ownership and changing group ownership of files and directories.

---

## Groups

Created Linux groups using:

```bash
groupadd
```

Added users to groups using:

```bash
usermod -aG
```

Configured an enterprise IT department group for shared access.

---

## Enterprise Shared Folder

Created a shared company directory.

```text
/shared-it
```

Configured:

- Owner
- Group
- Permissions

Verified access by logging in as the **itadmin** user and successfully creating files inside the shared directory.

---

# Concepts Learned

- Linux filesystem hierarchy
- File ownership
- User accounts
- Groups
- Least Privilege
- Enterprise access control
- Shared directories
- Symbolic permissions
- Numeric permissions

---

# Commands Practiced

```bash
pwd
ls
ls -l
cd
mkdir
touch
nano
cat
rm
rmdir
chmod
chown
chgrp
groupadd
usermod
whoami
groups
su
```

---

# Outcome

Successfully configured and administered an Ubuntu Linux server using enterprise administration principles. Implemented user management, group management, file ownership, Linux permissions, and shared resource access while documenting each configuration for future reference.

---

# Skills Demonstrated

- Linux Administration
- Bash
- File System Management
- User & Group Administration
- Linux Permissions
- Enterprise Access Control
- Azure Virtual Machines
- SSH Remote Administration