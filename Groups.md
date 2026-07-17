# Linux Groups

## Introduction

Linux is a multi-user operating system where multiple users can work on the same system. A Linux group is a collection of users that helps administrators manage permissions efficiently. Instead of assigning permissions to each user individually, permissions can be assigned to a group.

Groups simplify user management and improve system security.

---

# 1. Definition (What is a Linux Group?)

A Linux group is a collection of users that share the same access permissions to files, directories, and system resources. Every group has a unique Group ID (GID).

---

# 2. Why are Linux Groups Used?

Linux groups are used to:

- Manage multiple users efficiently.
- Assign permissions to a group instead of individual users.
- Improve system security.
- Simplify administration.
- Control access to files and directories.
- Organize users based on their roles.

---

# 3. Types of Linux Groups

## 1. Primary Group

- Every user belongs to one primary group.
- The primary group is assigned when the user is created.

Check a user's primary group:

```bash
id username
```

---

## 2. Secondary (Supplementary) Group

- A user can belong to multiple secondary groups.
- Used to grant additional permissions.

Example:

```bash
groups username
```

---

# 4. Important Group File

| File | Purpose |
|------|---------|
| /etc/group | Stores group information |
| /etc/gshadow | Stores secure group passwords and administrators |

---

# 5. Common Group Management Commands

| Command | Purpose |
|----------|---------|
| groupadd | Create a new group |
| groupmod | Modify an existing group |
| groupdel | Delete a group |
| groups | Display groups of a user |
| gpasswd | Manage group members and passwords |
| newgrp | Switch to another group |

---

# 6. Syntax

## Create a Group

```bash
sudo groupadd groupname
```

## Modify a Group

```bash
sudo groupmod [options] groupname
```

## Delete a Group

```bash
sudo groupdel groupname
```

## Display User Groups

```bash
groups username
```

## Add User to a Group

```bash
sudo gpasswd -a username groupname
```

## Remove User from a Group

```bash
sudo gpasswd -d username groupname
```

## Switch to Another Group

```bash
newgrp groupname
```

---

# 7. Practical Examples

## Example 1: Create a Group

```bash
sudo groupadd developers
```

Explanation:

Creates a new group named **developers**.

---

## Example 2: Display User Groups

```bash
groups rahul
```

Explanation:

Shows all groups to which the user **rahul** belongs.

---

## Example 3: Add User to a Group

```bash
sudo gpasswd -a rahul developers
```

Explanation:

Adds the user **rahul** to the **developers** group.

---

## Example 4: Remove User from a Group

```bash
sudo gpasswd -d rahul developers
```

Explanation:

Removes the user **rahul** from the **developers** group.

---

## Example 5: Rename a Group

```bash
sudo groupmod -n devteam developers
```

Explanation:

Renames the group **developers** to **devteam**.

---

## Example 6: Delete a Group

```bash
sudo groupdel devteam
```

Explanation:

Deletes the **devteam** group.

---

## Example 7: Switch to a Group

```bash
newgrp developers
```

Explanation:

Changes the current shell to use the **developers** group.

---

# 8. Real-World Use Case

In an IT company, all developers are added to the **developers** group. Permissions to the project directory are assigned to the group instead of each developer individually. When a new developer joins, the administrator only needs to add the user to the **developers** group.

---

# 9. Practice Exercise

### Task 1

Create a group.

```bash
sudo groupadd developers
```

---

### Task 2

Create a user.

```bash
sudo useradd -m rahul
```

---

### Task 3

Add the user to the group.

```bash
sudo gpasswd -a rahul developers
```

---

### Task 4

Verify group membership.

```bash
groups rahul
```

---

### Task 5

Rename the group.

```bash
sudo groupmod -n devteam developers
```

---

### Task 6

Delete the group.

```bash
sudo groupdel devteam
```

---

# 10. Screenshot Guide

Take screenshots after running the following commands:

```bash
sudo groupadd developers
```

```bash
groups rahul
```

```bash
sudo gpasswd -a rahul developers
```

```bash
sudo groupmod -n devteam developers
```

```bash
sudo groupdel devteam
```

Save the screenshots in:

```
screenshots/
```

Suggested file names:

```
groupadd.png
groups.png
gpasswd-add.png
groupmod.png
groupdel.png
```

---

# 11. Important Interview Questions

### Q1. What is a Linux group?

**Answer:** A Linux group is a collection of users used to manage permissions efficiently.

---

### Q2. What is the difference between a primary group and a secondary group?

**Answer:** A primary group is assigned when the user is created, while a secondary group provides additional permissions and a user can belong to multiple secondary groups.

---

### Q3. Which file stores Linux group information?

**Answer:** `/etc/group`

---

### Q4. Which command creates a new group?

**Answer:** `groupadd`

---

### Q5. Which command displays the groups of a user?

**Answer:** `groups`

---

### Q6. How do you add a user to a group?

**Answer:**

```bash
sudo gpasswd -a username groupname
```

---

### Q7. How do you remove a user from a group?

**Answer:**

```bash
sudo gpasswd -d username groupname
```

---

### Q8. How do you rename a group?

**Answer:**

```bash
sudo groupmod -n newgroup oldgroup
```

---

### Q9. How do you delete a group?

**Answer:**

```bash
sudo groupdel groupname
```

---

### Q10. What is the purpose of the `newgrp` command?

**Answer:** It changes the current shell session to use another group without logging out.

---

# 12. Summary

In this chapter, you learned:

- What Linux groups are.
- Primary and secondary groups.
- Important group-related files.
- Group management commands.
- Practical examples.
- Real-world use cases.
- Practice exercises.
- Interview questions.
