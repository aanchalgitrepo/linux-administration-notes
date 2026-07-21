# stat Command (Complete Professional Notes)

## Part 3B.1 – Introduction

The `stat` command is used to display detailed information (metadata) about a file or directory in Linux.

Unlike the `ls -l` command, which provides a summary of file details, the `stat` command displays complete metadata such as:

- File Size
- File Type
- File Permissions
- Owner
- Group
- Inode Number
- Device Number
- Number of Links
- Access Time
- Modify Time
- Change Time
- Block Size
- Total Blocks Allocated

The `stat` command is widely used by Linux Administrators, DevOps Engineers, Cloud Engineers, and Technical Support Engineers to inspect files, troubleshoot permission issues, and analyze file metadata.

---

### 1. Definition

The `stat` command displays detailed status information about a file or directory.

It retrieves metadata stored by the Linux filesystem and presents it in an easy-to-read format.

Unlike `ls -l`, it provides low-level filesystem information that is useful for system administration and troubleshooting.

---

### 2. Why is stat Used?

The `stat` command is used to:

- View complete file metadata.
- Check file permissions.
- Verify owner and group.
- Display inode number.
- View file size.
- Display filesystem block information.
- Check last access, modification, and status change times.
- Troubleshoot permission issues.
- Verify changes after using `chmod` or `chown`.
- Debug filesystem-related problems.

---

### 3. Syntax

Basic Syntax

```bash
stat filename
```

Example

```bash
stat notes.txt
```

Display Information for a Directory

```bash
stat project
```

Display Multiple Files

```bash
stat file1.txt file2.txt
```

---

### 4. Common Options

| Command | Description |
|---------|-------------|
| `stat filename` | Display metadata of a file |
| `stat directory` | Display metadata of a directory |
| `stat file1 file2` | Display metadata for multiple files |
| `stat -c "%n"` | Display only the file name |
| `stat -c "%s"` | Display only the file size |
| `stat -c "%A"` | Display file permissions in symbolic format |
| `stat -c "%a"` | Display permissions in numeric format |
| `stat -c "%U"` | Display file owner |
| `stat -c "%G"` | Display file group |
| `stat -c "%i"` | Display inode number |
| `stat -c "%x"` | Display last access time |
| `stat -c "%y"` | Display last modification time |
| `stat -c "%z"` | Display last status change time |

---

### 5. Understanding stat Output

Run the following command:

```bash
stat notes.txt
```

Example Output

```text
File: notes.txt
Size: 2048            Blocks: 8          IO Block: 4096 regular file
Device: 8,1           Inode: 157286      Links: 1
Access: (0644/-rw-r--r--) Uid: (1000/rahul) Gid: (1000/developers)
Access: 2026-07-18 10:20:15
Modify: 2026-07-18 10:30:10
Change: 2026-07-18 10:35:00
 Birth: 2026-07-18 10:20:15
```

The output contains complete filesystem metadata about the file.

---

### 6. File Information Explained

### File

```text
File: notes.txt
```

Displays the name of the file.

---

### Size

```text
Size: 2048
```

Shows the size of the file in **bytes**.

---

### Blocks

```text
Blocks: 8
```

Shows the number of filesystem blocks allocated to the file.

---

### IO Block

```text
IO Block: 4096
```

Displays the preferred block size used by the filesystem for input/output operations.

---

### File Type

```text
regular file
```

Possible file types include:

| Type | Meaning |
|------|---------|
| regular file | Normal file |
| directory | Folder |
| symbolic link | Link to another file |
| block special file | Block device |
| character special file | Character device |
| socket | Network socket |
| FIFO | Named pipe |

---

### Links

```text
Links: 1
```

Displays the number of hard links associated with the file.

---

### Owner (UID)

```text
Uid: (1000/rahul)
```

Shows the numeric User ID (UID) and the owner's username.

---

### Group (GID)

```text
Gid: (1000/developers)
```

Shows the numeric Group ID (GID) and the group name.

---

### Permissions

```text
0644
```

Numeric permission.

```text
-rw-r--r--
```

