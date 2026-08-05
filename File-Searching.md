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

# 📂 Part 10.2B – Advanced Practical Examples (Examples 11–20)

This section covers advanced examples of the **`find`** and **`grep`** commands that are frequently used by **Linux Administrators, DevOps Engineers, Cloud Engineers, AWS Engineers, and System Administrators**.

> **Note:** These examples work on **Ubuntu, CentOS, RHEL, Amazon Linux, and WSL** (unless otherwise noted).

---

# Example 11 – Find Files by Owner

## ✅ Practical Example

Find all files owned by the user **rahul**.

### ✅ Command

```bash
find . -user rahul
```

### ✅ Command Explanation

- `find` → Searches files and directories.
- `.` → Current directory.
- `-user rahul` → Search files owned by the user **rahul**.

### ✅ Expected Output

```text
./documents/report.txt
./projects/script.sh
```

### ✅ Real-World Use Case

System administrators use this command to audit files owned by a specific user before account deletion or migration.

### ✅ Screenshot Command

```bash
find . -user rahul
```

---

# Example 12 – Find Files by Permissions

## ✅ Practical Example

Find all files with permission **644**.

### ✅ Command

```bash
find . -perm 644
```

### ✅ Command Explanation

- `-perm` → Searches based on file permissions.
- `644` → Exact permission value.

### ✅ Expected Output

```text
./notes.txt
./README.md
```

### ✅ Real-World Use Case

Useful for verifying file permissions during security audits.

### ✅ Screenshot Command

```bash
find . -perm 644
```

---

# Example 13 – Find Files by Size

## ✅ Practical Example

Find all files larger than **100 MB**.

### ✅ Command

```bash
find . -type f -size +100M
```

### ✅ Command Explanation

- `-type f` → Search files only.
- `-size +100M` → Files larger than 100 MB.

### ✅ Expected Output

```text
./backup/database.sql
./videos/demo.mp4
```

### ✅ Real-World Use Case

Identify large files consuming disk space before performing cleanup.

### ✅ Screenshot Command

```bash
find . -type f -size +100M
```

---

# Example 14 – Find and Delete Files

## ✅ Practical Example

Delete all temporary (`.tmp`) files.

### ✅ Command

```bash
find . -name "*.tmp" -delete
```

### ✅ Command Explanation

- `-name "*.tmp"` → Search all `.tmp` files.
- `-delete` → Delete matched files.

### ✅ Expected Output

```text
(No output if deletion succeeds)
```

### ✅ Real-World Use Case

Automatically remove temporary files during scheduled maintenance.

> ⚠️ **Warning:** Verify the search results before using `-delete`, as deleted files cannot be recovered easily.

### ✅ Screenshot Command

```bash
find . -name "*.tmp"
```

Then:

```bash
find . -name "*.tmp" -delete
```

---

# Example 15 – Execute Commands Using `find -exec`

## ✅ Practical Example

Display detailed information for every shell script found.

### ✅ Command

```bash
find . -name "*.sh" -exec ls -l {} \;
```

### ✅ Command Explanation

- `-exec` → Execute a command on each matched file.
- `{}` → Placeholder for the matched filename.
- `\;` → Ends the `-exec` command.

### ✅ Expected Output

```text
-rwxr-xr-x user user 450 Jul 22 backup.sh
-rwxr-xr-x user user 320 Jul 23 deploy.sh
```

### ✅ Real-World Use Case

Execute operations such as listing, copying, compressing, or changing permissions on multiple files.

### ✅ Screenshot Command

```bash
find . -name "*.sh" -exec ls -l {} \;
```

---

# Example 16 – Search Multiple Patterns

## ✅ Practical Example

Search for **ERROR** or **WARNING** inside a log file.

### ✅ Command

```bash
grep -E "ERROR|WARNING" app.log
```

### ✅ Command Explanation

- `-E` → Enables extended regular expressions.
- `ERROR|WARNING` → Matches either pattern.

### ✅ Expected Output

```text
ERROR: Database connection failed
WARNING: Low disk space
```

### ✅ Real-World Use Case

Monitor application logs for multiple error conditions.

### ✅ Screenshot Command

```bash
grep -E "ERROR|WARNING" app.log
```

---

