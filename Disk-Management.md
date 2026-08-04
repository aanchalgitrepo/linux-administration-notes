# Part 9.1 – Introduction

Disk Management is one of the most important Linux Administration topics. Every Linux administrator, DevOps Engineer, Cloud Engineer, and System Administrator should know how Linux stores data, manages disks, creates filesystems, mounts storage devices, and monitors disk usage.

This chapter covers everything from the basics of disks and partitions to practical commands used in production environments.

---

# ✅ Definition

## What is Disk Management?

**Disk Management** is the process of organizing, monitoring, configuring, and maintaining storage devices in a Linux system.

It includes tasks such as:

- Creating partitions
- Formatting disks
- Creating filesystems
- Mounting storage devices
- Monitoring disk usage
- Managing swap space
- Checking filesystem health
- Preventing storage-related failures

Disk Management ensures that data is stored safely and efficiently while keeping the operating system running smoothly.

---

## Why is Disk Management Important?

Proper disk management is important because it helps:

- Store data efficiently
- Improve system performance
- Prevent disk full errors
- Organize storage logically
- Protect important data
- Increase server reliability
- Reduce downtime
- Support backup and disaster recovery

Without proper disk management, applications may stop working due to insufficient storage space.

---

## Types of Storage Devices

Linux supports many different storage devices.

| Storage Device | Description | Common Usage |
|---------------|-------------|--------------|
| HDD | Hard Disk Drive | Traditional storage |
| SSD | Solid State Drive | Fast operating system storage |
| NVMe SSD | High-speed SSD using PCIe | Cloud servers, databases |
| USB Drive | Portable storage | Backup and file transfer |
| External HDD | External hard drive | Backup storage |
| SD Card | Flash memory | Embedded systems |
| Network Storage (NAS/SAN) | Storage over network | Enterprise storage |

---

## HDD vs SSD vs NVMe

| Feature | HDD | SSD | NVMe SSD |
|---------|-----|-----|----------|
| Technology | Magnetic Disk | Flash Memory | PCIe Flash Memory |
| Speed | Slow | Fast | Extremely Fast |
| Moving Parts | Yes | No | No |
| Noise | Yes | Silent | Silent |
| Power Consumption | High | Low | Low |
| Price | Cheapest | Moderate | Highest |
| Boot Time | Slow | Fast | Very Fast |
| Best Use Case | Large storage | Desktop/Laptop | Cloud & Database Servers |

---

## What is a Filesystem?

A **Filesystem** is the method Linux uses to organize and store data on a storage device.

Without a filesystem, Linux cannot read or write files.

Common Linux filesystems include:

- ext4
- XFS
- Btrfs
- FAT32
- exFAT
- NTFS

Example:

```bash
mkfs.ext4 /dev/sdb1
```

This command creates an **ext4 filesystem** on the partition.

---

## What is a Partition?

A **Partition** is a logical section of a physical disk.

One hard disk can contain multiple partitions.

Example:

```text
Disk
│
├── sda1
├── sda2
└── sda3
```

Each partition can have its own filesystem.

Example:

```text
/dev/sda1
/dev/sda2
/dev/sdb1
```

---

## What is a Mount Point?

A **Mount Point** is a directory where a filesystem becomes accessible.

Linux does not automatically use a partition until it is mounted.

Example:

```bash
sudo mount /dev/sdb1 /mnt/data
```

Now everything inside `/dev/sdb1` becomes available through:

```text
/mnt/data
```

---

## What is Swap Space?

**Swap Space** is disk space used as virtual memory when RAM becomes full.

Linux moves inactive memory pages from RAM to swap.

Example:

```bash
free -h
```

Example Output:

```text
Swap: 2.0G
```

---

## What is Disk Usage?

Disk Usage refers to the amount of storage currently being used and the amount still available.

Common commands:

```bash
df -h
```

```bash
du -sh /home
```

These help administrators monitor available storage.

---

# ✅ Why Disk Management is Used

Disk management is used in almost every Linux server.

## Storage Management

Organize storage devices efficiently.