Symbolic permission.

---

### 7. File Timestamp Explained

The `stat` command displays several timestamps that are useful for auditing and troubleshooting.

---

## Access Time (atime)

```text
Access:
```

Shows the last time the file was **read or accessed**.

Example:

```bash
cat notes.txt
```

Reading the file updates the access time (depending on filesystem mount options).

---

## Modify Time (mtime)

```text
Modify:
```

Shows the last time the **contents of the file** were changed.

Example:

```bash
echo "Hello" >> notes.txt
```

---

## Change Time (ctime)

```text
Change:
```

Shows the last time the file's **metadata** changed.

Metadata changes include:

- Permissions (`chmod`)
- Ownership (`chown`)
- Link count
- File rename

Example:

```bash
chmod 755 notes.txt
```

---

## Birth Time

```text
Birth:
```

Shows when the file was originally created.

> **Note:** Not all Linux filesystems store or display the file creation (Birth) time. If the filesystem does not support it, this field may be unavailable.

---

### 8. Inode, Device & Block Information

## Inode Number

```text
Inode: 157286
```

An inode is a unique identifier assigned to every file and directory in a Linux filesystem.

It stores metadata such as:

- File permissions
- Owner
- Group
- Size
- Timestamps
- Block locations

---

## Device Number

```text
Device: 8,1
```

Identifies the storage device or partition where the file is stored.

This information is mainly used for filesystem management and troubleshooting.

---

## Blocks

```text
Blocks: 8
```

Represents the number of disk blocks allocated to the file.

This value may differ from the file size because filesystems allocate storage in fixed-size blocks.

---

## IO Block

```text
IO Block: 4096
```

Indicates the preferred block size for efficient input/output operations.

---

### 9. Difference Between stat and ls -l

| Feature | stat | ls -l |
|---------|------|--------|
| Purpose | Displays complete file metadata | Displays file details in long listing format |
| File Size | ✅ Yes | ✅ Yes |
| Permissions | ✅ Yes | ✅ Yes |
| Owner | ✅ Yes | ✅ Yes |
| Group | ✅ Yes | ✅ Yes |
| Inode Number | ✅ Yes | Only with `ls -li` |
| Device Information | ✅ Yes | ❌ No |
| Block Information | ✅ Yes | ❌ No |
| Access Time | ✅ Yes | ❌ No |
| Modify Time | ✅ Yes | ✅ Yes |
| Change Time | ✅ Yes | ❌ No |
| Birth Time | ✅ Yes (if supported) | ❌ No |
| Best Use | Detailed metadata analysis | Quick file inspection |

---

### Key Learning Points

- `stat` displays detailed filesystem metadata for files and directories.
- It shows file size, permissions, owner, group, inode, timestamps, device information, and allocated blocks.
- It is commonly used by Linux Administrators, DevOps Engineers, and Technical Support professionals for troubleshooting and auditing.
- `stat` provides much more detailed information than `ls -l`.
- Understanding `atime`, `mtime`, and `ctime` is essential for Linux administration and interview preparation.
- Combine `stat` with commands such as `ls -l`, `chmod`, `chown`, `find`, and `grep` for effective file management and debugging.

"What is the difference between atime, mtime, and ctime?"
 - atime (Access Time): Last time the file was read.
 - mtime (Modify Time): Last time the file content changed.
 - ctime (Change Time): Last time the file metadata (permissions, ownership, etc.) changed.


## stat Practical Examples (Part 3B.2A)

This section contains practical examples of the `stat` command used in Linux Administration, Technical Support, Cloud Computing, and DevOps.

---

#### Example 1: Display Metadata of a File

## Command

```bash
stat notes.txt
```

### Command Explanation

Displays complete metadata of the file **notes.txt**, including permissions, owner, group, size, inode, timestamps, and block information.

### Expected Output

```text
File: notes.txt
Size: 2048
Access: (0644/-rw-r--r--)
Uid: (1000/user)
Gid: (1000/user)
```

### Real-World Use Case

A Linux administrator checks complete file details before troubleshooting permission issues.

