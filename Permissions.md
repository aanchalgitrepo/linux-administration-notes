# Linux File Permissions (Part 1)

## Introduction

Linux is a multi-user operating system where multiple users can access the same system. To protect files and directories from unauthorized access, Linux uses a **permission system**.

Permissions determine **who can read, write, or execute** a file or directory. This helps maintain security, privacy, and proper access control in the operating system.

Every file and directory in Linux has an owner, a group, and a set of permissions that define what actions different users can perform.

---

# 1. Definition (What are Linux File Permissions?)

Linux file permissions are a security mechanism that controls who can access a file or directory and what actions they are allowed to perform.

Permissions are assigned to three categories of users:

- Owner (User)
- Group
- Others

Each category can have one or more of the following permissions:

- Read (r)
- Write (w)
- Execute (x)

These permissions help protect files from unauthorized access or modification.

---

# 2. Why are Linux File Permissions Used?

Linux file permissions are used to:

- Protect important files from unauthorized access.
- Control who can read, modify, or execute files.
- Improve system security.
- Prevent accidental deletion or modification of files.
- Allow multiple users to work safely on the same system.
- Secure applications and services.
- Restrict access to confidential data.

---

# 3. Types of Linux Permissions

Linux provides three basic permissions:

## 1. Read Permission (r)

### Symbol

```
r
```

### Value

```
4
```

### Description

Allows a user to read or view the contents of a file.

For directories, it allows the user to view the list of files inside the directory.

Example:

```bash
cat file.txt
```

---

## 2. Write Permission (w)

### Symbol

```
w
```

### Value

```
2
```

### Description

Allows a user to modify the contents of a file.

For directories, it allows creating, deleting, or renaming files.

Example:

```bash
echo "Hello Linux" >> file.txt
```

---

## 3. Execute Permission (x)

### Symbol

```
x
```

### Value

```
1
```

### Description

Allows a user to execute a file as a program or script.

For directories, it allows entering (accessing) the directory.

Example:

```bash
./script.sh
```

---

# 4. Permission Categories

Linux permissions are assigned to three different categories.

## 1. Owner (User)

The person who owns the file.

Symbol:

```
u
```

Example:

The owner can have:

```
rwx
```

---

## 2. Group

Users belonging to the same group.

Symbol:

```
g
```

Example:

```
r-x
```

---

## 3. Others

All remaining users on the system.

Symbol:

```
o
```

Example:

```
r--
```

---

# 5. Understanding Permission Representation

Run the following command:

```bash
ls -l
```

Example Output:

```text
-rwxr-xr-- 1 rahul developers 1024 Jul 17 file.sh
```

Breakdown:

| Part | Meaning |
|------|---------|
| - | File Type |
| rwx | Owner Permissions |
| r-x | Group Permissions |
| r-- | Others Permissions |

---

# Understanding rwxr-xr--

```
rwx   r-x   r--
```

Owner

```
rwx
```

- Read ✅
- Write ✅
- Execute ✅

Group

```
r-x
```

- Read ✅
- Write ❌
- Execute ✅

Others

```
r--
```

- Read ✅
- Write ❌
- Execute ❌

---

# 6. Numeric (Octal) Permissions

Linux represents permissions using numbers.

| Permission | Value |
|------------|------:|
| Read | 4 |
| Write | 2 |
| Execute | 1 |

The values are added together.

Examples:

| Permission | Calculation | Number |
|------------|------------:|-------:|
| rwx | 4+2+1 | 7 |
| rw- | 4+2 | 6 |
| r-x | 4+1 | 5 |
| r-- | 4 | 4 |
| --- | 0 | 0 |

---

# Common Numeric Permissions

## 777

```
rwxrwxrwx
```

Meaning:

- Owner = Full Permission
- Group = Full Permission
- Others = Full Permission

⚠️ Not recommended for production systems because everyone has full access.

---

## 755

```
rwxr-xr-x
```

Meaning:

Owner

- Read
- Write
- Execute

Group

- Read
- Execute

Others

- Read
- Execute

Commonly used for executable scripts and directories.

---

## 700

```
rwx------
```

Meaning:

Only the owner has access.

Used for private files and SSH directories.

---

## 644

```
rw-r--r--
```

Meaning:

Owner

- Read
- Write

Group

- Read

Others

- Read

Commonly used for text files and configuration files.

---

## 600

```
rw-------
```

Meaning:

Only the owner can read and write.

Used for passwords, private keys, and confidential files.

---

# 7. Symbolic Permissions

Instead of numbers, Linux also supports symbolic permissions.

| Symbol | Meaning |
|--------|---------|
| u | User (Owner) |
| g | Group |
| o | Others |
| a | All Users |

Permission Symbols

| Symbol | Meaning |
|--------|---------|
| + | Add Permission |
| - | Remove Permission |
| = | Assign Exact Permission |

Examples:

Add execute permission for the owner:

```bash
chmod u+x script.sh
```

Remove write permission from the group:

```bash
chmod g-w file.txt
```

Give read permission to others:

```bash
chmod o+r file.txt
```

Give everyone execute permission:

```bash
chmod a+x script.sh
```

Assign read and write permission only to the owner:

```bash
chmod u=rw file.txt
```

---

# Key Points

- Linux permissions improve system security.
- Every file has an owner, a group, and others.
- Linux uses Read (r), Write (w), and Execute (x) permissions.
- Permissions can be represented in numeric (755, 644, 777) or symbolic (u+x, g-w, o+r) format.
- Understanding permissions is essential for Linux Administration, Cloud Computing, and DevOps.


# chmod Command (Change File Permissions) (Part 2A.1)

## 1. Definition

The `chmod` (Change Mode) command is used to change the permissions of files and directories in Linux.

