# 📂 Part 12.1 – Introduction

## 📖 Definition

### What is File Synchronization?

**File Synchronization** is the process of keeping two or more files or directories **identical** by copying only the new or modified files from the source to the destination.

Unlike a normal copy operation, synchronization updates only the differences between the source and destination, making it much faster and more efficient.

It is widely used for:

- Backup automation
- Server replication
- Website deployment
- Disaster recovery
- Cloud storage synchronization
- DevOps automation

### Example

```
Source Directory
│
├── notes.txt
├── report.pdf
└── script.sh

        │
        ▼

Destination Directory
│
├── notes.txt
├── report.pdf
└── script.sh
```

After synchronization, both directories contain the same files.

---

# 🔄 What is `rsync`?

`rsync` (**Remote Sync**) is a powerful Linux command-line utility used to synchronize files and directories efficiently between:

- Local directories
- Local and remote systems
- Remote servers

Unlike the `cp` command, `rsync` transfers **only changed data**, making synchronization much faster and reducing network bandwidth usage.

It supports:

- Incremental file transfer
- Compression
- Permission preservation
- Ownership preservation
- Timestamp preservation
- Symbolic links
- SSH-based secure transfers

---

# 🎯 Why `rsync` is Used

`rsync` is one of the most commonly used Linux utilities because it is fast, reliable, and efficient.

Common use cases include:

- Daily server backups
- Website deployment
- Synchronizing project files
- Copying home directories
- Migrating servers
- Docker volume backup
- Configuration backup
- Cloud server synchronization
- Disaster recovery
- CI/CD deployment

---

# 📊 Difference Between `cp`, `scp`, and `rsync`

| Feature | `cp` | `scp` | `rsync` |
|---------|------|--------|----------|
| Local Copy | ✅ | ❌ | ✅ |
| Remote Copy | ❌ | ✅ | ✅ |
| Incremental Transfer | ❌ | ❌ | ✅ |
| Compression | ❌ | ❌ | ✅ |
| SSH Support | ❌ | ✅ | ✅ |
| Resume Interrupted Transfer | ❌ | ❌ | ✅ |
| Preserve Permissions | Limited | Yes | Yes |
| Delete Extra Files | ❌ | ❌ | ✅ |
| Best For | Simple copy | Secure remote copy | Synchronization & backup |

### Summary

**cp**

- Copies files locally.
- Always copies the complete file.

**scp**

- Securely copies files over SSH.
- Transfers the entire file every time.

**rsync**

- Synchronizes files efficiently.
- Transfers only changed data.
- Ideal for backups and deployments.

---

# ⭐ Features of `rsync`

Some important features include:

- Fast incremental synchronization
- Copies only modified files
- Preserves permissions
- Preserves ownership
- Preserves timestamps
- Preserves symbolic links
- Compresses data during transfer
- Works over SSH
- Supports bandwidth limiting
- Supports deletion of removed files
- Supports dry-run mode
- Supports progress display
- Efficient for large datasets

---

# 📝 `rsync` Syntax

## Basic Syntax

```bash
rsync [OPTIONS] SOURCE DESTINATION
```

### Example

```bash
rsync -av source/ destination/
```

---

### Remote Synchronization

```bash
rsync -av source/ user@server:/backup/
```

---

### Download from Remote Server

```bash
rsync -av user@server:/backup/ local-folder/
```

---

# ⚙️ Common `rsync` Options

| Option | Description |
|---------|-------------|
| `-a` | Archive mode (preserves permissions, ownership, timestamps, symbolic links, etc.) |
| `-v` | Verbose output |
| `-z` | Compress data during transfer |
| `-h` | Human-readable output |
| `-r` | Recursive copy |
| `-P` | Show progress and resume interrupted transfers |
| `--progress` | Display transfer progress |
| `--delete` | Delete extra files in destination |
| `--dry-run` | Preview changes without copying |
| `--exclude` | Exclude files/directories |
| `--include` | Include specific files |
| `-e ssh` | Use SSH as transport |
| `--bwlimit` | Limit transfer speed |

---

# 🏠 Local vs Remote Synchronization

## Local Synchronization

Synchronizes directories on the same machine.

```bash
rsync -av source/ backup/
```

### Example

```
Documents
     │
     ▼
Backup
```

---

## Remote Synchronization

Synchronizes files between two Linux systems using SSH.

```bash
rsync -av project/ user@192.168.1.10:/home/user/project/
```

---

## Download from Remote

```bash
rsync -av user@192.168.1.10:/backup/ local-backup/
```

---

# ⚙️ `rsync` Working Process

```
Source Directory
        │
        ▼
Compare Files
        │
        ▼
Find Differences
        │
        ▼
Transfer Only Changed Data
        │
        ▼
Destination Directory Updated
```

### Explanation

Instead of copying every file, `rsync`:

1. Compares source and destination.
2. Detects changed files.
3. Transfers only the differences.
4. Leaves unchanged files untouched.

This makes synchronization much faster than using `cp` or `scp`.

---

# 📄 Understanding `rsync` Output

## Example

```bash
rsync -av project/ backup/
```

### Sample Output

```text
sending incremental file list

notes.txt
script.sh

sent 1,254 bytes
received 42 bytes

total size is 2,580
speedup is 2.10
```

---

### Output Explanation

| Output | Meaning |
|---------|----------|
| sending incremental file list | rsync is comparing files |
| notes.txt | File transferred |
| script.sh | File transferred |
| sent | Data sent |
| received | Data received |
| total size | Total size of synchronized files |
| speedup | Efficiency compared to copying everything |

---

# 🐧 Ubuntu / CentOS / WSL Notes

## Ubuntu

- `rsync` is **usually pre-installed** on modern Ubuntu systems.
- If it is missing, install it using:

```bash
sudo apt update
sudo apt install rsync
```

---

## CentOS / RHEL

Install `rsync` using:

```bash
sudo yum install rsync
```

or (CentOS Stream/RHEL 8+)

```bash
sudo dnf install rsync
```

---

## Amazon Linux

Install using:

```bash
sudo yum install rsync
```

---

## WSL Ubuntu

`rsync` works exactly like a normal Ubuntu installation.

If it is not installed:

```bash
sudo apt update
sudo apt install rsync
```

It supports:

- Local synchronization
- Backup practice
- Directory synchronization
- Permission preservation

Remote synchronization over SSH also works if an SSH server is available.

---

# 📌 Key Points

- **File Synchronization** keeps two locations identical.
- **`rsync`** is the most popular Linux synchronization utility.
- It transfers **only changed data**, making it fast and bandwidth-efficient.
- It supports local and remote synchronization.
- It works securely over SSH.
- It is widely used in **Linux Administration**, **DevOps**, **AWS**, **Cloud Computing**, **System Administration**, and **Technical Support**.
- Learning `rsync` is essential for backups, deployments, disaster recovery, and automation.