# Example 17 – Show Line Numbers with `grep -n`

## ✅ Practical Example

Display matching lines along with their line numbers.

### ✅ Command

```bash
grep -n "main" script.sh
```

### ✅ Command Explanation

- `-n` → Shows line numbers with each matching line.

### ✅ Expected Output

```text
12:main() {
45:echo "main completed"
```

### ✅ Real-World Use Case

Locate code quickly while debugging or reviewing configuration files.

### ✅ Screenshot Command

```bash
grep -n "main" script.sh
```

---

# Example 18 – Count Matches with `grep -c`

## ✅ Practical Example

Count how many lines contain the word **ERROR**.

### ✅ Command

```bash
grep -c "ERROR" app.log
```

### ✅ Command Explanation

- `-c` → Counts matching lines instead of displaying them.

### ✅ Expected Output

```text
8
```

### ✅ Real-World Use Case

Generate quick statistics from log files or reports.

### ✅ Screenshot Command

```bash
grep -c "ERROR" app.log
```

---

# Example 19 – Invert Matches Using `grep -v`

## ✅ Practical Example

Display all lines **except** comments.

### ✅ Command

```bash
grep -v "^#" config.conf
```

### ✅ Command Explanation

- `-v` → Displays non-matching lines.
- `^#` → Matches lines beginning with `#`.

### ✅ Expected Output

```text
Port 22
PermitRootLogin no
PasswordAuthentication yes
```

### ✅ Real-World Use Case

View active configuration settings while ignoring comments.

### ✅ Screenshot Command

```bash
grep -v "^#" config.conf
```

---

# Example 20 – Search Logs Using `grep`

## ✅ Practical Example

Search SSH authentication logs for failed login attempts.

### ✅ Ubuntu / Debian

```bash
grep "Failed" /var/log/auth.log
```

### ✅ CentOS / RHEL

```bash
grep "Failed" /var/log/secure
```

### ✅ WSL Note

WSL usually does **not** generate `/var/log/auth.log` or `/var/log/secure` unless an SSH server and logging services are configured. You can create a sample log file to practice:

```bash
echo "Failed password for user" > sample.log
grep "Failed" sample.log
```

### ✅ Command Explanation

- Searches authentication logs for failed login attempts.
- Helps identify unauthorized access attempts.

### ✅ Expected Output

```text
Failed password for invalid user admin
Failed password for root
```

### ✅ Real-World Use Case

Security teams and system administrators use this command to investigate suspicious login activity and monitor server security.

### ✅ Screenshot Command

**Ubuntu**

```bash
grep "Failed" /var/log/auth.log
```

**CentOS**

```bash
grep "Failed" /var/log/secure
```

**WSL Practice**

```bash
grep "Failed" sample.log
```

---

# 🎯 Summary

In this section, you learned how to:

- Find files by owner.
- Find files based on permissions.
- Locate files by size.
- Delete files using `find`.
- Execute commands using `find -exec`.
- Search multiple patterns with `grep -E`.
- Display line numbers using `grep -n`.
- Count matching lines using `grep -c`.
- Exclude matching lines using `grep -v`.
- Search authentication and application logs using `grep`.

These advanced commands are used daily by **Linux Administrators, DevOps Engineers, Cloud Engineers, Security Engineers, and System Administrators** for troubleshooting, automation, auditing, and server maintenance.

---

# 📂 Part 10.3 – Practice Exercises

This section contains hands-on exercises to help you practice the **`find`** and **`grep`** commands. These exercises are designed for beginners as well as aspiring **Linux Administrators, DevOps Engineers, AWS Engineers, Cloud Engineers, Technical Support Engineers, and System Administrators**.

> **Note for WSL Users:** Most exercises work without any changes. Some log file examples differ because WSL does not always generate the same system logs as a full Linux installation.

---

# 🎯 Practice Exercise 1 – Find a File by Name

## ✅ Objective

Create a file and search for it.

### Steps

```bash
mkdir -p ~/search-practice
cd ~/search-practice

touch notes.txt

find . -name "notes.txt"
```

### Expected Output

```text
./notes.txt
```

---

# 🎯 Practice Exercise 2 – Find a Directory

## ✅ Objective

Create and locate a directory.

### Steps