Example:

Separate disks for:

- Operating System
- Database
- Logs
- Backup

---

## Capacity Planning

Administrators monitor available storage before disks become full.

Example:

```bash
df -h
```

---

## Performance Optimization

Fast storage devices like SSD and NVMe improve:

- Boot speed
- Database performance
- Application response time

---

## Backup Planning

Separate backup storage protects important data.

Example:

```text
/backup
```

---

## Server Administration

Administrators regularly:

- Check disk usage
- Mount new disks
- Remove unused storage
- Verify filesystem health

---

## Cloud Instance Storage Management

Cloud providers such as AWS, Azure, and GCP allow administrators to:

- Attach new volumes
- Resize disks
- Mount additional storage

AWS Example:

```text
EC2 + EBS Volume
```

---

## Database Storage

Databases often use dedicated storage for better performance.

Examples:

- MySQL
- PostgreSQL
- MongoDB

---

## Log Storage

Logs can grow very large.

Administrators monitor:

```text
/var/log
```

to prevent disks from filling up.

---

## Preventing Disk Full Errors

Regular monitoring helps prevent application failures.

Useful commands:

```bash
df -h
```

```bash
du -sh *
```

---

# ✅ Linux Storage Architecture

```text
Physical Disk
      │
      ▼
Partition
      │
      ▼
Filesystem
      │
      ▼
Mount Point
      │
      ▼
Users / Applications
```

### Explanation

### Physical Disk

Actual hardware such as:

- HDD
- SSD
- NVMe

↓

### Partition

Logical division of the disk.

↓

### Filesystem

Organizes files.

↓

### Mount Point

Makes storage accessible.

↓

### Users / Applications

Applications read and write data.

---

# ✅ Common Disk Management Commands

| Command | Purpose |
|----------|---------|
| `lsblk` | List block devices |
| `df` | Show filesystem disk usage |
| `df -h` | Human-readable disk usage |
| `du` | Display directory or file size |
| `du -sh` | Show total directory size |
| `fdisk` | Manage partitions |
| `parted` | Advanced partition management |
| `blkid` | Display filesystem UUID |
| `mount` | Mount filesystem |
| `umount` | Unmount filesystem |
| `findmnt` | Display mounted filesystems |
| `fsck` | Check filesystem consistency |
| `mkfs` | Create filesystem |
| `swapon` | Enable swap |
| `swapoff` | Disable swap |
| `free -h` | Display RAM and swap usage |

---

# ✅ Disk Management in Different Linux Distributions

| Distribution | Package / Tool | Notes |
|--------------|---------------|-------|
| Ubuntu | util-linux | Default utilities available |
| Debian | util-linux | Similar to Ubuntu |
| CentOS 7/8/9 | util-linux | Enterprise Linux |
| RHEL | util-linux | Production environments |
| Amazon Linux | util-linux | AWS EC2 instances |
| WSL Ubuntu | util-linux (limited) | Physical partitioning is limited |

---

# ✅ WSL Important Note

WSL does **not** behave exactly like a physical Linux installation.

It stores Linux inside a virtual hard disk (`ext4.vhdx`) managed by Windows.

Because of this:

- Some storage commands work normally.
- Some partitioning commands have limited functionality.
- You should **not** repartition your Windows disk from WSL.

---

## Commands That Work Well in WSL

```bash
lsblk
```

```bash
df -h
```

```bash
du -sh .
```

```bash
mount
```

```bash
findmnt
```

---

## Commands with Limited Functionality

```bash
fdisk
```

```bash
parted
```

```bash
mkfs
```

```bash
fsck
```

---

## Why?

WSL uses a **virtual disk (VHDX)** instead of directly managing your physical hard drive.

Therefore, creating or modifying real partitions from WSL is generally not recommended.

For full disk management practice, use:

- Ubuntu Server (VirtualBox / VMware)
- AWS EC2
- Azure Virtual Machine
- Google Cloud VM

---

# ✅ Important Directories