### Screenshot Command

```bash
stat notes.txt
```

Suggested Screenshot:

```text
stat-file-details.png
```

---

#### Example 2: Display Metadata of a Directory

## Command

```bash
stat project
```

### Command Explanation

Displays metadata of the **project** directory instead of its contents.

### Expected Output

```text
File: project
Size: 4096
Access: (0755/drwxr-xr-x)
```

### Real-World Use Case

Useful for verifying directory permissions before granting user access.

### Screenshot Command

```bash
stat project
```

Suggested Screenshot:

```text
stat-directory-details.png
```

---

#### Example 3: Display Metadata of Multiple Files

## Command

```bash
stat file1.txt file2.txt
```

### Command Explanation

Displays metadata for multiple files in a single command.

### Expected Output

```text
File: file1.txt
...

File: file2.txt
...
```

### Real-World Use Case

Useful when comparing multiple configuration files.

### Screenshot Command

```bash
stat file1.txt file2.txt
```

Suggested Screenshot:

```text
stat-multiple-files.png
```

---

#### Example 4: Display Only File Name

## Command

```bash
stat -c "%n" notes.txt
```

### Command Explanation

Displays only the file name.

### Expected Output

```text
notes.txt
```

### Real-World Use Case

Useful in shell scripts where only the filename is required.

### Screenshot Command

```bash
stat -c "%n" notes.txt
```

Suggested Screenshot:

```text
stat-filename.png
```

---

#### Example 5: Display Only File Size

## Command

```bash
stat -c "%s" notes.txt
```

### Command Explanation

Displays only the file size in bytes.

### Expected Output

```text
2048
```

### Real-World Use Case

Useful when validating backup sizes or checking upload limits.

### Screenshot Command

```bash
stat -c "%s" notes.txt
```

Suggested Screenshot:

```text
stat-filesize.png
```

---

#### Example 6: Display Symbolic Permissions

## Command

```bash
stat -c "%A" notes.txt
```

### Command Explanation

Displays file permissions in symbolic format.

### Expected Output

```text
-rw-r--r--
```

### Real-World Use Case

Useful for quickly checking file access permissions.

### Screenshot Command

```bash
stat -c "%A" notes.txt
```

Suggested Screenshot:

```text
stat-symbolic-permissions.png
```

---

#### Example 7: Display Numeric Permissions

## Command

```bash
stat -c "%a" notes.txt
```

### Command Explanation

Displays file permissions in numeric format.

### Expected Output

```text
644
```

### Real-World Use Case

Useful while configuring file permissions using `chmod`.

### Screenshot Command

```bash
stat -c "%a" notes.txt
```

Suggested Screenshot:

```text
stat-numeric-permissions.png
```

---

#### Example 8: Display File Owner

## Command

```bash
stat -c "%U" notes.txt
```

### Command Explanation

Displays only the owner of the file.

### Expected Output

```text
rahul
```

### Real-World Use Case

Useful for verifying ownership after using the `chown` command.

### Screenshot Command

```bash
stat -c "%U" notes.txt
```

Suggested Screenshot:

```text
stat-owner.png
```

---

#### Example 9: Display File Group

## Command

```bash
stat -c "%G" notes.txt
```

### Command Explanation

Displays only the group associated with the file.

### Expected Output

```text
developers
```

### Real-World Use Case

Useful for checking group ownership in shared project directories.

### Screenshot Command

```bash
stat -c "%G" notes.txt
```

Suggested Screenshot:

```text
stat-group.png
```

---

#### Example 10: Display Inode Number

## Command

```bash
stat -c "%i" notes.txt
```

### Command Explanation

Displays the inode number of the file.

### Expected Output

```text
157286
```

### Real-World Use Case

Useful for filesystem troubleshooting and identifying hard links.

### Screenshot Command

```bash
stat -c "%i" notes.txt
```

Suggested Screenshot:

```text
stat-inode.png
```

---

### Key Learning Points

