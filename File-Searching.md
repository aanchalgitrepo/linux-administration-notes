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
