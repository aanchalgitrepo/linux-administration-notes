# 📂 Part 10.1 – Introduction to File Searching (`find` & `grep`)

File searching is one of the most important skills in Linux Administration, DevOps, Cloud Computing, AWS, Cybersecurity, and System Administration. Linux provides powerful command-line utilities to locate files, directories, and text efficiently.

The two most commonly used commands are:

- **`find`** → Searches for files and directories.
- **`grep`** → Searches for text or patterns inside files.

---

# 📖 Definition

**File Searching** is the process of locating files, directories, or specific text within files using Linux commands.

Linux provides several search utilities, but **`find`** and **`grep`** are the most powerful and widely used.

These commands are essential for:

- Linux Administration
- DevOps
- AWS & Cloud Computing
- Technical Support
- Cybersecurity
- System Administration

---

# 📂 What is File Searching?

File Searching is the process of locating:

- Files
- Directories
- Configuration files
- Log files
- Scripts
- Text inside files
- Recently modified files
- Large files
- Files owned by a particular user

Without file searching tools, finding information on systems containing thousands or even millions of files would be difficult and time-consuming.

---

# 🔍 What is `find`?

The **`find`** command searches for **files and directories** based on various conditions.

It can search using:

- File name
- Directory name
- File type
- File size
- Owner
- Group
- Permissions
- Modification time
- Access time
- Empty files/directories

### Example

```bash
find . -name "*.txt"
```

**Output**

```text
./notes.txt
./docs/readme.txt
```

**Use Case**

Find all `.txt` files inside the current directory and its subdirectories.

---

# 🔎 What is `grep`?

The **`grep`** command searches for **text or patterns inside files**.

It supports:

- Plain text search
- Case-insensitive search
- Recursive search
- Regular expressions
- Multiple pattern matching

### Example

```bash
grep "ERROR" app.log
```

**Output**

```text
ERROR: Database connection failed
```

**Use Case**

Find all lines containing the word **ERROR** inside a log file.

---

# 🎯 Why File Searching is Used

File searching helps administrators and developers quickly locate files and information.

### Common Uses

- Find configuration files
- Search log files
- Locate scripts
- Find large files
- Find recently modified files
- Search application errors
- Troubleshoot production servers
- Audit user files
- Automate system administration tasks

### Real-World Examples

| Task | Command |
|------|---------|
| Find all log files | `find /var/log -name "*.log"` |
| Search failed logins | `grep "Failed" /var/log/auth.log` |
| Find files larger than 100 MB | `find / -size +100M` |
| Search SSH configuration | `grep "Port" /etc/ssh/sshd_config` |

---

# ⚖️ Difference between `find` and `grep`

| Feature | `find` | `grep` |
|----------|--------|---------|
| Purpose | Search files/directories | Search text inside files |
| Searches | File names and attributes | File contents |
| Works On | Filesystem | Text data |
| Output | File paths | Matching lines |
| Recursive Search | Yes | Yes (`-r`) |
| Regular Expressions | Limited | Fully supported |
| Common Use | Locate files | Search specific text |

### Example

Find shell scripts:

```bash
find . -name "*.sh"
```

Search the word **backup** inside a script:

```bash
grep "backup" script.sh
```

---

# 📝 `find` Syntax

## Basic Syntax

```bash
find [path] [options] [expression]
```

## General Syntax

```bash
find /path [options]
```

### Examples

Search by filename:

```bash
find . -name "notes.txt"
```

Search directories only:

```bash
find . -type d
```

Search files larger than 10 MB:

```bash
find . -size +10M
```

---

# 📝 `grep` Syntax

## Basic Syntax

```bash
grep [options] "pattern" file
```

## General Syntax

```bash
grep option "text" filename
```

### Examples

Search text:

```bash
grep "Linux" notes.txt
```

Recursive search:

```bash
grep -r "ERROR" /var/log
```

Case-insensitive search:

```bash
grep -i "ubuntu" file.txt
```

---

# ⚙️ Common `find` Options