- `stat` displays detailed metadata about files and directories.
- The `-c` option allows you to display specific information.
- `%n` → File name
- `%s` → File size
- `%A` → Symbolic permissions
- `%a` → Numeric permissions
- `%U` → Owner
- `%G` → Group
- `%i` → Inode number
- These options are especially useful in shell scripting and Linux system administration.

---

## stat Practical Examples (Part 3B.2B)

This section contains advanced practical examples of the `stat` command used in Linux Administration, DevOps, Cloud Computing, and Technical Support.

---

#### Example 11: Display Last Access Time

## Command

```bash
stat -c "%x" notes.txt
```

### Command Explanation

Displays the last time the file was accessed (read).

### Expected Output

```text
2026-07-21 10:15:30.123456789 +0530
```

### Real-World Use Case

Useful for checking whether a file has been recently read by an application or user.

### Screenshot Command

```bash
stat -c "%x" notes.txt
```

Suggested Screenshot:

```text
stat-access-time.png
```

---

#### Example 12: Display Last Modification Time

## Command

```bash
stat -c "%y" notes.txt
```

### Command Explanation

Displays the last time the file contents were modified.

### Expected Output

```text
2026-07-21 10:20:45.987654321 +0530
```

### Real-World Use Case

Useful for tracking changes in configuration files or project files.

### Screenshot Command

```bash
stat -c "%y" notes.txt
```

Suggested Screenshot:

```text
stat-modify-time.png
```

---

#### Example 13: Display Last Status Change Time

## Command

```bash
stat -c "%z" notes.txt
```

### Command Explanation

Displays the last time the file metadata changed (permissions, ownership, etc.).

### Expected Output

```text
2026-07-21 10:30:12.654321987 +0530
```

### Real-World Use Case

Useful for verifying whether `chmod` or `chown` has recently modified the file metadata.

### Screenshot Command

```bash
stat -c "%z" notes.txt
```

Suggested Screenshot:

```text
stat-change-time.png
```

---

#### Example 14: Check Metadata After chmod

## Command

```bash
chmod 755 notes.txt
stat notes.txt
```

### Command Explanation

Changes file permissions and then displays the updated metadata.

### Expected Output

```text
Access: (0755/-rwxr-xr-x)
```

### Real-World Use Case

System administrators verify permission changes after using `chmod`.

### Screenshot Command

```bash
chmod 755 notes.txt
stat notes.txt
```

Suggested Screenshot:

```text
stat-after-chmod.png
```

---

#### Example 15: Check Metadata After chown

## Command

```bash
sudo chown rahul:developers notes.txt
stat notes.txt
```

### Command Explanation

Changes the owner and group of a file and verifies the updated metadata.

### Expected Output

```text
Uid: (1001/rahul)
Gid: (1002/developers)
```

### Real-World Use Case

Useful for verifying ownership changes after transferring project files.

### Screenshot Command

```bash
sudo chown rahul:developers notes.txt
stat notes.txt
```

Suggested Screenshot:

```text
stat-after-chown.png
```

---

#### Example 16: Compare Metadata of Two Files

## Command

```bash
stat file1.txt file2.txt
```

### Command Explanation

Displays metadata of two files together for comparison.

### Expected Output

```text
File: file1.txt
...

File: file2.txt
...
```

### Real-World Use Case

Useful when comparing backup files or configuration files.

### Screenshot Command

```bash
stat file1.txt file2.txt
```

Suggested Screenshot:

```text
stat-compare-files.png
```

---

#### Example 17: Display File Name and Size Together

## Command

```bash
stat -c "File: %n | Size: %s bytes" notes.txt
```

### Command Explanation

Displays the file name and file size in a custom format.

### Expected Output

```text
File: notes.txt | Size: 2048 bytes
```

### Real-World Use Case

Useful in shell scripts and automation reports.

### Screenshot Command

```bash
stat -c "File: %n | Size: %s bytes" notes.txt
```

Suggested Screenshot:

```text
stat-custom-format.png
```

---

#### Example 18: Display Owner, Group and Permissions

## Command

```bash
stat -c "Owner: %U | Group: %G | Permissions: %A" notes.txt
```

### Command Explanation