| Directory | Purpose |
|-----------|---------|
| `/` | Root filesystem |
| `/home` | User home directories |
| `/boot` | Bootloader and kernel files |
| `/var` | Logs, caches, and variable data |
| `/tmp` | Temporary files |
| `/mnt` | Temporary mount points |
| `/media` | Auto-mounted removable devices |

---

# ✅ Understanding `df` Output

Example:

```bash
df -h
```

Sample Output:

```text
Filesystem      Size Used Avail Use% Mounted on
/dev/sda1        50G  20G   28G  42% /
```

### Explanation

| Field | Meaning |
|--------|---------|
| Filesystem | Partition or device name |
| Size | Total disk size |
| Used | Space currently used |
| Avail | Free space available |
| Use% | Percentage of storage used |
| Mounted on | Mount point |

---

# ✅ Understanding `du` Output

Example:

```bash
du -sh /home
```

Sample Output:

```text
2.4G    /home
```

### Explanation

| Field | Meaning |
|--------|---------|
| `2.4G` | Total size of the directory |
| `/home` | Directory analyzed |

---

# ✅ Understanding `lsblk` Output

Example:

```bash
lsblk
```

Sample Output:

```text
NAME   MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
sda      8:0    0   50G  0 disk
└─sda1   8:1    0   50G  0 part /
```

### Explanation

| Column | Meaning |
|--------|---------|
| NAME | Device name |
| MAJ:MIN | Major and minor device numbers |
| RM | Removable device (1 = Yes, 0 = No) |
| SIZE | Total capacity |
| RO | Read-only status |
| TYPE | Device type (disk, partition, loop) |
| MOUNTPOINT | Directory where the filesystem is mounted |

---

# ✅ Mount vs Unmount

| Mount | Unmount |
|--------|----------|
| Makes a filesystem accessible | Safely disconnects the filesystem |
| Uses `mount` | Uses `umount` |
| Required before accessing storage | Required before removing storage |
| Connects storage to the directory tree | Detaches storage from the directory tree |

---

# ✅ `df` vs `du`

| `df` | `du` |
|------|------|
| Shows filesystem usage | Shows directory or file usage |
| Disk-level information | Directory-level information |
| Displays total partition usage | Displays usage of a specific directory |
| Useful for checking free space | Useful for finding large folders |

---

# ✅ Filesystem Types

| Filesystem | Description |
|------------|-------------|
| ext4 | Default Linux filesystem |
| XFS | Common in RHEL/CentOS |
| Btrfs | Advanced Linux filesystem with snapshots |
| FAT32 | Compatible with Windows and USB drives |
| exFAT | Supports large files on removable media |
| NTFS | Windows filesystem |
| Swap | Virtual memory area |

---

# ✅ Common Mount Points

| Mount Point | Purpose |
|-------------|---------|
| `/` | Root filesystem |
| `/boot` | Boot partition |
| `/home` | User data |
| `/var` | Logs and application data |
| `/mnt` | Temporary mounts |
| `/media` | USB/CD/DVD auto mounts |
| `swap` | Virtual memory |

---

## 🎯 Interview Tips

- Know the difference between **`df`** and **`du`**.
- Understand what a **filesystem**, **partition**, and **mount point** are.
- Be able to explain why **swap space** is used.
- Mention that **WSL has limitations** for partitioning because it runs on a virtual disk.
- Practice commands like `df -h`, `du -sh`, `lsblk`, `mount`, and `findmnt`, as they are frequently asked in Linux Administration and DevOps interviews.

---

# Part 9.2A – Practical Examples (Examples 1–10)

This section covers the most commonly used **Disk Management** commands used by **Linux Administrators, DevOps Engineers, Cloud Engineers, AWS Engineers, and System Administrators**.

> **Note for WSL Users**
>
> Most commands in this section work in WSL. However, commands related to physical disk partitioning (such as `fdisk`) may show limited information because WSL runs inside a virtual disk (`ext4.vhdx`).

---

# Example 1 – Check Disk Usage

## ✅ Practical Example

Display disk usage for all mounted filesystems.

### ✅ Command

```bash
df -h
```

