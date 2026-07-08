# Linux File Permissions & Ownership Interview Questions

## Most Frequently Asked Interview Questions

### Question 1

**Question**

What are File Permissions in Linux, and why are they important?

**Answer**

File permissions define who can read, modify, or execute files and directories.

Linux permissions protect:

- Files
- Directories
- Applications
- Scripts
- Configuration files

Permission categories:

- User (Owner)
- Group
- Others

**Explanation**

Linux uses a permission-based security model to prevent unauthorized access and accidental modifications.

**Used in Production**

Permissions secure configuration files, SSH keys, scripts, application binaries, and log files.

**Common Mistake**

Many candidates believe root permissions apply to all users. Linux permissions are evaluated separately for the owner, group, and others.

---

### Question 2

**Question**

Who are User, Group, and Others in Linux?

**Answer**

Linux permissions are assigned to three categories:

| Category | Description |
|----------|-------------|
| User (u) | Owner of the file |
| Group (g) | Users belonging to the assigned group |
| Others (o) | All remaining users |

Example:

```bash
-rwxr-xr--
```

- Owner → rwx
- Group → r-x
- Others → r--

**Explanation**

Every file has one owner and one associated group, while all other users fall under "Others."

**Used in Production**

Administrators use these permission categories to control access to shared resources.

---

### Question 3

**Question**

What are Read, Write, and Execute permissions?

**Answer**

| Permission | File | Directory |
|------------|------|-----------|
| Read (r) | View file contents | List directory contents |
| Write (w) | Modify file | Create/Delete files |
| Execute (x) | Execute program/script | Enter (traverse) directory |

Permission values:

```text
Read     = 4
Write    = 2
Execute  = 1
```

**Explanation**

Permissions determine what operations a user can perform on files and directories.

**Used in Production**

Application scripts require execute permission, while configuration files often require only read and write permissions.

---

### Question 4

**Question**

What is the `chmod` command?

**Answer**

`chmod` changes file or directory permissions.

Examples:

```bash
chmod 755 script.sh

chmod +x script.sh

chmod u+x script.sh
```

**Explanation**

`chmod` allows administrators to modify access rights using either numeric or symbolic notation.

**Used in Production**

`chmod` is commonly used to make scripts executable and to secure sensitive files.

**Common Mistake**

Granting overly permissive permissions such as `777` without considering the security implications.

---

### Question 5

**Question**

What is the `chown` command?

**Answer**

`chown` changes the owner of a file or directory.

Example:

```bash
chown ubuntu file.txt
```

Change both owner and group:

```bash
chown ubuntu:developers file.txt
```

**Explanation**

Ownership determines which user has primary control over a file.

**Used in Production**

Administrators change ownership when deploying applications or transferring files between service accounts.

---

### Question 6

**Question**

What is the `chgrp` command?

**Answer**

`chgrp` changes the group ownership of a file or directory.

Example:

```bash
chgrp developers file.txt
```

**Explanation**

Changing the group allows multiple users to share access without changing the file owner.

**Used in Production**

Development teams often share files through common Linux groups.

---

### Question 7

**Question**

What is the difference between Numeric and Symbolic permissions?

**Answer**

**Numeric Permissions**

Example:

```bash
chmod 755 script.sh
```

Meaning:

```text
7 = rwx
5 = r-x
5 = r-x
```

**Symbolic Permissions**

Examples:

```bash
chmod u+x script.sh

chmod g-w file.txt

chmod o-r file.txt
```

**Explanation**

Numeric notation is concise and commonly used in automation, while symbolic notation is easier for modifying specific permissions.

**Used in Production**

Automation scripts typically use numeric notation, while administrators often use symbolic notation for quick adjustments.

---

### Question 8

**Question**

What is `umask`?

**Answer**

`umask` defines the default permissions assigned to newly created files and directories.

View current value:

```bash
umask
```

Example:

```text
022
```

**Explanation**

`umask` removes permissions from the system defaults:

- Files start with `666`
- Directories start with `777`

The final permissions are determined after subtracting the `umask`.

**Used in Production**

Organizations configure `umask` to enforce secure default permissions.

---

### Question 9

**Question**

How do you interpret the permission string `-rwxr-xr--`?

**Answer**

Breakdown:

```text
-
rwx
r-x
r--
```

Meaning:

- `-` → Regular file
- Owner → Read, Write, Execute
- Group → Read, Execute
- Others → Read only

Equivalent numeric permission:

```text
754
```

**Explanation**

Understanding permission strings is essential for troubleshooting access issues.

**Used in Production**

Administrators regularly inspect permissions using `ls -l`.

---

### Question 10

**Question**

Why is using `chmod 777` generally considered a bad practice?

**Answer**

`777` grants:

- Read
- Write
- Execute

to everyone.

Risks include:

- Unauthorized modifications
- Security vulnerabilities
- Malware execution
- Accidental deletion
- Compliance violations

**Explanation**

