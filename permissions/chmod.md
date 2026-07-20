# Linux File Permissions 

## Introduction

Linux is a multi-user operating system where multiple users can access the same system. To protect files and directories from unauthorized access, Linux uses a **permission system**.

Permissions determine **who can read, write, or execute** a file or directory. This helps maintain security, privacy, and proper access control in the operating system.

Every file and directory in Linux has an owner, a group, and a set of permissions that define what actions different users can perform.

---

### 1. Definition (What are Linux File Permissions?)

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

### 2. Why are Linux File Permissions Used?

Linux file permissions are used to:

- Protect important files from unauthorized access.
- Control who can read, modify, or execute files.
- Improve system security.
- Prevent accidental deletion or modification of files.
- Allow multiple users to work safely on the same system.
- Secure applications and services.
- Restrict access to confidential data.

---

### 3. Types of Linux Permissions

Linux provides three basic permissions:

#### 1. Read Permission (r)

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

#### 2. Write Permission (w)

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

#### 3. Execute Permission (x)

### Symbol

```
x
```

### Value

```
1
```
---

### Description

Allows a user to execute a file as a program or script.

For directories, it allows entering (accessing) the directory.

Example:

```bash
./script.sh
```

---

### 4. Permission Categories

Linux permissions are assigned to three different categories.

#### 1. Owner (User)

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

#### 2. Group

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

#### 3. Others

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

### 5. Understanding Permission Representation

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

 Understanding rwxr-xr--

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

### 6. Numeric (Octal) Permissions

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

### Common Numeric Permissions

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

### 7. Symbolic Permissions

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

### Key Points

- Linux permissions improve system security.
- Every file has an owner, a group, and others.
- Linux uses Read (r), Write (w), and Execute (x) permissions.
- Permissions can be represented in numeric (755, 644, 777) or symbolic (u+x, g-w, o+r) format.
- Understanding permissions is essential for Linux Administration, Cloud Computing, and DevOps.


## chmod Command (Change File Permissions) (Part 2A.1)

### 1. Definition

The `chmod` (Change Mode) command is used to change the permissions of files and directories in Linux.

It allows the system administrator or the file owner to control who can read, write, or execute a file or directory.

Linux uses permissions to protect files from unauthorized access and modification.

---

### 2. Why is chmod Used?

The `chmod` command is used to:

- Change file permissions.
- Change directory permissions.
- Improve system security.
- Prevent unauthorized users from modifying files.
- Allow users to execute shell scripts.
- Secure sensitive files and directories.
- Control access to shared resources.

---

### 3. Syntax

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

### 4. chmod Options

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

### 5. Understanding Numeric Permissions

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

### Common Numeric Permissions

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

### 6. Symbolic Permissions

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

### Symbolic Permission Examples

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

### Difference Between Numeric and Symbolic Permissions

| Numeric Mode | Symbolic Mode |
|--------------|---------------|
| Uses numbers (755, 644, 777) | Uses symbols (u+x, g-w, o+r) |
| Faster for setting complete permissions | Better for adding or removing specific permissions |
| Common in automation scripts | Easier to understand and modify existing permissions |

---

### Key Points

- `chmod` stands for **Change Mode**.
- It is used to change file and directory permissions.
- Permissions can be changed using **Numeric Mode** or **Symbolic Mode**.
- Numeric mode is preferred in automation and scripting.
- Symbolic mode is useful when changing a specific permission.
- Avoid using `777` unless absolutely necessary because it creates security risks.
- `755` and `644` are the most commonly used permission sets in Linux systems.

### chmod Practical Examples (Part 2A.2A)

The following examples demonstrate how to use the `chmod` command in real-world Linux administration.

---

#### Example 1: Give Full Permissions to Everyone

## Command

```bash
chmod 777 file.txt
```

### Explanation

- Owner → Read, Write, Execute
- Group → Read, Write, Execute
- Others → Read, Write, Execute

Permission becomes:

```
rwxrwxrwx
```

### Expected Output

```bash
ls -l file.txt
```

```text
-rwxrwxrwx 1 user user 0 Jul 17 10:00 file.txt
```

### Real-World Use Case

Used only for testing purposes.

⚠️ **Not recommended** in production because anyone can modify or delete the file.

---

#### Example 2: Give Owner Full Access and Others Read & Execute

## Command

```bash
chmod 755 script.sh
```

### Explanation

Owner:

- Read
- Write
- Execute

Group:

- Read
- Execute

Others:

- Read
- Execute

Permission becomes:

```
rwxr-xr-x
```

