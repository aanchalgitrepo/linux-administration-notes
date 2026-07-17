# Linux Users

## Introduction

Linux is a multi-user operating system. A user is an account that allows a person or a service to log in and use the Linux system. Every user has a unique User ID (UID), a username, a home directory, and specific permissions.

Managing users is one of the most important responsibilities of a Linux System Administrator because it helps maintain system security and control access to resources.

---

# 1. Definition (What is a Linux User?)

A Linux user is an account created in the operating system that allows a person or service to access the system. Each user has a unique username and a unique User ID (UID).

---

# 2. Why are Linux Users Used?

Linux users are used to:

- Allow authorized users to log in.
- Improve system security.
- Control access to files and directories.
- Assign permissions to different users.
- Manage multiple users on the same server.
- Track user activities.
- Separate administrator accounts from normal user accounts.

---

# 3. Types of Linux Users

## 1. Root User

- UID = 0
- Has complete control over the Linux system.
- Can perform any administrative task.

Example:

```bash
sudo su
```

---

## 2. Regular User

A normal user created for everyday work.

Example:

```bash
whoami
```

---

## 3. System User

Used by services and applications such as MySQL, Apache, Nginx, and Docker.

Example:

```bash
cat /etc/passwd
```

---

# 4. Important Files

| File | Purpose |
|------|---------|
| /etc/passwd | Stores user account information |
| /etc/shadow | Stores encrypted passwords |
| /etc/group | Stores group information |
| /home | User home directories |

---

# 5. Common User Management Commands

| Command | Purpose |
|----------|---------|
| useradd | Create a new user |
| adduser | Create a new user (interactive) |
| usermod | Modify a user |
| userdel | Delete a user |
| passwd | Set or change password |
| id | Display UID and GID |
| whoami | Display current user |
| who | Show logged-in users |
| last | Show login history |
| su | Switch user |
| sudo | Run commands as another user |

---

# 6. Syntax

## Create User

```bash
sudo useradd username
```

## Set Password

```bash
sudo passwd username
```

## Delete User

```bash
sudo userdel username
```

## Modify User

```bash
sudo usermod [options] username
```

---

# 7. Practical Examples

## Example 1: Create a User

```bash
sudo useradd rohit
```

Explanation:

Creates a new user named rohit.

---

## Example 2: Set Password

```bash
sudo passwd rohit
```

Explanation:

Assigns a password to the user.

---

## Example 3: Display User ID

```bash
id rohit
```

Explanation:

Displays the UID, GID, and group information.

---

## Example 4: Check Current User

```bash
whoami
```

Explanation:

Displays the currently logged-in user.

---

## Example 5: View Login History

```bash
last
```

Explanation:

Displays previous login sessions.

---

# 8. Real-World Use Case

In an IT company, when a new employee joins, the Linux Administrator creates a new user account using the `useradd` command, sets a password, assigns the user to the appropriate groups, and provides only the permissions required for that employee's role.

---

# 9. Practice Exercise

### Task 1

Create a user named testuser.

```bash
sudo useradd testuser
```

---

### Task 2

Set a password.

```bash
sudo passwd testuser
```

---

### Task 3

Verify the user.

```bash
id testuser
```

---

### Task 4

Check current user.

```bash
whoami
```

---

### Task 5

Delete the user.

```bash
sudo userdel testuser
```

---

# 10. Screenshot Guide

Take screenshots after running the following commands:

```bash
sudo useradd testuser
```

```bash
sudo passwd testuser
```

```bash
id testuser
```

```bash
whoami
```

Save screenshots inside:

```
screenshots/
```

Example:

```
useradd.png
passwd.png
id.png
whoami.png
```

---

# 11. Important Interview Questions

### Q1. What is a Linux user?

### Q2. What is the difference between the root user and a normal user?

### Q3. What is UID?

### Q4. What is the purpose of the /etc/passwd file?

### Q5. What is the purpose of the /etc/shadow file?

### Q6. What is the difference between useradd and adduser?

### Q7. How do you delete a Linux user?

### Q8. How do you change a user's password?

### Q9. What is the purpose of the whoami command?

### Q10. How do you display a user's UID and GID?

---

# 12. Summary

In this chapter, you learned:

- What Linux users are.
- Types of Linux users.
- Important user-related files.
- User management commands.
- Practical examples.
- Real-world use cases.
- Practice exercises.
- Interview questions.
