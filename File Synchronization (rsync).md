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

---

# 💻 Part 12.2A – Practical Examples (Examples 1–10)

This section contains **beginner-friendly `rsync` practical examples**. These examples are suitable for **GitHub portfolios**, **Linux Administration**, **DevOps**, **AWS**, **Cloud Computing**, and **System Administration** interviews.

> ## 📌 Prerequisites
>
> Create sample directories for practice.
>
> ```bash
> mkdir -p ~/rsync-demo/source
> mkdir -p ~/rsync-demo/destination
>
> echo "Linux Notes" > ~/rsync-demo/source/notes.txt
> echo "DevOps Guide" > ~/rsync-demo/source/devops.txt
> echo "Shell Script" > ~/rsync-demo/source/script.sh
> ```
>
> Verify:
>
> ```bash
> tree ~/rsync-demo
> ```
>
> If `tree` is not installed:
>
> ```bash
> ls -R ~/rsync-demo
> ```

---

# Example 1 – Synchronize One Directory to Another

## ✅ Practical Example

Synchronize all files from the **source** directory to the **destination** directory.

### ✅ Command

```bash
rsync -av ~/rsync-demo/source/ ~/rsync-demo/destination/
```

### ✅ Command Explanation

| Option | Description |
|---------|-------------|
| `-a` | Archive mode (preserves permissions, ownership, timestamps, symbolic links, etc.) |
| `-v` | Verbose output |

### ✅ Expected Output

```text
sending incremental file list

notes.txt
devops.txt
script.sh

sent ...
received ...
```

### ✅ Real-World Use Case

Synchronize project folders before deployment.

### ✅ Screenshot Command

```bash
rsync -av ~/rsync-demo/source/ ~/rsync-demo/destination/

tree ~/rsync-demo
```

### ✅ Ubuntu

Works without additional configuration.

### ✅ CentOS

Fully supported.

### ✅ WSL Note

Works exactly like Ubuntu.

---

# Example 2 – Copy Files Using `rsync`

## ✅ Practical Example

Copy a single file using `rsync`.

### ✅ Command

```bash
rsync -av ~/rsync-demo/source/notes.txt ~/rsync-demo/destination/
```

### ✅ Command Explanation

Copies only the specified file while preserving its metadata.

### ✅ Expected Output

```text
notes.txt
```

### ✅ Real-World Use Case

Copy configuration files between directories.

### ✅ Screenshot Command

```bash
rsync -av ~/rsync-demo/source/notes.txt ~/rsync-demo/destination/

ls ~/rsync-demo/destination
```

### ✅ Ubuntu

Supported.

### ✅ CentOS

Supported.

### ✅ WSL Note

Works normally.

---

# Example 3 – Synchronize Recursively

## ✅ Practical Example

Synchronize directories and all their subdirectories.

### ✅ Command

```bash
mkdir ~/rsync-demo/source/docs

echo "README" > ~/rsync-demo/source/docs/readme.md

rsync -avr ~/rsync-demo/source/ ~/rsync-demo/destination/
```

### ✅ Command Explanation

| Option | Description |
|---------|-------------|
| `-r` | Recursive synchronization |
| `-a` | Archive mode |
| `-v` | Verbose output |

### ✅ Expected Output

```text
docs/
docs/readme.md
```

### ✅ Real-World Use Case

Synchronize complete project directories.

### ✅ Screenshot Command

```bash
rsync -avr ~/rsync-demo/source/ ~/rsync-demo/destination/

tree ~/rsync-demo/destination
```

### ✅ Ubuntu

Supported.

### ✅ CentOS

Supported.

### ✅ WSL Note

Fully supported.

---

# Example 4 – Preserve Permissions and Timestamps

## ✅ Practical Example

Synchronize while preserving file metadata.

### ✅ Command

```bash
rsync -a ~/rsync-demo/source/ ~/rsync-demo/destination/
```

### ✅ Command Explanation

Archive mode preserves:

- Permissions
- Ownership
- Timestamps
- Symbolic links

### ✅ Expected Output

Files appear identical in both directories.

### ✅ Real-World Use Case

Server backup and migration.

### ✅ Screenshot Command

```bash
rsync -a ~/rsync-demo/source/ ~/rsync-demo/destination/

ls -l ~/rsync-demo/destination
```

### ✅ Ubuntu

Supported.

### ✅ CentOS

Supported.

### ✅ WSL Note

Works normally.

---

# Example 5 – Show Verbose Output

## ✅ Practical Example

Display detailed synchronization information.

### ✅ Command

```bash
rsync -av ~/rsync-demo/source/ ~/rsync-demo/destination/
```