### Expected Output

```bash
ls -l script.sh
```

```text
-rwxr-xr-x 1 user user 520 Jul 17 10:15 script.sh
```

### Real-World Use Case

Most commonly used for:

- Shell scripts
- Website directories
- Executable programs

---

#### Example 3: Give Owner Read & Write Only

## Command

```bash
chmod 600 secret.txt
```

### Explanation

Owner:

- Read
- Write

Group:

- No Permission

Others:

- No Permission

Permission becomes:

```
rw-------
```

### Expected Output

```bash
ls -l secret.txt
```

```text
-rw------- 1 user user 120 Jul 17 10:20 secret.txt
```

### Real-World Use Case

Used for:

- Password files
- SSH private keys
- Confidential documents

---

#### Example 4: Read-Only File

## Command

```bash
chmod 444 notes.txt
```

### Explanation

Everyone can read the file.

No one can modify or execute it.

Permission becomes:

```
r--r--r--
```

### Expected Output

```bash
-r--r--r-- 1 user user 200 Jul 17 10:25 notes.txt
```

### Real-World Use Case

Used for:

- Public documentation
- Manuals
- Read-only reports

---

#### Example 5: Add Execute Permission to Owner

## Command

```bash
chmod u+x script.sh
```

### Explanation

- `u` = Owner
- `+` = Add
- `x` = Execute

Only the owner gets execute permission.

### Expected Output

Before:

```text
-rw-r--r--
```

After:

```text
-rwxr--r--
```

### Real-World Use Case

Used when a shell script needs to be executed by its owner.

---

#### Example 6: Remove Write Permission from Group

## Command

```bash
chmod g-w project.txt
```

### Explanation

- `g` = Group
- `-` = Remove
- `w` = Write

The group can no longer modify the file.

### Expected Output

Before:

```text
-rw-rw-r--
```

After:

```text
-rw-r--r--
```

### Real-World Use Case

Useful when team members should only read project files.

---

#### Example 7: Give Read Permission to Others

## Command

```bash
chmod o+r file.txt
```

### Explanation

Adds read permission for all other users.

### Expected Output

Before:

```text
-rw-r-----
```

After:

```text
-rw-r--r--
```

### Real-World Use Case

Useful when sharing documents with all users.

---

#### Example 8: Remove Execute Permission from Everyone

## Command

```bash
chmod a-x script.sh
```

### Explanation

- `a` = All users
- `-` = Remove
- `x` = Execute

Nobody can execute the file.

### Expected Output

Before:

```text
-rwxr-xr-x
```

After:

```text
-rw-r--r--
```

### Real-World Use Case

Used to prevent accidental execution of scripts.

---

#### Example 9: Assign Read and Write Permission to Owner Only

### Command

```bash
chmod u=rw file.txt
```

### Explanation

Owner gets:

- Read
- Write

Execute permission is removed.

### Expected Output

```text
-rw-r--r--
```

### Real-World Use Case

Used for text files that only the owner should edit.

---

#### Example 10: Change Permissions Recursively

## Command

```bash
chmod -R 755 project/
```

### Explanation

- `-R` = Recursive
- Applies the permission to the directory and all files/subdirectories inside it.

### Expected Output

```bash
ls -l project
```

All files and directories inside `project/` will have updated permissions.

### Real-World Use Case

Used when deploying a website or application so that all project files have consistent permissions.

---

### Key Learning Points

- Use `755` for executable scripts and directories.
- Use `644` for normal files.
- Use `600` for confidential files.
- Avoid `777` in production systems.
- Use symbolic mode (`u+x`, `g-w`, `o+r`) when changing specific permissions.
- Use `-R` carefully because it changes permissions for every file and directory inside the specified path.

## chmod Practice Exercises & Screenshot Guide (Part 2A.3)

This section contains hands-on exercises to help you practice the `chmod` command. Perform these exercises in your Linux terminal and capture screenshots for your GitHub repository.

---

#### Practice Exercise 1: Create a Test File

## Command

```bash
touch file1.txt
```

### Verify

```bash
ls -l file1.txt
```

### Expected Output

```text
-rw-r--r-- 1 user user 0 Jul 17 10:00 file1.txt
```

---

#### Practice Exercise 2: Change Permission to 777

## Command

```bash
chmod 777 file1.txt
```

### Verify

```bash
ls -l file1.txt
```

### Expected Output

```text
-rwxrwxrwx 1 user user 0 Jul 17 10:05 file1.txt
```

---

#### Practice Exercise 3: Change Permission to 755

## Command

