
# Linux Sudo Enumeration Notes

## Objective

Identify which commands the current account is authorized to execute with elevated privileges.

## Step 1: Identify the Account

```bash
whoami
id
```

Record the username, UID, and group memberships.

## Step 2: Inspect Sudo Permissions

```bash
sudo -l
```

Review the output for commands that can be executed as root.

Do not assume that every listed command provides arbitrary command execution. Read the permitted command and argument restrictions carefully.

## Step 3: Locate Relevant Binaries

```bash
command -v tar
ls -l "$(command -v tar)"
```

Record the path, ownership, and permission bits.

Ordinary root ownership is expected for many system binaries and is not, by itself, evidence of privilege escalation.

## Step 4: Review Configuration

With appropriate authorization, inspect the applicable sudoers rules and any relevant administrative scripts.

Use `visudo` to edit sudoers configuration safely.

## Step 5: Compare Against GTFOBins

Reference:

https://gtfobins.github.io/gtfobins/tar/

Compare the observed permission context with the documented prerequisites.

A technique documented for Sudo must not automatically be assumed to work through SUID, capabilities, or another execution context.

## Step 6: Record Your Findings

For each suspected issue, document:

- The command or configuration examined.
- The observed permissions.
- The prerequisite that appears to be satisfied.
- The remaining conditions that require validation.
- The impact if exploitation is confirmed.
- The recommended fix.

## Important

Enumeration identifies possible attack paths. Validation establishes whether those paths are actually exploitable.

Do not confuse a potential weakness with a confirmed security finding.