### ✅ Command Explanation

Verbose mode shows every processed file.

### ✅ Expected Output

```text
notes.txt
devops.txt
script.sh
```

### ✅ Real-World Use Case

Monitor synchronization during troubleshooting.

### ✅ Screenshot Command

```bash
rsync -av ~/rsync-demo/source/ ~/rsync-demo/destination/
```

### ✅ Ubuntu

Supported.

### ✅ CentOS

Supported.

### ✅ WSL Note

No differences.

---

# Example 6 – Dry Run Before Synchronization

## ✅ Practical Example

Preview changes without copying files.

### ✅ Command

```bash
echo "New File" > ~/rsync-demo/source/new.txt

rsync -av --dry-run ~/rsync-demo/source/ ~/rsync-demo/destination/
```

### ✅ Command Explanation

`--dry-run` shows what would happen without making changes.

### ✅ Expected Output

```text
new.txt
```

### ✅ Real-World Use Case

Verify synchronization before production deployment.

### ✅ Screenshot Command

```bash
rsync -av --dry-run ~/rsync-demo/source/ ~/rsync-demo/destination/
```

### ✅ Ubuntu

Supported.

### ✅ CentOS

Supported.

### ✅ WSL Note

Recommended before large synchronization jobs.

---

# Example 7 – Delete Extra Files in Destination

## ✅ Practical Example

Remove files from the destination that no longer exist in the source.

### ✅ Command

```bash
rsync -av --delete ~/rsync-demo/source/ ~/rsync-demo/destination/
```

### ✅ Command Explanation

`--delete` keeps the destination identical to the source.

### ✅ Expected Output

Extra files are removed from the destination.

### ✅ Real-World Use Case

Mirror production and backup directories.

### ✅ Screenshot Command

```bash
rsync -av --delete ~/rsync-demo/source/ ~/rsync-demo/destination/

tree ~/rsync-demo/destination
```

### ✅ Ubuntu

Supported.

### ✅ CentOS

Supported.

### ✅ WSL Note

⚠️ Use carefully, as deleted files cannot be recovered.

---

# Example 8 – Synchronize Only Updated Files

## ✅ Practical Example

Transfer only files that have changed.

### ✅ Command

```bash
echo "Updated Content" >> ~/rsync-demo/source/notes.txt

rsync -av ~/rsync-demo/source/ ~/rsync-demo/destination/
```

### ✅ Command Explanation

`rsync` compares source and destination and copies only modified files.

### ✅ Expected Output

```text
notes.txt
```

Only the updated file is transferred.

### ✅ Real-World Use Case

Daily incremental backups.

### ✅ Screenshot Command

```bash
rsync -av ~/rsync-demo/source/ ~/rsync-demo/destination/
```

### ✅ Ubuntu

Supported.

### ✅ CentOS

Supported.

### ✅ WSL Note

Fully supported.

---

# Example 9 – Display Progress During Transfer

## ✅ Practical Example

Monitor synchronization progress.

### ✅ Command

```bash
rsync -av --progress ~/rsync-demo/source/ ~/rsync-demo/destination/
```

### ✅ Command Explanation

`--progress` displays transfer speed, percentage completed, and remaining data.

### ✅ Expected Output

```text
notes.txt
      100% ...
```

### ✅ Real-World Use Case

Monitor large backup or migration operations.

### ✅ Screenshot Command

```bash
rsync -av --progress ~/rsync-demo/source/ ~/rsync-demo/destination/
```

### ✅ Ubuntu

Supported.

### ✅ CentOS

Supported.

### ✅ WSL Note

Works normally.

---

# Example 10 – Verify Synchronized Files

## ✅ Practical Example

Verify that both directories contain identical files.

### ✅ Command

```bash
diff -r ~/rsync-demo/source ~/rsync-demo/destination
```

### ✅ Command Explanation

`diff -r` recursively compares two directories.

### ✅ Expected Output

If both directories are identical:

```text
(no output)
```

### ✅ Real-World Use Case

Verify backups after synchronization.

### ✅ Screenshot Command

```bash
diff -r ~/rsync-demo/source ~/rsync-demo/destination
```

### ✅ Ubuntu

Supported.

### ✅ CentOS

Supported.

### ✅ WSL Note

Works exactly like Ubuntu.

---

# 📌 Key Takeaways

- `rsync -av` → Synchronize files while preserving metadata.
- `rsync --dry-run` → Preview changes safely.
- `rsync --delete` → Keep destination identical to source.
- `rsync --progress` → Display transfer progress.
- `diff -r` → Verify synchronized directories.
- `rsync` transfers **only changed files**, making it significantly faster than repeatedly using `cp`.