```bash
chmod 755 file1.txt
```

### Verify

```bash
ls -l file1.txt
```

### Expected Output

```text
-rwxr-xr-x 1 user user 0 Jul 17 10:10 file1.txt
```

---

#### Practice Exercise 4: Change Permission to 644

## Command

```bash
chmod 644 file1.txt
```

### Verify

```bash
ls -l file1.txt
```

### Expected Output

```text
-rw-r--r-- 1 user user 0 Jul 17 10:15 file1.txt
```

---

#### Practice Exercise 5: Change Permission to 600

## Command

```bash
chmod 600 file1.txt
```

### Verify

```bash
ls -l file1.txt
```

### Expected Output

```text
-rw------- 1 user user 0 Jul 17 10:20 file1.txt
```

---

#### Practice Exercise 6: Add Execute Permission to Owner

## Command

```bash
chmod u+x file1.txt
```

### Verify

```bash
ls -l file1.txt
```

### Expected Output

```text
-rwx------ 1 user user 0 Jul 17 10:25 file1.txt
```

---

#### Practice Exercise 7: Remove Write Permission from Group

## Command

```bash
chmod g-w file1.txt
```

### Verify

```bash
ls -l file1.txt
```

Observe how the group write permission changes.

---

#### Practice Exercise 8: Give Read Permission to Others

## Command

```bash
chmod o+r file1.txt
```

### Verify

```bash
ls -l file1.txt
```

---

#### Practice Exercise 9: Remove Execute Permission from Everyone

## Command

```bash
chmod a-x file1.txt
```

### Verify

```bash
ls -l file1.txt
```

---

#### Practice Exercise 10: Recursive Permission Change

## Step 1: Create a Directory

```bash
mkdir project
```

## Step 2: Create Files

```bash
touch project/file1.txt
touch project/file2.txt
```

## Step 3: Apply Permissions Recursively

```bash
chmod -R 755 project
```

## Step 4: Verify

```bash
ls -l project
```

---

### Screenshot Guide

Capture screenshots of the following commands and their outputs.

### Screenshot 1

```bash
ls -l file1.txt
```

Suggested filename:

```text
chmod-before.png
```

---

### Screenshot 2

```bash
chmod 777 file1.txt
ls -l file1.txt
```

Suggested filename:

```text
chmod-777.png
```

---

### Screenshot 3

```bash
chmod 755 file1.txt
ls -l file1.txt
```

Suggested filename:

```text
chmod-755.png
```

---

### Screenshot 4

```bash
chmod 644 file1.txt
ls -l file1.txt
```

Suggested filename:

```text
chmod-644.png
```

---

### Screenshot 5

```bash
chmod 600 file1.txt
ls -l file1.txt
```

Suggested filename:

```text
chmod-600.png
```

---

### Screenshot 6

```bash
chmod u+x file1.txt
ls -l file1.txt
```

Suggested filename:

```text
chmod-u-plus-x.png
```

---

### Screenshot 7

```bash
chmod g-w file1.txt
ls -l file1.txt
```

Suggested filename:

```text
chmod-g-minus-w.png
```

---

### Screenshot 8

```bash
chmod o+r file1.txt
ls -l file1.txt
```

Suggested filename:

```text
chmod-o-plus-r.png
```

---

### Screenshot 9

```bash
chmod a-x file1.txt
ls -l file1.txt
```

Suggested filename:

```text
chmod-a-minus-x.png
```

---

### Screenshot 10

```bash
chmod -R 755 project
ls -l project
```

Suggested filename:

```text
chmod-recursive.png
```

---

### Common Mistakes to Avoid

- Do not use `777` on production servers unless absolutely necessary.
- Verify permissions using `ls -l` after every `chmod` command.
- Use `-R` carefully because it changes permissions for all files and subdirectories.
- Ensure you have the required ownership or use `sudo` if needed.
- Avoid changing permissions on critical system files without understanding the impact.

---

## Summary

After completing these exercises, you should be able to:

- Change file permissions using numeric mode.
- Change file permissions using symbolic mode.
- Apply permissions recursively.
- Verify permission changes using `ls -l`.
- Capture professional screenshots for your GitHub documentation.

## chmod Practical Examples (Part 2A.2B)

This section covers more practical examples of the `chmod` command used in Linux system administration.

---

#### Example 11: Give Read Permission to Group

## Command

```bash
chmod g+r report.txt
```

### Explanation

- `g` = Group
- `+` = Add
- `r` = Read

Adds read permission to the group.

### Expected Output

Before

```text
-rw------- report.txt
```