```bash
mkdir project

find . -type d -name "project"
```

### Expected Output

```text
./project
```

---

# 🎯 Practice Exercise 3 – Find Files by Extension

## ✅ Objective

Find all shell script files.

### Steps

```bash
touch backup.sh

touch deploy.sh

find . -name "*.sh"
```

### Expected Output

```text
./backup.sh
./deploy.sh
```

---

# 🎯 Practice Exercise 4 – Find Empty Files

## ✅ Objective

Locate empty files.

### Steps

```bash
touch empty.txt

find . -type f -empty
```

### Expected Output

```text
./empty.txt
```

---

# 🎯 Practice Exercise 5 – Find Empty Directories

## ✅ Objective

Locate empty directories.

### Steps

```bash
mkdir empty-folder

find . -type d -empty
```

### Expected Output

```text
./empty-folder
```

---

# 🎯 Practice Exercise 6 – Search Text Using `grep`

## ✅ Objective

Search for a word inside a file.

### Steps

```bash
echo "Linux Administration" > notes.txt
echo "AWS DevOps" >> notes.txt

grep "Linux" notes.txt
```

### Expected Output

```text
Linux Administration
```

---

# 🎯 Practice Exercise 7 – Recursive Search

## ✅ Objective

Search inside all files recursively.

### Steps

```bash
mkdir logs

echo "ERROR: Database failed" > logs/app.log

grep -r "ERROR" .
```

### Expected Output

```text
./logs/app.log:ERROR: Database failed
```

---

# 🎯 Practice Exercise 8 – Case-Insensitive Search

## ✅ Objective

Search regardless of uppercase or lowercase letters.

### Steps

```bash
echo "Linux" > os.txt
echo "linux" >> os.txt
echo "LINUX" >> os.txt

grep -i "linux" os.txt
```

### Expected Output

```text
Linux
linux
LINUX
```

---

# 🎯 Practice Exercise 9 – Count Matching Lines

## ✅ Objective

Count occurrences of a word.

### Steps

```bash
echo "ERROR" > app.log
echo "ERROR" >> app.log
echo "INFO" >> app.log

grep -c "ERROR" app.log
```

### Expected Output

```text
2
```

---

# 🎯 Practice Exercise 10 – Show Line Numbers

## ✅ Objective

Display matching lines with their line numbers.

### Steps

```bash
grep -n "Linux" notes.txt
```

### Expected Output

```text
1:Linux Administration
```

---

# 🎯 Practice Exercise 11 – Find Large Files

## ✅ Objective

Locate files larger than a specific size.

### Steps

```bash
find . -type f -size +1M
```

### Expected Output

Displays files larger than **1 MB**.

---

# 🎯 Practice Exercise 12 – Find Recently Modified Files

## ✅ Objective

Find files modified within the last day.

### Steps

```bash
find . -type f -mtime -1
```

### Expected Output

Displays files modified during the last **24 hours**.

---

# 🐧 WSL-Friendly Exercises

The following exercises work perfectly in WSL:

- Find a file by name.
- Find directories.
- Search by extension.
- Search file contents using `grep`.
- Recursive search using `grep -r`.
- Count matching lines using `grep -c`.
- Case-insensitive search using `grep -i`.
- Show line numbers using `grep -n`.
- Find recently modified files.
- Find large files.

> **Tip:** Practice inside your home directory (`~/search-practice`) instead of Windows-mounted directories (`/mnt/c`) for better performance.

---

# 🐧 Ubuntu Server Exercises

Practice the following commands on an Ubuntu Server:

```bash
find /etc -name "*.conf"

find /var/log -name "*.log"

grep "Port" /etc/ssh/sshd_config

grep -r "ERROR" /var/log
```

### Learning Objectives

- Locate configuration files.
- Search system logs.
- Explore SSH configuration.
- Practice recursive log searching.

---

# 🐧 CentOS Equivalents

The same commands work on CentOS.

Examples:

Find configuration files:

```bash
find /etc -name "*.conf"
```

Search SSH configuration:

```bash
grep "Port" /etc/ssh/sshd_config
```

Search authentication logs:

```bash
grep "Failed" /var/log/secure
```

Search all log files:

```bash
grep -r "ERROR" /var/log
```