---

# 🚀 Part 12.2B – Advanced Practical Examples (Examples 11–20)

This section covers **advanced `rsync` examples** commonly used in **Linux Administration, DevOps, AWS, Cloud Computing, System Administration, and Production Linux Servers**.

> **Prerequisites**
>
> ```bash
> mkdir -p ~/rsync-demo/source
> mkdir -p ~/rsync-demo/destination
>
> echo "Linux Notes" > ~/rsync-demo/source/notes.txt
> echo "DevOps Guide" > ~/rsync-demo/source/devops.txt
> echo "Shell Script" > ~/rsync-demo/source/script.sh
> ```
>
> Verify:
>
> ```bash
> tree ~/rsync-demo
> ```
>
> or
>
> ```bash
> ls -R ~/rsync-demo
> ```

---

# Example 11 – Synchronize Over SSH

## ✅ Practical Example

Synchronize files securely to a remote Linux server using SSH.

### ✅ Command

```bash
rsync -avz ~/rsync-demo/source/ user@192.168.1.100:/home/user/backup/
```

### ✅ Command Explanation

| Option | Description |
|---------|-------------|
| `-a` | Archive mode |
| `-v` | Verbose output |
| `-z` | Compress data during transfer |

### ✅ Expected Output

```text
sending incremental file list

notes.txt
script.sh
```

### ✅ Real-World Use Case

- AWS EC2 backup
- Production server deployment
- Remote configuration backup

### ✅ Screenshot Command

```bash
rsync -avz ~/rsync-demo/source/ user@192.168.1.100:/home/user/backup/
```

---

# Example 12 – Synchronize Using a Custom SSH Port

## ✅ Practical Example

Use a non-default SSH port.

### ✅ Command

```bash
rsync -avz -e "ssh -p 2222" ~/rsync-demo/source/ user@192.168.1.100:/backup/
```

### ✅ Command Explanation

`-e` specifies the remote shell.

Here SSH connects using port **2222**.

### ✅ Expected Output

```text
sending incremental file list
```

### ✅ Real-World Use Case

Many production servers disable port **22** for security.

### ✅ Screenshot Command

```bash
rsync -avz -e "ssh -p 2222" ~/rsync-demo/source/ user@192.168.1.100:/backup/
```

---

# Example 13 – Exclude Files from Synchronization

## ✅ Practical Example

Exclude log files while synchronizing.

### ✅ Command

```bash
rsync -av --exclude="*.log" ~/rsync-demo/source/ ~/rsync-demo/destination/
```

### ✅ Command Explanation

`--exclude` ignores matching files.

### ✅ Expected Output

```text
notes.txt
script.sh
```

`error.log` is skipped.

### ✅ Real-World Use Case

Ignore:

- Log files
- Cache files
- Temporary files

### ✅ Screenshot Command

```bash
touch ~/rsync-demo/source/error.log

rsync -av --exclude="*.log" ~/rsync-demo/source/ ~/rsync-demo/destination/
```

---

# Example 14 – Include Specific Files Only

## ✅ Practical Example

Synchronize only `.txt` files.

### ✅ Command

```bash
rsync -av \
--include="*.txt" \
--exclude="*" \
~/rsync-demo/source/ \
~/rsync-demo/destination/
```

### ✅ Command Explanation

Only text files are copied.

Everything else is ignored.

### ✅ Expected Output

```text
notes.txt
devops.txt
```

### ✅ Real-World Use Case

Synchronize only configuration or documentation files.

### ✅ Screenshot Command

```bash
rsync -av \
--include="*.txt" \
--exclude="*" \
~/rsync-demo/source/ \
~/rsync-demo/destination/
```

---

# Example 15 – Synchronize Multiple Directories

## ✅ Practical Example

Synchronize multiple folders into one destination.

### ✅ Command

```bash
mkdir ~/rsync-demo/config
mkdir ~/rsync-demo/logs

rsync -av ~/rsync-demo/source ~/rsync-demo/config ~/rsync-demo/logs ~/rsync-demo/destination/
```

### ✅ Command Explanation

Multiple directories can be synchronized in a single command.

### ✅ Expected Output

```text
source/
config/
logs/
```

### ✅ Real-World Use Case

Backup multiple application directories.

### ✅ Screenshot Command

```bash
rsync -av ~/rsync-demo/source ~/rsync-demo/config ~/rsync-demo/logs ~/rsync-demo/destination/
```

---

# Example 16 – Limit Transfer Bandwidth

## ✅ Practical Example

Restrict network usage during synchronization.