### ✅ Command Explanation

- `df` → Displays filesystem disk usage.
- `-h` → Shows sizes in a human-readable format (KB, MB, GB).

### ✅ Expected Output

```text
Filesystem      Size Used Avail Use% Mounted on
/dev/sda1        50G  18G   30G  38% /
```

### ✅ Real-World Use Case

System administrators regularly use `df -h` to ensure servers do not run out of disk space.

### ✅ Screenshot Command

```bash
df -h
```

### ✅ Ubuntu

```bash
df -h
```

### ✅ CentOS

```bash
df -h
```

### ✅ WSL Note

Fully supported in WSL.

---

# Example 2 – Check Directory Size

## ✅ Practical Example

Display the total size of a directory.

### ✅ Command

```bash
du -sh /home
```

### ✅ Command Explanation

- `du` → Displays disk usage of files/directories.
- `-s` → Summary only.
- `-h` → Human-readable output.

### ✅ Expected Output

```text
2.4G    /home
```

### ✅ Real-World Use Case

Find which directory is consuming the most disk space.

### ✅ Screenshot Command

```bash
du -sh /home
```

### ✅ Ubuntu

```bash
du -sh /home
```

### ✅ CentOS

```bash
du -sh /home
```

### ✅ WSL Note

Works normally.

---

# Example 3 – List Block Devices

## ✅ Practical Example

Display available storage devices.

### ✅ Command

```bash
lsblk
```

### ✅ Command Explanation

Lists all available block devices including:

- HDD
- SSD
- NVMe
- Partitions

### ✅ Expected Output

```text
NAME   SIZE TYPE MOUNTPOINT
sda     50G disk
└─sda1  50G part /
```

### ✅ Real-World Use Case

Useful when adding a new disk to a Linux server.

### ✅ Screenshot Command

```bash
lsblk
```

### ✅ Ubuntu

```bash
lsblk
```

### ✅ CentOS

```bash
lsblk
```

### ✅ WSL Note

Shows the WSL virtual disk instead of physical Windows disks.

---

# Example 4 – Display Mounted Filesystems

## ✅ Practical Example

Display all currently mounted filesystems.

### ✅ Command

```bash
mount
```

### ✅ Command Explanation

Shows all mounted filesystems along with their mount points and options.

### ✅ Expected Output

```text
/dev/sda1 on / type ext4 (...)
```

### ✅ Real-World Use Case

Verify whether a storage device has been mounted successfully.

### ✅ Screenshot Command

```bash
mount
```

### ✅ Ubuntu

```bash
mount
```

### ✅ CentOS

```bash
mount
```

### ✅ WSL Note

Displays WSL mount information and Windows-mounted drives.

---

# Example 5 – Show Mounted Filesystems

## ✅ Practical Example

Display mounted filesystems in a tree structure.

### ✅ Command

```bash
findmnt
```

### ✅ Command Explanation

Displays all mounted filesystems in an easy-to-read hierarchical format.

### ✅ Expected Output

```text
TARGET SOURCE
/      /dev/sda1
```

### ✅ Real-World Use Case

Useful when troubleshooting mount-related issues.

### ✅ Screenshot Command

```bash
findmnt
```

### ✅ Ubuntu

```bash
findmnt
```

### ✅ CentOS

```bash
findmnt
```

### ✅ WSL Note

Fully supported.

---

# Example 6 – View Filesystem UUID

## ✅ Practical Example

Display filesystem UUID information.

### ✅ Command

```bash
sudo blkid
```

### ✅ Command Explanation

Displays:

- UUID
- Filesystem type
- Partition label

### ✅ Expected Output

```text
/dev/sda1: UUID="AB12-CD34" TYPE="ext4"
```

### ✅ Real-World Use Case

Used while configuring:

```text
/etc/fstab
```

for permanent mounts.

### ✅ Screenshot Command

```bash
sudo blkid
```

### ✅ Ubuntu

```bash
sudo blkid
```

### ✅ CentOS

```bash
sudo blkid
```

### ✅ WSL Note