Displays selected metadata in a customized format.

### Expected Output

```text
Owner: rahul | Group: developers | Permissions: -rw-r--r--
```

### Real-World Use Case

Useful for quick audits and system administration scripts.

### Screenshot Command

```bash
stat -c "Owner: %U | Group: %G | Permissions: %A" notes.txt
```

Suggested Screenshot:

```text
stat-owner-group-permissions.png
```

---

#### Example 19: Display Inode and File Name

## Command

```bash
stat -c "Inode: %i | File: %n" notes.txt
```

### Command Explanation

Displays the inode number along with the file name.

### Expected Output

```text
Inode: 157286 | File: notes.txt
```

### Real-World Use Case

Useful when troubleshooting hard links or filesystem issues.

### Screenshot Command

```bash
stat -c "Inode: %i | File: %n" notes.txt
```

Suggested Screenshot:

```text
stat-inode-file.png
```

---

#### Example 20: Display Complete Metadata of the Current Directory

## Command

```bash
stat .
```

### Command Explanation

Displays complete metadata of the current working directory.

### Expected Output

```text
File: .
Size: 4096
Access: (0755/drwxr-xr-x)
```

### Real-World Use Case

Useful for checking the permissions, ownership, and timestamps of the current project directory.

### Screenshot Command

```bash
stat .
```

Suggested Screenshot:

```text
stat-current-directory.png
```

---

### Key Learning Points

- `%x` → Last Access Time (atime)
- `%y` → Last Modification Time (mtime)
- `%z` → Last Status Change Time (ctime)
- `stat` helps verify permission and ownership changes after using `chmod` and `chown`.
- The `-c` option allows customized output, making `stat` very useful for shell scripting and automation.
- `stat` is commonly used for auditing files, troubleshooting permissions, and analyzing filesystem metadata.

---

## stat Practice Exercises (Part 3B.3)

This section contains hands-on practice exercises to help you master the `stat` command. Complete these exercises on your Linux system and capture screenshots for your GitHub repository.

---

### Practice Exercise 1: Display File Metadata

### Commands

```bash
touch notes.txt
stat notes.txt
```

### Task

Create a file and display its complete metadata.

### Verify

- File name
- File size
- Permissions
- Owner
- Group
- Timestamps

---

### Practice Exercise 2: Display Directory Metadata

### Commands

```bash
mkdir project
stat project
```

### Task

Display metadata of a directory.

### Verify

- Directory permissions
- Owner
- Group
- Inode number

---

### Practice Exercise 3: Display Metadata of Multiple Files

### Commands

```bash
touch file1.txt file2.txt
stat file1.txt file2.txt
```

### Task

Compare metadata of multiple files.

---

### Practice Exercise 4: Display Only File Name

### Command

```bash
stat -c "%n" notes.txt
```

### Task

Display only the filename.

### Expected Output

```text
notes.txt
```

---

### Practice Exercise 5: Display File Size

### Command

```bash
stat -c "%s" notes.txt
```

### Task

Display the size of the file in bytes.

---

### Practice Exercise 6: Display Permissions

### Commands

```bash
chmod 755 notes.txt
stat -c "%A" notes.txt
stat -c "%a" notes.txt
```

### Task

Display symbolic and numeric permissions.

### Expected Output

```text
-rwxr-xr-x
755
```

---

### Practice Exercise 7: Display Owner and Group

### Commands

```bash
stat -c "%U" notes.txt
stat -c "%G" notes.txt
```

### Task

Display the file owner and group.

---

### Practice Exercise 8: Display Inode Number

### Command

```bash
stat -c "%i" notes.txt
```

### Task

Display the inode number of the file.

---

### Practice Exercise 9: Display File Timestamps

### Commands

```bash
stat -c "%x" notes.txt
stat -c "%y" notes.txt
stat -c "%z" notes.txt
```

### Task

Observe the Access, Modify, and Change timestamps.

---

### Practice Exercise 10: Verify Permission Change

### Commands

```bash
chmod 644 notes.txt
stat notes.txt
```

### Task

