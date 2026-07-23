# Ticket 013 – Enterprise Security Auditing & Vulnerability Remediation

## Objective

Perform an enterprise Linux security audit, identify security weaknesses, remediate vulnerabilities, and validate security improvements using Lynis.

---

# Business Scenario

Following enterprise security hardening, the Red Foundation required a security assessment before its annual compliance review.

As the Linux Systems Administrator, I performed a complete security audit, analyzed findings, remediated vulnerabilities, and verified improvements through re-auditing.

---

# Environment

- Platform: Microsoft Azure
- Operating System: Ubuntu 24.04 LTS
- Security Auditor:
  - Lynis

---

# Phase 1 – Security Audit Planning

Initially attempted to perform security auditing using OpenSCAP.

Successfully installed:

- OpenSCAP Scanner
- Security Guide packages

While validating installation, discovered Ubuntu 24.04 repositories did not include the required benchmark XML content.

Instead of forcing unsupported packages, verified:

- Package installation
- Repository contents
- Package availability

Pivoted to Lynis as a supported enterprise security auditing solution.

---

# Enterprise Lesson

Troubleshooting included:

- Verifying assumptions
- Investigating package availability
- Validating installation paths
- Adapting to operating system changes

---

# Phase 2 – Install Lynis

Installed Lynis.

```bash
sudo apt install lynis -y
```

---

# Phase 3 – Initial Security Audit

Executed a full enterprise audit.

```bash
sudo lynis audit system
```

Initial Results

```text
Hardening Index: 61
```

Performed approximately:

```text
258 Tests
```

Validated:

- Firewall
- Authentication
- Users
- Services
- Networking
- Kernel
- Logging
- Installed Software

---

# Phase 4 – Review Findings

Extracted recommendations.

```bash
sudo grep "Warning\|Suggestion" /var/log/lynis-report.dat
```

Findings included:

- Repository warning
- Vulnerable packages

Investigated instead of immediately applying changes.

---

# Phase 5 – Validate Findings

Updated repositories.

```bash
sudo apt update
```

Reviewed available updates.

```bash
sudo apt list --upgradable
```

Identified:

```text
12 Upgradable Packages
```

Including:

- Linux Kernel
- PAM
- rsyslog
- Azure packages

---

# Enterprise Concept

Security scanners identify potential vulnerabilities.

Administrators validate findings before applying remediation.

---

# Phase 6 – Patch Management

Applied security updates.

```bash
sudo apt upgrade -y
```

Performed enterprise patch management to reduce system vulnerabilities.

---

# Phase 7 – Validation

Re-ran security audit.

```bash
sudo lynis audit system
```

Final Results

Initial Score

```text
61
```

↓

Final Score

```text
66
```

Security posture successfully improved.

---

# Enterprise Security Workflow

```text
Audit

↓

Identify Findings

↓

Validate Findings

↓

Patch Vulnerabilities

↓

Re-Audit

↓

Verify Improvements
```

---

# Enterprise Concepts Learned

## Security Auditing

Identify weaknesses before attackers do.

---

## Vulnerability Management

- Detect
- Validate
- Prioritize
- Remediate
- Verify

---

## Patch Management

Regularly update operating system packages to reduce exposure to known vulnerabilities.

---

## Continuous Improvement

Security is an ongoing process rather than a one-time configuration.

---

# Skills Demonstrated

- Linux Security Auditing
- Lynis
- Vulnerability Assessment
- Patch Management
- Security Validation
- Linux Package Management
- Enterprise Security
- Security Remediation
- Ubuntu Administration
- Risk Assessment

---

# Commands Used

```bash
apt update
apt list --upgradable
apt upgrade -y
lynis audit system
grep "Warning\|Suggestion"
```

---

# Key Takeaways

- Performed an enterprise Linux security audit.
- Identified security weaknesses.
- Validated audit findings.
- Patched vulnerable software packages.
- Improved system hardening score through remediation.
- Verified improvements by performing a second security audit.
- Demonstrated a complete vulnerability management lifecycle used in enterprise environments.