> **Note:** CentOS stores authentication logs in **`/var/log/secure`**, whereas Ubuntu uses **`/var/log/auth.log`**.

---

# 📸 Screenshot Guide

Capture screenshots of the following commands for your GitHub repository:

```bash
find . -name "notes.txt"
```

```bash
find . -type d -name "project"
```

```bash
find . -name "*.sh"
```

```bash
find . -type f -empty
```

```bash
find . -type d -empty
```

```bash
find . -type f -size +1M
```

```bash
find . -type f -mtime -1
```

```bash
grep "Linux" notes.txt
```

```bash
grep -r "ERROR" .
```

```bash
grep -i "linux" os.txt
```

```bash
grep -n "Linux" notes.txt
```

```bash
grep -c "ERROR" app.log
```

---

# ❗ Common Errors & Troubleshooting

## 1. No such file or directory

### Error

```text
find: ‘notes.txt’: No such file or directory
```

### Cause

The specified file or directory does not exist.

### Solution

Verify the path using:

```bash
ls
pwd
```

---

## 2. Permission Denied

### Error

```text
find: '/root': Permission denied
```

### Cause

You do not have permission to access the directory.

### Solution

Use:

```bash
sudo find /root
```

---

## 3. No Output from `find`

### Cause

No files match the search criteria.

### Solution

Check the filename, extension, or search path.

Example:

```bash
find . -name "*.txt"
```

---

## 4. No Matches Found with `grep`

### Cause

The specified text does not exist in the file.

### Solution

Verify file contents:

```bash
cat filename
```

---

## 5. Binary File Matches

### Cause

`grep` detected binary content.

### Solution

Search only text files or use:

```bash
grep -a "text" filename
```

---

## 6. Slow Search Performance

### Cause

Searching very large directories.

### Solution

Limit the search path.

Example:

```bash
find ~/Documents -name "*.txt"
```

Instead of:

```bash
find /
```

---

# ✅ Best Practices

- Search specific directories instead of the entire filesystem whenever possible.
- Use meaningful filenames for easier searching.
- Verify search results before deleting files.
- Use `find -exec` carefully.
- Test commands before combining them with `-delete`.
- Use `grep -i` when text case is uncertain.
- Use `grep -n` for easier debugging.
- Use `grep -r` for recursive searches in source code or logs.
- Avoid running `find /` unnecessarily on production servers.
- Practice inside a dedicated directory before working on system files.

---

# 🧹 Cleanup Commands

Remove all practice files and directories after completing the exercises.

```bash
cd ~

rm -f ~/search-practice/notes.txt
rm -f ~/search-practice/backup.sh
rm -f ~/search-practice/deploy.sh
rm -f ~/search-practice/empty.txt
rm -f ~/search-practice/os.txt
rm -f ~/search-practice/app.log

rm -rf ~/search-practice/logs
rm -rf ~/search-practice/project
rm -rf ~/search-practice/empty-folder

rm -rf ~/search-practice
```

---

# 🎯 Summary

After completing these exercises, you should be able to:

- Search for files and directories using `find`.
- Search text within files using `grep`.
- Perform recursive searches.
- Find files based on size, type, and modification time.
- Count and filter search results.
- Troubleshoot common search-related errors.
- Use `find` and `grep` confidently in Ubuntu, CentOS, and WSL.

These practical exercises build the foundational skills required for **Linux Administration, DevOps, Cloud Computing, AWS, Technical Support, and System Administration**.

---

# 📂 Part 10.4A – Interview Questions & Answers (1–15)

This section contains **beginner to intermediate interview questions** on the **`find`** and **`grep`** commands. These questions are commonly asked in interviews for **Linux Administrator, DevOps Engineer, AWS Engineer, Cloud Engineer, Technical Support Engineer, and System Administrator** roles.

---

# Question 1 – What is the `find` command in Linux?

## ✅ Professional Answer

The **`find`** command is a Linux utility used to search for **files and directories** based on various criteria such as:

- File name
- File type
- Size
- Owner
- Group
- Permissions
- Modification time
- Access time

Unlike `locate`, the `find` command searches the **live filesystem**, ensuring that the results are always up to date.

### ✅ Example

```bash
find . -name "notes.txt"
```