| Option | Description |
|---------|-------------|
| `-name` | Search by filename |
| `-iname` | Case-insensitive filename search |
| `-type f` | Search files only |
| `-type d` | Search directories only |
| `-size` | Search by file size |
| `-user` | Search by owner |
| `-group` | Search by group |
| `-perm` | Search by permissions |
| `-mtime` | Search by modification time |
| `-atime` | Search by access time |
| `-empty` | Search empty files/directories |
| `-exec` | Execute a command on matched files |
| `-delete` | Delete matched files |

### Example

```bash
find . -size +50M
```

---

# ⚙️ Common `grep` Options

| Option | Description |
|---------|-------------|
| `-i` | Ignore case |
| `-r` | Recursive search |
| `-n` | Show line numbers |
| `-v` | Show non-matching lines |
| `-c` | Count matching lines |
| `-l` | Display matching filenames |
| `-w` | Match whole words only |
| `-E` | Use extended regular expressions |
| `-F` | Search fixed strings |
| `--color=auto` | Highlight matched text |

### Example

```bash
grep -n "main" script.sh
```

---

# 🌟 Wildcards

Wildcards are special characters used to match filenames.

| Wildcard | Meaning |
|-----------|---------|
| `*` | Matches zero or more characters |
| `?` | Matches exactly one character |
| `[abc]` | Matches any listed character |
| `[a-z]` | Matches any lowercase letter |
| `[0-9]` | Matches any digit |

### Examples

Find all text files:

```bash
find . -name "*.txt"
```

Find all shell scripts:

```bash
find . -name "*.sh"
```

Find files starting with "log":

```bash
find . -name "log*"
```

---

# 🧩 Regular Expressions (Regex)

A **Regular Expression (Regex)** is a search pattern used to match text.

`grep` supports powerful regular expression searching.

| Pattern | Meaning |
|----------|---------|
| `^` | Beginning of line |
| `$` | End of line |
| `.` | Any single character |
| `*` | Zero or more occurrences |
| `+` | One or more occurrences (`grep -E`) |
| `[0-9]` | Any digit |
| `[a-z]` | Lowercase letters |

### Examples

Search lines starting with "Error":

```bash
grep "^Error" log.txt
```

Search lines ending with ".conf":

```bash
grep ".conf$" files.txt
```

Search lines containing numbers:

```bash
grep "[0-9]" data.txt
```

---

# 📊 `find` vs `locate`

| Feature | `find` | `locate` |
|----------|--------|----------|
| Search Method | Live filesystem | Prebuilt database |
| Speed | Slower | Faster |
| Accuracy | Always up to date | Depends on updated database |
| Requires Database | ❌ No | ✅ Yes |
| Search Criteria | Multiple conditions | Filename only |
| Best Use | Advanced searching | Quick filename lookup |

### Example

Using `find`

```bash
find /home -name "notes.txt"
```

Using `locate`

```bash
locate notes.txt
```

### Install `locate`

**Ubuntu / Debian**

```bash
sudo apt update
sudo apt install plocate
sudo updatedb
```

**CentOS / RHEL**

```bash
sudo yum install mlocate
sudo updatedb
```

---

# 📊 `grep` vs `egrep` vs `fgrep`

| Command | Description | Recommended Usage |
|----------|-------------|-------------------|
| `grep` | Standard text search | ✅ Yes |
| `egrep` | Extended regular expressions | ⚠ Deprecated (use `grep -E`) |
| `fgrep` | Fixed string search | ⚠ Deprecated (use `grep -F`) |

### Modern Equivalents

Instead of:

```bash
egrep "error|warning" file.txt
```

Use:

```bash
grep -E "error|warning" file.txt
```

Instead of:

```bash
fgrep "Linux" file.txt
```

Use:

```bash
grep -F "Linux" file.txt
```

---

# 🐧 Ubuntu / CentOS / WSL Notes

## Ubuntu

- `find` is installed by default.
- `grep` is installed by default.
- `locate` may need to be installed manually.

Install `locate`:

```bash
sudo apt update
sudo apt install plocate
sudo updatedb
```

---

## CentOS / RHEL

- `find` is available by default.
- `grep` is available by default.
- `locate` can be installed if required.

CentOS 7

```bash
sudo yum install mlocate
sudo updatedb
```

CentOS Stream / RHEL 8+

```bash
sudo dnf install mlocate
sudo updatedb
```

---

## WSL (Windows Subsystem for Linux)