The Principle of Least Privilege recommends granting only the permissions required for a task.

**Used in Production**

Well-managed environments avoid world-writable permissions except in very specific, controlled cases.

**Common Mistake**

Using `777` as a quick fix for permission errors instead of identifying the correct ownership or permission issue.

---

### Question 11

**Question**

What are some best practices for managing Linux permissions?

**Answer**

Best practices include:

- Apply the Principle of Least Privilege.
- Use groups for shared access.
- Avoid `777` permissions.
- Review permissions regularly.
- Set appropriate ownership using `chown`.
- Use `umask` to enforce secure defaults.
- Verify permissions with `ls -l` before making changes.
- Restrict access to sensitive files such as SSH keys and configuration files.

**Explanation**

Proper permission management improves system security and reduces operational risk.

**Used in Production**

Administrators routinely audit permissions to protect critical system resources.

---

## Scenario-Based Interview Questions

### Scenario 1

**Question**

A Bash script cannot be executed even though it exists. What would you investigate?

**Answer**

Check:

- Execute permission using `ls -l`.
- File ownership.
- Current user.
- File path.
- Interpreter (`#!/bin/bash`).

Grant execute permission if needed:

```bash
chmod +x script.sh
```

**Explanation**

Scripts require execute permission before they can run.

---

### Scenario 2

**Question**

A developer cannot modify a configuration file owned by another user. How would you resolve this?

**Answer**

Check:

- File owner.
- Group ownership.
- File permissions.

If appropriate:

```bash
chown developer file.conf
```

or

```bash
chgrp developers file.conf
```

Grant only the minimum required permissions.

**Explanation**

Ownership and permissions determine whether a user can modify a file.

---

### Scenario 3

**Question**

Your application cannot read its configuration file after deployment. What would you check?

**Answer**

Verify:

- Read permission.
- File owner.
- Group ownership.
- Application service account.
- Directory permissions.

**Explanation**

Applications often fail because the service account lacks permission to access required files.

---

### Scenario 4

**Question**

A teammate suggests using `chmod 777` to solve a permission issue. Would you recommend it?

**Answer**

No.

Instead:

- Identify the correct owner.
- Verify group membership.
- Assign only the required permissions.
- Apply the Principle of Least Privilege.

**Explanation**

`777` grants unrestricted access and creates unnecessary security risks.

---

### Scenario 5

**Question**

Several developers need to modify the same project files. How would you manage access?

**Answer**

- Create a shared Linux group.
- Assign the files to that group using `chgrp`.
- Grant appropriate group permissions.
- Keep ownership with the application owner if appropriate.

**Explanation**

Using groups is more scalable and secure than assigning permissions individually.

---

### Scenario 6

**Question**

Newly created files are automatically receiving permissions that are too restrictive. What would you investigate?

**Answer**

Check the current `umask` value:

```bash
umask
```

Adjust it if necessary to align with organizational security requirements.

**Explanation**

`umask` determines the default permissions assigned to newly created files and directories.

---

### Scenario 7

**Question**

A deployment pipeline creates files owned by `root`, causing the application to fail. How would you fix this?

**Answer**

- Identify the application service account.
- Change ownership using `chown`.
- Verify file permissions.
- Ensure future deployments create files with the correct ownership.

**Explanation**

Incorrect ownership is a common cause of application startup failures after deployment.

---

### Scenario 8

**Question**

A user receives a "Permission denied" error when accessing a directory, even though the files inside have read permission. Why?

**Answer**

Check the directory's execute (`x`) permission.

Users need execute permission on a directory to access its contents.

**Explanation**

Directory permissions control traversal independently of file permissions.

---

### Scenario 9

**Question**

An application team wants to share log files between multiple administrators without giving access to all users. What would you recommend?

**Answer**

- Create an administrators group.
- Assign the log directory to that group.
- Grant appropriate group read permissions.
- Remove unnecessary permissions from "Others."

**Explanation**

Group-based permissions provide secure shared access.

---

### Scenario 10

**Question**

During a security audit, you discover several configuration files with world-writable permissions. How would you address this?

**Answer**

- Identify affected files.
- Reduce permissions using `chmod`.
- Verify ownership.
- Review `umask` settings.
- Audit recent permission changes.

**Explanation**

Configuration files should be writable only by authorized users.

---

### Scenario 11

**Question**

A production application suddenly starts failing with "Permission denied" errors after a deployment. How would you troubleshoot the issue?

**Answer**

1. Verify file and directory permissions using:

```bash
ls -l
```

2. Confirm ownership with:

```bash
ls -l
```

3. Check the application's service account.
4. Verify group membership.
5. Ensure the application has the required read, write, or execute permissions.
6. Correct ownership using `chown` or group ownership using `chgrp` if necessary.
7. Apply the Principle of Least Privilege rather than granting excessive permissions.

**Explanation**

Permission and ownership changes are common causes of production failures after deployments. A systematic review of permissions, ownership, and service account access helps identify the root cause while maintaining system security.