This command searches for a file named **notes.txt** in the current directory and all of its subdirectories.

---

# Question 2 – What is the `grep` command?

## ✅ Professional Answer

The **`grep`** command is used to search for **specific text or patterns inside files**.

It supports:

- Plain text searching
- Case-insensitive searching
- Recursive searching
- Regular expressions
- Pattern matching

It is widely used for analyzing log files, configuration files, source code, and application output.

### ✅ Example

```bash
grep "ERROR" app.log
```

This command displays all lines containing the word **ERROR**.

---

# Question 3 – What is the difference between `find` and `grep`?

## ✅ Professional Answer

Both commands are used for searching, but they search different things.

| `find` | `grep` |
|---------|---------|
| Searches files and directories | Searches text inside files |
| Searches the filesystem | Searches file contents |
| Returns file paths | Returns matching lines |
| Uses file attributes | Uses text patterns |

### ✅ Example

Find shell scripts:

```bash
find . -name "*.sh"
```

Search the word **backup** inside a shell script:

```bash
grep "backup" backup.sh
```

---

# Question 4 – How do you search for a file by its name?

## ✅ Professional Answer

Use the **`-name`** option with the `find` command.

### ✅ Example

```bash
find . -name "config.yml"
```

This command searches for a file named **config.yml** in the current directory and all subdirectories.

---

# Question 5 – How do you search for files by extension?

## ✅ Professional Answer

Use the **`-name`** option with wildcard characters.

### ✅ Example

Search all text files:

```bash
find . -name "*.txt"
```

Search all shell scripts:

```bash
find . -name "*.sh"
```

This command returns every file with the specified extension.

---

# Question 6 – How do you search for files owned by a specific user?

## ✅ Professional Answer

Use the **`-user`** option with the `find` command.

### ✅ Example

```bash
find . -user rahul
```

This command displays all files owned by the user **rahul**.

It is commonly used during user account audits and ownership verification.

---

# Question 7 – How do you search for files with specific permissions?

## ✅ Professional Answer

Use the **`-perm`** option.

### ✅ Example

```bash
find . -perm 644
```

This command finds files with **644** permissions.

It is useful for security audits and permission verification.

---

# Question 8 – What is recursive searching?

## ✅ Professional Answer

Recursive searching means searching through a directory and **all of its subdirectories** automatically.

The `find` command searches recursively by default.

For `grep`, recursive searching is enabled using the **`-r`** option.

### ✅ Example

```bash
grep -r "ERROR" .
```

This command searches every file in the current directory and its subdirectories for the word **ERROR**.

---

# Question 9 – What are Regular Expressions (Regex)?

## ✅ Professional Answer

Regular Expressions (Regex) are search patterns used to match text efficiently.

Regex allows users to search for:

- Words
- Numbers
- Email addresses
- Dates
- Specific patterns

The `grep` command supports regular expressions.

### ✅ Example

Search lines starting with "Error":

```bash
grep "^Error" app.log
```

Search lines ending with ".conf":

```bash
grep ".conf$" files.txt
```

---

# Question 10 – What are some common options used with the `find` command?

## ✅ Professional Answer

Some commonly used options include:

| Option | Purpose |
|---------|----------|
| `-name` | Search by filename |
| `-type` | Search by file type |
| `-size` | Search by file size |
| `-user` | Search by owner |
| `-group` | Search by group |
| `-perm` | Search by permissions |
| `-mtime` | Search by modification time |
| `-empty` | Search empty files/directories |
| `-exec` | Execute commands on matched files |

### ✅ Example

```bash
find . -type f -size +100M
```

---

# Question 11 – What are some commonly used `grep` options?

## ✅ Professional Answer

Some of the most commonly used options are:

| Option | Purpose |
|---------|----------|
| `-i` | Ignore case |
| `-r` | Recursive search |
| `-n` | Show line numbers |
| `-v` | Show non-matching lines |
| `-c` | Count matching lines |
| `-l` | Display matching filenames |
| `-E` | Extended regular expressions |
| `-F` | Fixed string search |

### ✅ Example

```bash
grep -in "linux" notes.txt
```

This command performs a case-insensitive search and displays line numbers.

---

# Question 12 – How do you search for a word regardless of letter case?