- `find` works exactly like Ubuntu.
- `grep` works exactly like Ubuntu.
- `locate` may not be installed by default.

Install `locate`:

```bash
sudo apt update
sudo apt install plocate
sudo updatedb
```

> **WSL Note**
>
> - `find` and `grep` work best inside the Linux filesystem (e.g., `/home/user`).
> - Searching inside Windows-mounted drives (`/mnt/c`, `/mnt/d`) may be slower because WSL accesses Windows files through a mounted filesystem.
> - No special configuration is required for `find` or `grep`.

---

# 📌 Key Takeaways

- `find` searches **files and directories**.
- `grep` searches **text inside files**.
- `find` is used for locating files based on attributes like name, size, owner, permissions, and timestamps.
- `grep` is used for searching text in log files, configuration files, and source code.
- `find` searches the live filesystem, while `locate` searches a prebuilt database.
- Use `grep -E` instead of the deprecated `egrep`, and `grep -F` instead of `fgrep`.
- Mastering `find` and `grep` is essential for Linux Administration, DevOps, Cloud Computing, AWS, Technical Support, and System Administration.

---

# 📂 Part 10.2A – Practical Examples (Examples 1–10)

This section contains beginner-friendly practical examples of the **`find`** and **`grep`** commands. These examples are commonly used in **Linux Administration, DevOps, AWS, Cloud Computing, Technical Support, and System Administration**.

> **Note for WSL Users:** All examples work in **Ubuntu, CentOS, and WSL** unless otherwise specified.

---

# Example 1 – Find File by Name

## ✅ Practical Example

Find a file named **notes.txt** in the current directory and all subdirectories.

### ✅ Command

```bash
find . -name "notes.txt"
```

### ✅ Command Explanation

- `find` → Searches for files and directories.
- `.` → Search starts from the current directory.
- `-name` → Search using an exact filename.
- `"notes.txt"` → File to search.

### ✅ Expected Output

```text
./documents/notes.txt
```

### ✅ Real-World Use Case

Locate a configuration file, script, or document when you don't remember its exact location.

### ✅ Screenshot Command

```bash
find . -name "notes.txt"
```

### ✅ Ubuntu

Works by default.

### ✅ CentOS

Works by default.

### ✅ WSL Note

Works exactly like Ubuntu.

---

# Example 2 – Find Directory

## ✅ Practical Example

Find a directory named **project**.

### ✅ Command

```bash
find . -type d -name "project"
```

### ✅ Command Explanation

- `-type d` → Search directories only.
- `-name` → Match directory name.

### ✅ Expected Output

```text
./projects/project
```

### ✅ Real-World Use Case

Locate project folders or application directories on large systems.

### ✅ Screenshot Command

```bash
find . -type d -name "project"
```

### ✅ Ubuntu

Supported.

### ✅ CentOS

Supported.

### ✅ WSL Note

Works without modification.

---

# Example 3 – Find Files by Extension

## ✅ Practical Example

Find all shell scripts.

### ✅ Command

```bash
find . -name "*.sh"
```

### ✅ Command Explanation

- `*.sh` matches every shell script.

### ✅ Expected Output

```text
./backup.sh
./scripts/install.sh
```

### ✅ Real-World Use Case

Locate automation scripts before editing or executing them.

### ✅ Screenshot Command

```bash
find . -name "*.sh"
```

### ✅ Ubuntu

Supported.

### ✅ CentOS

Supported.

### ✅ WSL Note

Fully supported.

---

# Example 4 – Find Empty Files

## ✅ Practical Example

Find all empty files.

### ✅ Command

```bash
find . -type f -empty
```

### ✅ Command Explanation

- `-type f` → Files only.
- `-empty` → Empty files.

### ✅ Expected Output

```text
./empty.txt
./logs/debug.log
```

### ✅ Real-World Use Case

Remove unused files and clean storage.

### ✅ Screenshot Command

```bash
find . -type f -empty
```

### ✅ Ubuntu

Supported.

### ✅ CentOS

Supported.

### ✅ WSL Note

Works normally.

---

# Example 5 – Find Empty Directories

## ✅ Practical Example

Find empty directories.

### ✅ Command

```bash
find . -type d -empty
```

### ✅ Command Explanation

