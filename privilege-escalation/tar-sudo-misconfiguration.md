
# GNU tar and Linux Privilege Escalation

## 1. Overview

GNU tar is a utility used to create, inspect, and extract archives.

It is widely used for backups, software distribution, and system administration.

Official GTFOBins reference:

https://gtfobins.github.io/gtfobins/tar/

GTFOBins documents ways legitimate Unix binaries can be abused when they are available in privileged execution contexts.

The security issue discussed here is excessive privilege granted to tar, not simply the installation of tar.

## 2. How tar Works

An archive groups files and directory information into a single file.

Example:

```bash
tar -cf backup.tar documents/
```

This creates an archive named `backup.tar` containing the selected directory.

The important options are:

- `-c`: create an archive.
- `-f`: specify the archive filename.
- `-t`: list archive contents.
- `-x`: extract archive contents.

GNU tar also supports checkpoint functionality and checkpoint actions. Some actions can execute external commands.

These features can be useful for legitimate automation, but become security-relevant when an unrestricted privileged invocation is available to an untrusted user.

## 3. The Privilege-Escalation Scenario

Consider the following hypothetical situation:

1. An administrator wants a backup operator to create archives.
2. The administrator grants that operator permission to execute tar as root.
3. The policy does not adequately restrict the permitted arguments or behavior.
4. The operator discovers that tar supports features beyond ordinary archive creation.
5. Those features may provide a path to executing commands with the process's elevated privileges.

The central weakness is excessive privilege combined with insufficient restriction.

The exact result depends on the sudoers policy, program implementation, arguments, and execution environment.

## 4. Why GTFOBins Matters

GTFOBins is a reference for identifying potentially dangerous capabilities in standard Unix binaries.

Its entries are organized by execution context, including:

- Sudo
- SUID
- Capabilities
- Shell
- File read
- File write

Not every category applies to every binary.

For tar, review the Sudo section and understand its prerequisites. Do not assume that a SUID technique or capability technique applies merely because a Sudo technique exists.

## 5. Safe Enumeration

Start by identifying your current identity:

```bash
whoami
id
```

Review the commands your account may run through sudo:

```bash
sudo -l
```

Locate the tar executable:

```bash
command -v tar
```

Inspect its file metadata:

```bash
ls -l "$(command -v tar)"
```

Record the observed output in your assessment notes.

These commands help establish the environment, but they do not independently prove that privilege escalation is possible.

## 6. Questions to Investigate

- Does sudo permit tar to run as root?
- Is the permission necessary for the user's role?
- Are permitted arguments restricted?
- Is the program the expected implementation of GNU tar?
- Can the permitted operation invoke external commands?
- Are there controls preventing unintended command execution?
- Is the behavior reproducible in an authorized test environment?

## 7. Evidence Requirements

Collect evidence showing:

- The identity of the test account.
- The relevant sudo permission.
- The binary's location and implementation.
- The exact configuration that grants elevated execution.
- The behavior observed during authorized validation.
- The potential or confirmed security impact.

Do not include passwords, authentication tokens, private keys, or unrelated sensitive information in your report.

## 8. Impact

If unrestricted privileged execution is confirmed, a low-privileged user may be able to execute arbitrary commands as root.

Possible consequences include:

- Unauthorized access to protected files.
- Modification of system configuration.
- Changes to user accounts or permissions.
- Compromise of services running on the host.
- Loss of system integrity or availability.

The actual impact depends on the privileges demonstrated and the affected environment.

## 9. Remediation

Recommended controls include:

1. Remove unnecessary sudo access to tar.
2. Avoid granting unrestricted root execution to general-purpose utilities.
3. Use a dedicated backup program or narrowly scoped wrapper.
4. Validate arguments and permitted paths.
5. Ensure that privileged automation cannot execute user-controlled commands.
6. Review scheduled tasks and backup scripts for similar weaknesses.
7. Re-test the configuration after remediation.

## 10. Conclusion

GNU tar is a legitimate administrative utility. However, its features can become dangerous when exposed through excessive privileges.

A valid finding must connect the actual configuration to a demonstrated or well-supported security impact. The binary's presence alone is not sufficient evidence of a vulnerability.