## ✅ Professional Answer

Use the **`-i`** option with `grep`.

This option ignores uppercase and lowercase differences during the search.

### ✅ Example

```bash
grep -i "linux" notes.txt
```

It matches:

```text
Linux
LINUX
linux
LiNuX
```

---

# Question 13 – How do you display line numbers in `grep` output?

## ✅ Professional Answer

Use the **`-n`** option.

This option displays the line number before each matching line.

### ✅ Example

```bash
grep -n "main" script.sh
```

### Sample Output

```text
15:main()
38:echo "Main completed"
```

This is especially useful while debugging source code or configuration files.

---

# Question 14 – How do you count the number of matching lines in a file?

## ✅ Professional Answer

Use the **`-c`** option.

Instead of displaying matching lines, `grep` shows the total number of matching lines.

### ✅ Example

```bash
grep -c "ERROR" app.log
```

### Sample Output

```text
8
```

This indicates that **8 lines** contain the word **ERROR**.

---

# Question 15 – Why are `find` and `grep` important for Linux administrators?

## ✅ Professional Answer

`find` and `grep` are essential because they help administrators quickly locate files and search for information within those files.

These commands are used daily for:

- Troubleshooting
- Log analysis
- Configuration management
- Security auditing
- Automation scripts
- Monitoring
- System administration
- DevOps workflows

Using these commands improves productivity and reduces the time required to locate files or diagnose system issues.

### ✅ Example

Find SSH configuration files:

```bash
find /etc -name "sshd_config"
```

Search the SSH configuration for the listening port:

```bash
grep "^Port" /etc/ssh/sshd_config
```

These commands help administrators verify SSH configuration quickly.

---

# 📌 Key Takeaways

- `find` searches for **files and directories** based on attributes.
- `grep` searches for **text patterns inside files**.
- `find` supports searching by name, owner, permissions, size, and modification time.
- `grep` supports recursive searching, regular expressions, case-insensitive searches, and line numbering.
- Understanding `find` and `grep` is essential for Linux Administration, DevOps, AWS, Cloud Computing, Technical Support, and System Administration interviews.

---

# 📂 Part 10.4B – Interview Questions & Answers (16–30)

This section contains **advanced interview questions** on **`find`** and **`grep`**. These questions are commonly asked in interviews for **Linux Administrator, DevOps Engineer, AWS Engineer, Cloud Engineer, Site Reliability Engineer (SRE), and System Administrator** roles.

---

# Question 16 – How do you search for files larger than a specific size?

## ✅ Professional Answer

The **`-size`** option with the `find` command is used to search for files based on their size.

### ✅ Example

Find files larger than **100 MB**:

```bash
find . -type f -size +100M
```

This command displays all files larger than **100 MB** in the current directory and its subdirectories.

---

# Question 17 – How do you search for recently modified files?

## ✅ Professional Answer

The **`-mtime`** option searches files based on their modification time.

### ✅ Example

Find files modified within the last **7 days**:

```bash
find . -type f -mtime -7
```

This is commonly used to identify recently updated log files, configuration files, or project files.

---

# Question 18 – What is the purpose of the `-exec` option in the `find` command?

## ✅ Professional Answer

The **`-exec`** option allows you to execute another command on every file matched by `find`.

It is useful for automating operations such as:

- Listing file details
- Changing permissions
- Moving files
- Copying files
- Compressing files
- Deleting files

### ✅ Example

```bash
find . -name "*.log" -exec ls -l {} \;
```

This command displays detailed information for every `.log` file found.

---

# Question 19 – How do you delete files using the `find` command?

## ✅ Professional Answer

The **`-delete`** option removes files that match the search criteria.

### ✅ Example

```bash
find . -name "*.tmp" -delete
```

This command deletes all `.tmp` files in the current directory and its subdirectories.

> **Interview Tip:** Always verify the search results before using `-delete` because deleted files cannot be recovered easily.

---

# Question 20 – What is recursive searching in `grep`?

## ✅ Professional Answer

Recursive searching allows `grep` to search inside **all files within a directory and its subdirectories**.

Use the **`-r`** option.

### ✅ Example

```bash
grep -r "ERROR" .
```

This command searches every file in the current directory for the word **ERROR**.