- `-type d` → Directories only.
- `-empty` → Empty directories.

### ✅ Expected Output

```text
./old_project
./temp
```

### ✅ Real-World Use Case

Identify unused folders before cleanup.

### ✅ Screenshot Command

```bash
find . -type d -empty
```

### ✅ Ubuntu

Supported.

### ✅ CentOS

Supported.

### ✅ WSL Note

Works the same as Ubuntu.

---

# Example 6 – Find Large Files

## ✅ Practical Example

Find files larger than **10 MB**.

### ✅ Command

```bash
find . -type f -size +10M
```

### ✅ Command Explanation

- `-size +10M` → Files larger than 10 MB.

### ✅ Expected Output

```text
./videos/demo.mp4
./backup/database.sql
```

### ✅ Real-World Use Case

Locate large files consuming disk space.

### ✅ Screenshot Command

```bash
find . -type f -size +10M
```

### ✅ Ubuntu

Supported.

### ✅ CentOS

Supported.

### ✅ WSL Note

Works normally.

---

# Example 7 – Find Recently Modified Files

## ✅ Practical Example

Find files modified within the last 7 days.

### ✅ Command

```bash
find . -type f -mtime -7
```

### ✅ Command Explanation

- `-mtime -7` → Modified during the last 7 days.

### ✅ Expected Output

```text
./report.txt
./config.yml
```

### ✅ Real-World Use Case

Locate recently edited configuration files or project files.

### ✅ Screenshot Command

```bash
find . -type f -mtime -7
```

### ✅ Ubuntu

Supported.

### ✅ CentOS

Supported.

### ✅ WSL Note

Works without changes.

---

# Example 8 – Search Text Using `grep`

## ✅ Practical Example

Search for the word **ERROR** inside a log file.

### ✅ Command

```bash
grep "ERROR" app.log
```

### ✅ Command Explanation

- `grep` → Searches text.
- `"ERROR"` → Pattern to search.
- `app.log` → File to search.

### ✅ Expected Output

```text
ERROR: Database connection failed
ERROR: Permission denied
```

### ✅ Real-World Use Case

Quickly locate application errors inside log files.

### ✅ Screenshot Command

```bash
grep "ERROR" app.log
```

### ✅ Ubuntu

Installed by default.

### ✅ CentOS

Installed by default.

### ✅ WSL Note

Works exactly like Ubuntu.

---

# Example 9 – Recursive Search Using `grep -r`

## ✅ Practical Example

Search for the word **password** in all files under the current directory.

### ✅ Command

```bash
grep -r "password" .
```

### ✅ Command Explanation

- `-r` → Recursive search.
- `.` → Current directory.

### ✅ Expected Output

```text
./config.yml:password=admin123
./settings.conf:password=root
```

### ✅ Real-World Use Case

Search configuration files or source code for specific values.

### ✅ Screenshot Command

```bash
grep -r "password" .
```

### ✅ Ubuntu

Supported.

### ✅ CentOS

Supported.

### ✅ WSL Note

Works normally.

---

# Example 10 – Case-Insensitive Search

## ✅ Practical Example

Search for the word **linux** regardless of uppercase or lowercase letters.

### ✅ Command

```bash
grep -i "linux" notes.txt
```

### ✅ Command Explanation

- `-i` → Ignore letter case.
- Searches **Linux**, **LINUX**, **linux**, or **LiNuX**.

### ✅ Expected Output

```text
Linux Administration
linux kernel
LINUX Commands
```

### ✅ Real-World Use Case

Useful when searching logs or documents where text casing is inconsistent.

### ✅ Screenshot Command

```bash
grep -i "linux" notes.txt
```

### ✅ Ubuntu

Supported.

### ✅ CentOS

Supported.

### ✅ WSL Note

Works exactly like Ubuntu.

---

# 📌 Summary

In this section, you learned how to:

- Search files by name.
- Find directories.
- Search by file extension.
- Locate empty files and directories.
- Find large files.
- Find recently modified files.
- Search text using `grep`.
- Search recursively with `grep -r`.
- Perform case-insensitive searches using `grep -i`.

These commands are used daily by Linux Administrators, DevOps Engineers, Cloud Engineers, and System Administrators for troubleshooting, automation, and server management.

---