### ✅ Command

```bash
rsync -av --bwlimit=500 ~/rsync-demo/source/ ~/rsync-demo/destination/
```

### ✅ Command Explanation

`--bwlimit=500`

Limits bandwidth to approximately **500 KB/s**.

### ✅ Expected Output

Synchronization occurs at a limited speed.

### ✅ Real-World Use Case

Prevent backup jobs from consuming all available bandwidth.

### ✅ Screenshot Command

```bash
rsync -av --bwlimit=500 ~/rsync-demo/source/ ~/rsync-demo/destination/
```

---

# Example 17 – Backup Changed Files

## ✅ Practical Example

Store modified files in a backup directory before replacing them.

### ✅ Command

```bash
mkdir ~/rsync-demo/backup

rsync -av --backup --backup-dir=~/rsync-demo/backup \
~/rsync-demo/source/ \
~/rsync-demo/destination/
```

### ✅ Command Explanation

Modified destination files are saved in the backup directory.

### ✅ Expected Output

```text
backup/
```

contains previous versions.

### ✅ Real-World Use Case

Configuration backups before deployment.

### ✅ Screenshot Command

```bash
rsync -av --backup --backup-dir=~/rsync-demo/backup \
~/rsync-demo/source/ \
~/rsync-demo/destination/
```

---

# Example 18 – Synchronize Hidden Files

## ✅ Practical Example

Synchronize hidden files such as `.env` and `.gitignore`.

### ✅ Command

```bash
echo "SECRET" > ~/rsync-demo/source/.env

rsync -av ~/rsync-demo/source/ ~/rsync-demo/destination/
```

### ✅ Command Explanation

`rsync` copies hidden files automatically.

### ✅ Expected Output

```text
.env
```

### ✅ Real-World Use Case

Synchronize application configuration files.

### ✅ Screenshot Command

```bash
ls -la ~/rsync-demo/source

rsync -av ~/rsync-demo/source/ ~/rsync-demo/destination/
```

---

# Example 19 – Mirror Source to Destination

## ✅ Practical Example

Make the destination an exact copy of the source.

### ✅ Command

```bash
rsync -av --delete ~/rsync-demo/source/ ~/rsync-demo/destination/
```

### ✅ Command Explanation

`--delete`

Removes extra files from the destination.

### ✅ Expected Output

Source and destination become identical.

### ✅ Real-World Use Case

Website deployment.

Production backup.

Disaster recovery.

### ✅ Screenshot Command

```bash
rsync -av --delete ~/rsync-demo/source/ ~/rsync-demo/destination/

diff -r ~/rsync-demo/source ~/rsync-demo/destination
```

---

# Example 20 – Automate Synchronization Using Cron

## ✅ Practical Example

Run synchronization automatically every day at **2:00 AM**.

### ✅ Command

Edit the user's crontab:

```bash
crontab -e
```

Add the following entry:

```cron
0 2 * * * rsync -av --delete /home/$USER/rsync-demo/source/ /home/$USER/rsync-demo/destination/
```

### ✅ Command Explanation

| Field | Meaning |
|--------|---------|
| `0` | Minute |
| `2` | Hour (2 AM) |
| `*` | Every day of the month |
| `*` | Every month |
| `*` | Every day of the week |

### ✅ Expected Output

The synchronization runs automatically every day at **2:00 AM**.

### ✅ Real-World Use Case

- Nightly backups
- Website synchronization
- Configuration backups
- DevOps automation
- Disaster recovery

### ✅ Screenshot Command

```bash
crontab -l
```

---

# 📌 Key Takeaways

- `rsync -avz` → Synchronize securely over SSH.
- `-e "ssh -p PORT"` → Use a custom SSH port.
- `--exclude` → Skip unwanted files.
- `--include` → Synchronize only selected files.
- `--bwlimit` → Control bandwidth usage.
- `--backup` → Preserve previous file versions.
- Hidden files (e.g., `.env`) are synchronized automatically.
- `--delete` → Mirror the source to the destination.
- Cron can automate `rsync` for scheduled backups.

---

# 💡 Interview Tip

The most commonly used `rsync` commands in production environments are:

```bash
rsync -av source/ destination/
rsync -avz source/ user@server:/backup/
rsync -av --delete source/ destination/
rsync -av --progress source/ destination/
rsync -av --dry-run source/ destination/
rsync -av --exclude="*.log" source/ destination/
```

These commands are frequently used for:

- Linux server backups
- AWS EC2 synchronization
- Website deployments
- Docker volume backups
- Configuration management
- CI/CD pipelines
- Disaster recovery
- Automated backups with Cron

---