---

# Question 21 – What is the purpose of the `-i` option in `grep`?

## ✅ Professional Answer

The **`-i`** option performs a **case-insensitive search**.

It matches words regardless of uppercase or lowercase letters.

### ✅ Example

```bash
grep -i "linux" notes.txt
```

This command matches:

```text
Linux
LINUX
linux
LiNuX
```

---

# Question 22 – How do you display line numbers in `grep` output?

## ✅ Professional Answer

Use the **`-n`** option.

It displays the line number before each matching line.

### ✅ Example

```bash
grep -n "main" script.sh
```

### Sample Output

```text
15:main()
42:echo "main completed"
```

This is helpful while debugging source code.

---

# Question 23 – How do you count matching lines in a file?

## ✅ Professional Answer

Use the **`-c`** option with `grep`.

Instead of displaying matching lines, it returns the total count.

### ✅ Example

```bash
grep -c "ERROR" app.log
```

### Output

```text
5
```

This indicates that **5 lines** contain the word **ERROR**.

---

# Question 24 – What is the purpose of the `-v` option in `grep`?

## ✅ Professional Answer

The **`-v`** option displays **non-matching lines**.

It is useful for excluding unwanted entries from the output.

### ✅ Example

```bash
grep -v "^#" config.conf
```

This command displays only active configuration lines by ignoring comments.

---

# Question 25 – How do you search multiple patterns with `grep`?

## ✅ Professional Answer

Use **`grep -E`** with the pipe (`|`) operator.

### ✅ Example

```bash
grep -E "ERROR|WARNING" app.log
```

This command displays lines containing either **ERROR** or **WARNING**.

---

# Question 26 – What are Regular Expressions (Regex)?

## ✅ Professional Answer

Regular Expressions (Regex) are search patterns used to match text efficiently.

They allow flexible searching for:

- Numbers
- Dates
- Email addresses
- Words
- Character patterns

### ✅ Example

Search lines beginning with "Error":

```bash
grep "^Error" app.log
```

Search lines ending with ".conf":

```bash
grep ".conf$" files.txt
```

---

# Question 27 – What is the difference between `find` and `locate`?

## ✅ Professional Answer

Both commands search for files, but they work differently.

- **`find`** searches the live filesystem.
- **`locate`** searches a prebuilt database.

Because of this, `locate` is faster, while `find` always returns the most up-to-date results.

### ✅ Example

```bash
find . -name "notes.txt"
```

```bash
locate notes.txt
```

---

# Question 28 – What is the difference between `grep`, `egrep`, and `fgrep`?

## ✅ Professional Answer

These commands are used for text searching.

- **`grep`** → Standard search.
- **`grep -E`** → Extended regular expressions (replaces `egrep`).
- **`grep -F`** → Fixed string search (replaces `fgrep`).

Modern Linux systems recommend using **`grep -E`** and **`grep -F`** instead of the older `egrep` and `fgrep` commands.

### ✅ Example

```bash
grep -E "error|warning" app.log
```

```bash
grep -F "Linux" notes.txt
```

---

# Question 29 – What are some real-world uses of `find` and `grep`?

## ✅ Professional Answer

These commands are used daily by Linux administrators and DevOps engineers.

Common use cases include:

- Searching configuration files.
- Finding log files.
- Troubleshooting applications.
- Monitoring servers.
- Auditing user files.
- Finding large files.
- Locating recently modified files.
- Searching source code.
- Security investigations.
- Automation scripts.

### ✅ Example

Find SSH configuration:

```bash
find /etc -name "sshd_config"
```

Search the SSH port configuration:

```bash
grep "^Port" /etc/ssh/sshd_config
```

---

# Question 30 – Why are `find` and `grep` important in DevOps and Linux Administration?

## ✅ Professional Answer

`find` and `grep` are among the most frequently used Linux commands because they allow administrators and engineers to quickly locate files and search file contents.

These commands are essential for:

- Log analysis
- Configuration management
- Automation
- Troubleshooting
- Security auditing
- CI/CD pipelines
- Server maintenance
- Cloud infrastructure management

Strong knowledge of these commands is expected in Linux, DevOps, AWS, and System Administration interviews.

---