Verify that the updated permissions are reflected in the metadata.

---

### Practice Exercise 11: Verify Ownership Change

### Commands

```bash
sudo chown $USER:$USER notes.txt
stat notes.txt
```

> Replace `$USER:$USER` with another valid user and group if you are practicing ownership changes between different users.

### Task

Verify the updated owner and group information.

---

### Screenshot Guide

Capture screenshots of the following commands and their outputs.

---

### Screenshot 1

```bash
stat notes.txt
```

Suggested Filename

```text
stat-file-details.png
```

---

### Screenshot 2

```bash
stat project
```

Suggested Filename

```text
stat-directory-details.png
```

---

### Screenshot 3

```bash
stat file1.txt file2.txt
```

Suggested Filename

```text
stat-multiple-files.png
```

---

### Screenshot 4

```bash
stat -c "%n" notes.txt
```

Suggested Filename

```text
stat-filename.png
```

---

### Screenshot 5

```bash
stat -c "%s" notes.txt
```

Suggested Filename

```text
stat-filesize.png
```

---

### Screenshot 6

```bash
stat -c "%A" notes.txt
stat -c "%a" notes.txt
```

Suggested Filename

```text
stat-permissions.png
```

---

### Screenshot 7

```bash
stat -c "%U" notes.txt
stat -c "%G" notes.txt
```

Suggested Filename

```text
stat-owner-group.png
```

---

### Screenshot 8

```bash
stat -c "%i" notes.txt
```

Suggested Filename

```text
stat-inode.png
```

---

### Screenshot 9

```bash
stat -c "%x" notes.txt
stat -c "%y" notes.txt
stat -c "%z" notes.txt
```

Suggested Filename

```text
stat-timestamps.png
```

---

### Screenshot 10

```bash
chmod 644 notes.txt
stat notes.txt
```

Suggested Filename

```text
stat-after-chmod.png
```

---

### Screenshot 11

```bash
sudo chown $USER:$USER notes.txt
stat notes.txt
```

Suggested Filename

```text
stat-after-chown.png
```

---

### Common Errors & Troubleshooting

### Error 1: No such file or directory

### Problem

```bash
stat file.txt
```

Output:

```text
stat: cannot stat 'file.txt': No such file or directory
```

### Reason

The specified file does not exist.

### Solution

Check available files:

```bash
ls
```

Or create the file:

```bash
touch file.txt
```

---

### Error 2: Permission denied

### Problem

```bash
stat /root
```

Output:

```text
stat: cannot stat '/root': Permission denied
```

### Reason

The current user does not have permission to access the directory.

### Solution

```bash
sudo stat /root
```

---

### Error 3: Incorrect Filename

### Problem

```bash
stat Note.txt
```

Output:

```text
No such file or directory
```

### Reason

Linux filenames are case-sensitive.

### Solution

Use the correct filename:

```bash
stat notes.txt
```

---

### Error 4: Birth Time Not Displayed

### Problem

The **Birth** field is missing from the output.

### Reason

Some Linux filesystems do not store or display file creation time.

### Solution

This is normal behavior. Use `Access`, `Modify`, and `Change` times instead if Birth time is unavailable.

---

### Error 5: Incorrect Permission Interpretation

### Problem

Confusing `Access` permissions with timestamps.

### Solution

Remember:

- `Access: (0644/-rw-r--r--)` → Permissions
- `Access: 2026-07-21 ...` → Last access timestamp

These are two different sections of the output.

---

### Best Practices

- Use `stat` to verify file metadata after running `chmod` or `chown`.
- Combine `stat` with `ls -l` for complete file inspection.
- Use the `-c` option to display only the information you need.
- Verify timestamps when troubleshooting file modifications.
- Use `stat` in shell scripts for reporting and automation.
- Compare metadata of files before deleting or backing them up.

---

### Cleanup Commands

After completing the exercises, remove the practice files and directories.

```bash
rm -f notes.txt file1.txt file2.txt
rm -rf project
```

### Purpose

These commands clean up all temporary files and directories created during the practice exercises, keeping your working environment organized.