It allows the system administrator or the file owner to control who can read, write, or execute a file or directory.

Linux uses permissions to protect files from unauthorized access and modification.

---

# 2. Why is chmod Used?

The `chmod` command is used to:

- Change file permissions.
- Change directory permissions.
- Improve system security.
- Prevent unauthorized users from modifying files.
- Allow users to execute shell scripts.
- Secure sensitive files and directories.
- Control access to shared resources.

---

# 3. Syntax

## Numeric Mode

```bash
chmod [permissions] filename
```

Example

```bash
chmod 755 script.sh
```

---

## Symbolic Mode

```bash
chmod [user][operator][permission] filename
```

Example

```bash
chmod u+x script.sh
```

---

## Recursive Mode

Used to change permissions for all files and subdirectories.

```bash
chmod -R permissions directory_name
```

Example

```bash
chmod -R 755 project/
```

---

# 4. chmod Options

| Option | Description |
|---------|-------------|
| -R | Change permissions recursively for all files and directories. |
| -v | Display every file processed. |
| -c | Display only files whose permissions changed. |
| -f | Suppress most error messages. |
| --reference=file | Copy permissions from another file. |

---

## Option Examples

### Recursive

```bash
chmod -R 755 website/
```

Changes permissions of all files and folders inside the **website** directory.

---

### Verbose

```bash
chmod -v 755 script.sh
```

Displays the permission changes.

---

### Changes Only

```bash
chmod -c 644 file.txt
```

Displays output only if permissions are changed.

---

### Copy Permissions

```bash
chmod --reference=file1.txt file2.txt
```

Copies the permissions of **file1.txt** to **file2.txt**.

---

# 5. Understanding Numeric Permissions

Linux assigns a numeric value to each permission.

| Permission | Value |
|------------|------:|
| Read (r) | 4 |
| Write (w) | 2 |
| Execute (x) | 1 |

The values are added together to create permission codes.

---

## Numeric Permission Table

| Number | Permission | Meaning |
|--------:|------------|---------|
| 0 | --- | No permissions |
| 1 | --x | Execute only |
| 2 | -w- | Write only |
| 3 | -wx | Write + Execute |
| 4 | r-- | Read only |
| 5 | r-x | Read + Execute |
| 6 | rw- | Read + Write |
| 7 | rwx | Read + Write + Execute |

---

# Common Numeric Permissions

## 777

```text
rwxrwxrwx
```

Meaning

Owner

- Read
- Write
- Execute

Group

- Read
- Write
- Execute

Others

- Read
- Write
- Execute

Example

```bash
chmod 777 file.txt
```

⚠️ Warning:

This permission is **not recommended** because everyone has full access.

---

## 755

```text
rwxr-xr-x
```

Meaning

Owner

- Read
- Write
- Execute

Group

- Read
- Execute

Others

- Read
- Execute

Example

```bash
chmod 755 script.sh
```

Commonly used for:

- Shell scripts
- Executable files
- Website directories

---

## 700

```text
rwx------
```

Meaning

Only the owner has full access.

Example

```bash
chmod 700 private.sh
```

Commonly used for:

- SSH keys
- Private scripts
- Confidential directories

---

## 644

```text
rw-r--r--
```

Meaning

Owner

- Read
- Write

Group

- Read

Others

- Read

Example

```bash
chmod 644 notes.txt
```

Commonly used for:

- Configuration files
- Text files
- Documentation

---

## 600

```text
rw-------
```

Meaning

Only the owner can read and write.

Example

```bash
chmod 600 id_rsa
```

Commonly used for:

- SSH private keys
- Password files
- Sensitive configuration files

---

# 6. Symbolic Permissions

Instead of numbers, Linux also allows symbolic notation.

## User Symbols

| Symbol | Meaning |
|--------|---------|
| u | User (Owner) |
| g | Group |
| o | Others |
| a | All Users |

---

## Permission Symbols

| Symbol | Meaning |
|--------|---------|
| r | Read |
| w | Write |
| x | Execute |

---

## Operators

| Operator | Meaning |
|----------|---------|
| + | Add permission |
| - | Remove permission |
| = | Assign exact permission |

---

# Symbolic Permission Examples

### Add Execute Permission to Owner

```bash
chmod u+x script.sh
```

Meaning:

Adds execute permission only for the owner.

---

### Remove Write Permission from Group

```bash
chmod g-w file.txt
```

Meaning:

Removes write permission from the group.

---

### Give Read Permission to Others

```bash
chmod o+r notes.txt
```

Meaning:

Adds read permission for others.

---

### Give Execute Permission to Everyone

```bash
chmod a+x script.sh
```

Meaning:

Makes the file executable for all users.

---

### Give Read and Write Permission Only to Owner

```bash
chmod u=rw secret.txt
```

Meaning:

The owner gets only read and write permissions.

---

### Remove Execute Permission from Everyone

```bash
chmod a-x script.sh
```

Meaning:

Removes execute permission from all users.

---

# Difference Between Numeric and Symbolic Permissions

| Numeric Mode | Symbolic Mode |
|--------------|---------------|
| Uses numbers (755, 644, 777) | Uses symbols (u+x, g-w, o+r) |
| Faster for setting complete permissions | Better for adding or removing specific permissions |
| Common in automation scripts | Easier to understand and modify existing permissions |

---

# Key Points

- `chmod` stands for **Change Mode**.
- It is used to change file and directory permissions.
- Permissions can be changed using **Numeric Mode** or **Symbolic Mode**.
- Numeric mode is preferred in automation and scripting.
- Symbolic mode is useful when changing a specific permission.
- Avoid using `777` unless absolutely necessary because it creates security risks.
- `755` and `644` are the most commonly used permission sets in Linux systems.