After

```text
-rw-r----- report.txt
```

### Real-World Use Case

Useful when team members need to view reports but should not modify them.

---

#### Example 12: Remove Read Permission from Others

## Command

```bash
chmod o-r confidential.txt
```

### Explanation

Removes read permission from all other users.

### Expected Output

Before

```text
-rw-r--r--
```

After

```text
-rw-r-----
```

### Real-World Use Case

Used to protect confidential company documents.

---

#### Example 13: Add Write Permission to Owner

## Command

```bash
chmod u+w notes.txt
```

### Explanation

Allows the owner to edit the file.

### Expected Output

Before

```text
-r--r--r--
```

After

```text
-rw-r--r--
```

### Real-World Use Case

Useful when a read-only file needs to be updated by its owner.

---

#### Example 14: Remove Execute Permission from Owner

## Command

```bash
chmod u-x script.sh
```

### Explanation

Removes execute permission from the file owner.

### Expected Output

Before

```text
-rwxr-xr-x
```

After

```text
-rw-r-xr-x
```

### Real-World Use Case

Prevents accidental execution of scripts during maintenance.

---

#### Example 15: Give Read and Execute Permission to Group

## Command

```bash
chmod g=rx app.sh
```

### Explanation

The group receives only:

- Read
- Execute

Write permission is removed.

### Expected Output

```text
-rwxr-x---
```

### Real-World Use Case

Allows developers to run scripts without modifying them.

---

#### Example 16: Give Everyone Read Permission

## Command

```bash
chmod a+r document.txt
```

### Explanation

Adds read permission for:

- Owner
- Group
- Others

### Expected Output

```text
-r--r--r--
```

### Real-World Use Case

Useful for manuals, documentation, and public reports.

---

#### Example 17: Remove All Permissions from Others

## Command

```bash
chmod o= file.txt
chmod o-rwx file.txt
```

### Explanation

Removes all permissions from others.

### Expected Output

Before

```text
-rwxr-xr-x
```

After

```text
-rwxr-x---
```

### Real-World Use Case

Prevents unauthorized users from accessing sensitive files.

---

#### Example 18: Copy Permissions from Another File

## Command

```bash
chmod --reference=file1.txt file2.txt
```

### Explanation

Copies all permissions from **file1.txt** to **file2.txt**.

### Expected Output

If `file1.txt` has:

```text
-rwxr-xr-x
```

Then `file2.txt` will also become:

```text
-rwxr-xr-x
```

### Real-World Use Case

Useful when multiple files should have identical permissions.

---

#### Example 19: Change Permissions of an Entire Project

## Command

```bash
chmod -R 755 myproject/
```

### Explanation

Applies permission **755** to all files and directories inside **myproject** recursively.

### Expected Output

```bash
ls -l myproject
```

All items inside the directory display updated permissions.

### Real-World Use Case

Commonly used while deploying web applications.

---

#### Example 20: Secure a Private Directory

## Command

```bash
chmod 700 private_folder
```

### Explanation

Only the owner has:

- Read
- Write
- Execute

Group and Others have no permissions.

### Expected Output

```text
drwx------ private_folder
```

### Real-World Use Case

Used for:

- Personal documents
- SSH configuration
- Backup directories
- Sensitive application data

---

### Key Learning Points

- Use symbolic mode for small permission changes.
- Use numeric mode for setting complete permissions.
- Always verify changes using:

```bash
ls -l
```

- Avoid `777` unless absolutely necessary.
- Use `700` for private directories.
- Use `644` for normal files.
- Use `755` for executable scripts and directories.
- Use recursive (`-R`) permission changes carefully because they affect all files and subdirectories.

## chmod Interview Questions and Answers (Part 2A.4)

This section contains frequently asked interview questions on the `chmod` command. These questions are commonly asked in Linux Administration, Technical Support, System Administrator, Cloud, and DevOps interviews.

---

#### Q1. What is the purpose of the `chmod` command?

### Answer

The `chmod` (Change Mode) command is used to change the permissions of files and directories in Linux. It controls who can read, write, or execute a file or directory.

---

#### Q2. What are the three basic Linux permissions?

### Answer

Linux provides three basic permissions:

| Permission | Symbol | Value |
|------------|--------|------:|
| Read | r | 4 |
| Write | w | 2 |
| Execute | x | 1 |

---

#### Q3. Who can have permissions on a file?

### Answer

Permissions are assigned to three categories:

- Owner (User)
- Group
- Others

---

#### Q4. What is the difference between Numeric Mode and Symbolic Mode?

