
# Linux Users, Permissions, and Sudo

## 1. What Is a Linux User?

Linux uses user accounts to control who can access files, run programs, and administer a system.

A normal user typically has permission to manage their own files and perform tasks allowed by system policy.

The root account is the superuser. Its UID is 0, and it has extensive administrative control over the system.

## 2. What Is a UID?

UID stands for User Identifier.

Useful commands:

```bash
whoami
id
id -u
```

- `whoami` prints the effective username.
- `id` displays user and group information.
- `id -u` prints the effective UID.

UID 0 identifies root privileges.

## 3. Understanding File Permissions

Linux file permissions are commonly represented by:

- `r`: read
- `w`: write
- `x`: execute

For example:

```bash
ls -l /usr/bin/tar
```

This displays the file's permissions, owner, group, size, and other metadata.

The output must be interpreted carefully. A binary owned by root is normal and does not mean ordinary users can execute it with root privileges.

## 4. What Is Sudo?

Sudo allows an authorized user to execute a command as another user, commonly root.

Inspect your permissions with:

```bash
sudo -l
```

This displays the commands your account is allowed to execute through sudo, subject to the system's configuration.

An entry permitting a program to run as root can be dangerous if that program supports features that bypass the administrator's intended restrictions.

## 5. What Is the Sudoers File?

Sudo policy is commonly configured in `/etc/sudoers` and files under `/etc/sudoers.d/`.

Administrators should edit sudoers policy using `visudo`, which checks the configuration for syntax errors.

An authorized administrator can validate the configuration with:

```bash
sudo visudo -c
```

## 6. What Is Privilege Escalation?

Privilege escalation occurs when a user or process gains permissions beyond those intended by the system's security policy.

Two common categories are:

- Vertical privilege escalation: gaining higher privileges, such as root.
- Horizontal privilege escalation: accessing another user's permissions or resources at a similar privilege level.

## 7. Security Principle: Least Privilege

Users and programs should receive only the permissions necessary to perform their assigned tasks.

For example, a backup operator may need to archive specified directories. They do not necessarily need unrestricted root access to a general-purpose archive utility.