May show limited output because WSL uses a virtual filesystem.

---

# Example 7 – Display RAM and Swap

## ✅ Practical Example

Display memory and swap usage.

### ✅ Command

```bash
free -h
```

### ✅ Command Explanation

Displays:

- Total RAM
- Used RAM
- Free RAM
- Swap usage

### ✅ Expected Output

```text
              total used free
Mem:          3.8G 1.5G 2.3G
Swap:         2.0G 0B 2.0G
```

### ✅ Real-World Use Case

Monitor system memory before starting large applications.

### ✅ Screenshot Command

```bash
free -h
```

### ✅ Ubuntu

```bash
free -h
```

### ✅ CentOS

```bash
free -h
```

### ✅ WSL Note

Swap values depend on the WSL configuration.

---

# Example 8 – View Disk Partitions

## ✅ Practical Example

Display partition table information.

### ✅ Command

```bash
sudo fdisk -l
```

### ✅ Command Explanation

Lists:

- Disks
- Partitions
- Sizes
- Partition types

### ✅ Expected Output

```text
Disk /dev/sda: 50 GiB
/dev/sda1 Linux filesystem
```

### ✅ Real-World Use Case

Used before partitioning or resizing storage devices.

### ✅ Screenshot Command

```bash
sudo fdisk -l
```

### ✅ Ubuntu

```bash
sudo fdisk -l
```

### ✅ CentOS

```bash
sudo fdisk -l
```

### ✅ WSL Note

Physical Windows disks are generally **not** visible. Output is limited to the WSL virtual disk.

---

# Example 9 – Check Inode Usage

## ✅ Practical Example

Display inode usage for mounted filesystems.

### ✅ Command

```bash
df -i
```

### ✅ Command Explanation

Shows:

- Total inodes
- Used inodes
- Free inodes

### ✅ Expected Output

```text
Filesystem Inodes IUsed IFree IUse%
/dev/sda1 3276800 12345 3264455 1%
```

### ✅ Real-World Use Case

Useful when a filesystem reports **"No space left on device"** even though disk space is still available.

### ✅ Screenshot Command

```bash
df -i
```

### ✅ Ubuntu

```bash
df -i
```

### ✅ CentOS

```bash
df -i
```

### ✅ WSL Note

Works normally.

---

# Example 10 – Check Root Filesystem Usage

## ✅ Practical Example

Display usage information for the root (`/`) filesystem.

### ✅ Command

```bash
df -h /
```

### ✅ Command Explanation

Shows only the disk usage of the root filesystem instead of all mounted filesystems.

### ✅ Expected Output

```text
Filesystem Size Used Avail Use%
/dev/sda1   50G 18G 30G 38%
```

### ✅ Real-World Use Case

Monitor the primary filesystem where Linux is installed to prevent system outages caused by a full root partition.

### ✅ Screenshot Command

```bash
df -h /
```

### ✅ Ubuntu

```bash
df -h /
```

### ✅ CentOS

```bash
df -h /
```

### ✅ WSL Note

Works normally and displays the usage of the WSL root filesystem.

---

# Summary of Commands

| Example | Command | Purpose |
|---------|---------|---------|
| 1 | `df -h` | Check disk usage |
| 2 | `du -sh /home` | Check directory size |
| 3 | `lsblk` | List block devices |
| 4 | `mount` | Display mounted filesystems |
| 5 | `findmnt` | Show mount tree |
| 6 | `sudo blkid` | View filesystem UUID |
| 7 | `free -h` | Display RAM and swap |
| 8 | `sudo fdisk -l` | View partitions |
| 9 | `df -i` | Check inode usage |
| 10 | `df -h /` | Check root filesystem usage |

> **Interview Tip:** These commands (`df`, `du`, `lsblk`, `mount`, `findmnt`, `blkid`, `free`, `fdisk`, and `df -i`) are among the most frequently asked practical Linux commands in interviews. Make sure you understand **what each command displays, when to use it, and how its output is interpreted**, especially the differences between `df` and `du`, and between `mount` and `findmnt`.

---