### Answer

| Numeric Mode | Symbolic Mode |
|--------------|---------------|
| Uses numbers like 755, 644, 777 | Uses symbols like u+x, g-w, o+r |
| Sets complete permissions at once | Adds, removes, or changes specific permissions |
| Preferred in automation scripts | Preferred for small permission changes |

---

#### Q5. What does `chmod 777 file.txt` do?

### Answer

It gives **Read, Write, and Execute** permissions to:

- Owner
- Group
- Others

Permission:

```text
rwxrwxrwx
```

⚠️ It is not recommended for production systems because everyone has full access.

---

#### Q6. What does `chmod 755 script.sh` do?

### Answer

Permission becomes:

```text
rwxr-xr-x
```

- Owner → Read, Write, Execute
- Group → Read, Execute
- Others → Read, Execute

It is commonly used for executable scripts and directories.

---

#### Q7. What does `chmod 644 file.txt` do?

### Answer

Permission becomes:

```text
rw-r--r--
```

- Owner → Read, Write
- Group → Read
- Others → Read

This is one of the most common permission settings for text and configuration files.

---

#### Q8. What does `chmod 600 secret.txt` do?

### Answer

Permission becomes:

```text
rw-------
```

Only the owner can read and write the file.

It is commonly used for SSH private keys, password files, and confidential documents.

---

#### Q9. What is the purpose of the `-R` option?

### Answer

The `-R` (Recursive) option changes the permissions of a directory and all its files and subdirectories.

Example:

```bash
chmod -R 755 project/
```

---

#### Q10. What does `chmod u+x script.sh` do?

### Answer

It adds execute permission only for the owner of the file.

---

#### Q11. What does `chmod g-w file.txt` do?

### Answer

It removes write permission from the group while keeping the other permissions unchanged.

---

#### Q12. What does `chmod o+r file.txt` do?

### Answer

It adds read permission for all other users.

---

#### Q13. What does `chmod a+x script.sh` do?

### Answer

It gives execute permission to:

- Owner
- Group
- Others

---

#### Q14. Which permission is generally recommended for normal files?

### Answer

```text
644
```

Because:

- Owner can read and write.
- Group can read.
- Others can read.

---

#### Q15. Which permission is commonly used for executable scripts?

### Answer

```text
755
```

Because the owner has full access and others can execute the script.

---

#### Q16. Why is `777` considered insecure?

### Answer

Because everyone can:

- Read
- Write
- Execute

This increases the risk of unauthorized access, modification, or deletion of files.

---

#### Q17. How can you check file permissions?

### Answer

Use:

```bash
ls -l
```

Example output:

```text
-rwxr-xr-x script.sh
```

---

#### Q18. How can you verify that `chmod` changed permissions successfully?

### Answer

Run:

```bash
ls -l filename
```

or

```bash
stat filename
```

---

#### Q19. Who can change file permissions?

### Answer

- The file owner.
- The root user (using `sudo`).

---

#### Q20. Can `chmod` change file ownership?

### Answer

No.

`chmod` changes only permissions.

Ownership is changed using:

```bash
chown
```

---

#### Q21. What is the difference between `chmod` and `chown`?

### Answer

| chmod | chown |
|--------|--------|
| Changes file permissions | Changes file ownership |
| Controls Read, Write, Execute permissions | Changes Owner and Group |

---

#### Q22. Which command removes execute permission from everyone?

### Answer

```bash
chmod a-x filename
```

---

#### Q23. Which command removes all permissions from Others?

### Answer

```bash
chmod o-rwx filename
```

---

#### Q24. Which command gives Read and Write permission only to the Owner?

### Answer

```bash
chmod 600 filename
```

or

```bash
chmod u=rw,go= filename
```

---

#### Q25. What are the most commonly used permission values in Linux?

### Answer

| Permission | Meaning | Common Use |
|------------|---------|------------|
| 777 | Full access for everyone | Testing only |
| 755 | Owner full, others read & execute | Scripts, Directories |
| 700 | Owner only | Private directories |
| 644 | Owner read/write, others read | Normal files |
| 600 | Owner read/write only | Sensitive files |

---

### Quick Revision

- `chmod` = Change file or directory permissions.
- Numeric mode uses values such as `755`, `644`, and `600`.
- Symbolic mode uses expressions such as `u+x`, `g-w`, and `o+r`.
- Verify permission changes using `ls -l` or `stat`.
- Avoid using `777` on production systems.
- `755` is common for scripts and directories.
- `644` is common for normal files.
- `600` is common for confidential files.