# 📊 `find` vs `grep` Comparison Table

| Feature | `find` | `grep` |
|----------|---------|---------|
| Purpose | Search files and directories | Search text inside files |
| Searches | Filesystem | File contents |
| Output | File paths | Matching lines |
| Recursive Search | Yes (default) | Yes (`-r`) |
| Search Criteria | Name, owner, size, permissions, time | Text patterns and regular expressions |
| Common Use | Locate files | Analyze logs and configuration files |

---

# 📊 `find` vs `locate` Comparison Table

| Feature | `find` | `locate` |
|----------|---------|----------|
| Search Method | Live filesystem | Database |
| Speed | Slower | Faster |
| Accuracy | Always current | Depends on updated database |
| Requires Database | No | Yes |
| Search Criteria | Multiple attributes | Filename only |
| Best For | Advanced searches | Quick filename lookup |

---

# 📊 `grep` vs `egrep` vs `fgrep` Comparison Table

| Command | Purpose | Modern Equivalent |
|----------|----------|------------------|
| `grep` | Standard text search | `grep` |
| `egrep` | Extended regular expressions | `grep -E` |
| `fgrep` | Fixed string search | `grep -F` |

> **Note:** On modern Linux distributions, `egrep` and `fgrep` are considered deprecated. Use `grep -E` and `grep -F` instead.

---

# 📋 File Searching Cheat Sheet

| Command | Description |
|----------|-------------|
| `find . -name "file.txt"` | Find a file by name |
| `find . -type d` | Find directories |
| `find . -type f` | Find files only |
| `find . -name "*.txt"` | Find files by extension |
| `find . -size +100M` | Find files larger than 100 MB |
| `find . -mtime -7` | Find recently modified files |
| `find . -user username` | Find files by owner |
| `find . -perm 644` | Find files by permission |
| `find . -exec command {} \;` | Execute a command on matched files |
| `find . -delete` | Delete matched files |
| `grep "text" file` | Search text in a file |
| `grep -i "text" file` | Case-insensitive search |
| `grep -r "text" dir` | Recursive search |
| `grep -n "text" file` | Show line numbers |
| `grep -c "text" file` | Count matching lines |
| `grep -v "text" file` | Show non-matching lines |
| `grep -E "A\|B" file` | Search multiple patterns |
| `grep -F "text" file` | Fixed string search |

---

# 📝 Summary

- **`find`** searches for files and directories using attributes such as name, type, owner, permissions, size, and timestamps.
- **`grep`** searches for text or patterns inside files and supports regular expressions.
- `find` is best for locating filesystem objects, while `grep` is best for searching file contents.
- `find` searches the live filesystem, whereas `locate` searches a prebuilt database.
- Use `grep -E` instead of `egrep` and `grep -F` instead of `fgrep` on modern Linux systems.
- These commands are fundamental tools for Linux Administration, DevOps, Cloud Computing, AWS, and System Administration.

---

# ⚡ Quick Revision Notes

Remember these frequently used commands:

```bash
find . -name "file.txt"
```

```bash
find . -name "*.txt"
```

```bash
find . -type d
```

```bash
find . -size +100M
```

```bash
find . -mtime -7
```

```bash
find . -user username
```

```bash
find . -perm 644
```

```bash
grep "text" file
```

```bash
grep -i "text" file
```

```bash
grep -r "text" .
```

```bash
grep -n "text" file
```

```bash
grep -c "text" file
```

```bash
grep -v "^#" config.conf
```

```bash
grep -E "ERROR|WARNING" app.log
```

---

# 💼 Interview Tips

- Clearly explain the difference between **searching files** (`find`) and **searching text** (`grep`).
- Mention that **`find` searches the live filesystem**, while **`locate` uses a database**.
- Know commonly used `find` options such as `-name`, `-type`, `-size`, `-user`, `-perm`, `-mtime`, and `-exec`.
- Be comfortable with `grep` options like `-i`, `-r`, `-n`, `-c`, `-v`, `-E`, and `-F`.
- Demonstrate how `find` and `grep` can be combined in real-world scenarios, such as locating log files with `find` and searching for errors inside them with `grep`.
- Practice these commands regularly on Ubuntu, CentOS, and WSL to build confidence for technical interviews.
