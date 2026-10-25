
# Linux Privilege Escalation Notes

Beginner-friendly notes on Linux privilege escalation, sudo permissions, GTFOBins, enumeration, security assessment, and remediation.

## About This Repository

This repository documents my learning journey in Linux security and penetration testing. It explains how Linux permissions work, how privileged programs can be misconfigured, how to investigate potential privilege-escalation paths, and how to write professional security findings.

All testing should be performed only on systems you own or have explicit authorization to assess.

## Learning Objectives

- Understand Linux users, groups, UIDs, and GIDs.
- Learn the difference between normal users and root.
- Understand sudo and sudoers configuration.
- Learn how to enumerate permissions safely.
- Understand GTFOBins and legitimate Unix binary abuse.
- Investigate potential privilege escalation through GNU tar.
- Collect evidence and assess security impact.
- Write clear findings and recommend remediation.

## Topics

### 1. Linux Fundamentals

Learn users, groups, file permissions, ownership, and administrative privileges.

### 2. Linux Privilege Escalation

Understand how a low-privileged user might gain permissions they were not intended to have.

### 3. Sudo Misconfiguration

Learn how excessive sudo permissions can expose privileged functionality.

### 4. GTFOBins: tar

Study GNU tar's features, the conditions that make privileged execution dangerous, and defensive validation.

### 5. Enumeration

Practice identifying the current user, reviewing sudo permissions, and inspecting executable ownership.

### 6. Reporting

Document the affected configuration, evidence, impact, severity, and recommended remediation.

## Key References

- GTFOBins: https://gtfobins.github.io/
- GTFOBins tar: https://gtfobins.github.io/gtfobins/tar/
- GNU tar manual: https://www.gnu.org/software/tar/manual/
- Linux man-pages: https://man7.org/linux/man-pages/
- Sudo documentation: https://www.sudo.ws/docs/

## Responsible Testing

This repository is for education, defensive security, and authorized penetration testing. Never test systems without permission, access data belonging to other users, or attempt privilege escalation on production systems without explicit authorization.

## Disclaimer

The presence of a binary does not automatically indicate a vulnerability. Exploitability depends on the actual permissions, configuration, program implementation, and execution context.
