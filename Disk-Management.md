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

# Part 9.2B – Advanced Practical Examples (Examples 11–20)

This section covers advanced Disk Management tasks commonly performed by Linux Administrators, DevOps Engineers, Cloud Engineers, and System Administrators.

> **⚠️ Important for WSL Users**
>
> Commands such as `mount`, `umount`, `mkfs`, `fsck`, `swapon`, and `swapoff` may have limited functionality in WSL because it uses a virtual disk (`ext4.vhdx`). For full hands-on practice, use an Ubuntu Server VM, CentOS VM, or an AWS EC2 instance.

---

# Example 11 – Mount a Filesystem

## ✅ Practical Example

Mount a storage partition to a directory.

### ✅ Command

```bash
sudo mount /dev/sdb1 /mnt/data
```

### ✅ Command Explanation

- `mount` → Attaches a filesystem.
- `/dev/sdb1` → Partition to mount.
- `/mnt/data` → Mount point.

### ✅ Expected Output

Normally no output is displayed if the command succeeds.

Verify using:

```bash
mount | grep /mnt/data
```

or

```bash
findmnt
```

### ✅ Real-World Use Case

Mount a newly attached AWS EBS volume before using it.

### ✅ Screenshot Command

```bash
sudo mount /dev/sdb1 /mnt/data
findmnt
```

---

# Example 12 – Unmount a Filesystem

## ✅ Practical Example

Safely disconnect a mounted filesystem.

### ✅ Command

```bash
sudo umount /mnt/data
```

### ✅ Command Explanation

- `umount` removes the mounted filesystem.
- Files must not be in use.

### ✅ Expected Output

No output if successful.

Verify:

```bash
findmnt
```

### ✅ Real-World Use Case

Unmount a USB drive before removing it.

### ✅ Screenshot Command

```bash
sudo umount /mnt/data
findmnt
```

---

# Example 13 – Create a Filesystem

## ✅ Practical Example

Create an ext4 filesystem.

### ✅ Command

```bash
sudo mkfs.ext4 /dev/sdb1
```

### ✅ Command Explanation

Creates an ext4 filesystem on the partition.

**Warning:** This erases all existing data.

### ✅ Expected Output

```text
Creating filesystem...
Writing inode tables...
Writing superblocks...
```

### ✅ Real-World Use Case

Prepare a new disk before mounting it.

### ✅ Screenshot Command

```bash
sudo mkfs.ext4 /dev/sdb1
```

---

# Example 14 – Filesystem Check

## ✅ Practical Example

Check filesystem integrity.

### ✅ Command

```bash
sudo fsck /dev/sdb1
```

### ✅ Command Explanation

Scans the filesystem and repairs errors if possible.

### ✅ Expected Output

```text
Filesystem clean
```

or

```text
Fixed inode...
```

### ✅ Real-World Use Case

Repair corrupted filesystems after an unexpected shutdown.

### ✅ Screenshot Command

```bash
sudo fsck /dev/sdb1
```

---

# Example 15 – Enable Swap

## ✅ Practical Example

Enable swap space.

### ✅ Command

```bash
sudo swapon /swapfile
```

Verify:

```bash
free -h
```

### ✅ Command Explanation

Activates swap memory.

### ✅ Expected Output

```text
Swap: 2.0G
```

### ✅ Real-World Use Case

Increase virtual memory for systems with limited RAM.

### ✅ Screenshot Command

```bash
sudo swapon /swapfile
free -h
```

---

# Example 16 – Disable Swap

## ✅ Practical Example

Disable swap space.

### ✅ Command

```bash
sudo swapoff /swapfile
```

Verify:

```bash
free -h
```

### ✅ Command Explanation

Turns off swap memory.

### ✅ Expected Output

Swap usage becomes:

```text
Swap: 0B
```

### ✅ Real-World Use Case

Disable swap before resizing or deleting a swap file.

### ✅ Screenshot Command

```bash
sudo swapoff /swapfile
free -h
```

---

# Example 17 – Find Large Directories

## ✅ Practical Example

Find the largest directories in `/var`.

### ✅ Command

```bash
sudo du -h /var | sort -hr | head -10
```

### ✅ Command Explanation

- `du -h` → Shows directory sizes.
- `sort -hr` → Sorts from largest to smallest.
- `head -10` → Displays the top 10 results.

### ✅ Expected Output

```text
1.8G /var/log
700M /var/cache
```

### ✅ Real-World Use Case

Locate directories consuming excessive disk space.

### ✅ Screenshot Command

```bash
sudo du -h /var | sort -hr | head -10
```

---

# Example 18 – Analyze Disk Usage Recursively

## ✅ Practical Example

Analyze every subdirectory under `/home`.

### ✅ Command

```bash
du -h /home
```

### ✅ Command Explanation

Displays the size of every directory recursively.

### ✅ Expected Output

```text
50M /home/user/Documents
300M /home/user/Downloads
```

### ✅ Real-World Use Case

Identify which user directories consume the most storage.

### ✅ Screenshot Command

```bash
du -h /home
```

---

# Example 19 – Disk Cleanup Example

## ✅ Practical Example

Remove temporary files and package cache.

### ✅ Command

```bash
sudo rm -rf /tmp/*
sudo apt clean
```

> **CentOS/RHEL**

```bash
sudo yum clean all
```

### ✅ Command Explanation

- Removes temporary files.
- Clears package cache.

### ✅ Expected Output

Usually no output unless an error occurs.

### ✅ Real-World Use Case

Free disk space on production servers.

### ✅ Screenshot Command

```bash
sudo rm -rf /tmp/*
sudo apt clean
df -h
```

---

# Example 20 – Storage Monitoring Script

## ✅ Practical Example

Create a simple script to monitor disk usage.

### ✅ Command

Create the script:

```bash
nano disk-monitor.sh
```

Script:

```bash
#!/bin/bash

echo "Disk Usage Report"
echo "-----------------"
df -h

echo
echo "Largest Directories"
du -sh /home/*
```

Make executable:

```bash
chmod +x disk-monitor.sh
```

Run:

```bash
./disk-monitor.sh
```

### ✅ Command Explanation

The script:

- Displays disk usage.
- Displays user directory sizes.

### ✅ Expected Output

```text
Disk Usage Report

Filesystem Size Used Avail Use%

Largest Directories

2.3G /home/user
```

### ✅ Real-World Use Case

Automate daily storage monitoring using Cron Jobs.

### ✅ Screenshot Command

```bash
chmod +x disk-monitor.sh
./disk-monitor.sh
```

---

# Summary of Advanced Commands

| Example | Command | Purpose |
|---------|---------|---------|
| 11 | `mount` | Mount a filesystem |
| 12 | `umount` | Unmount a filesystem |
| 13 | `mkfs.ext4` | Create a filesystem |
| 14 | `fsck` | Check and repair a filesystem |
| 15 | `swapon` | Enable swap |
| 16 | `swapoff` | Disable swap |
| 17 | `du -h \| sort -hr \| head` | Find large directories |
| 18 | `du -h /home` | Analyze disk usage recursively |
| 19 | `rm -rf /tmp/*` + `apt clean` | Clean temporary files and package cache |
| 20 | `disk-monitor.sh` | Automate storage monitoring |

---

## 💼 Interview Tips

- Always **unmount a filesystem before running `fsck`** to avoid corruption.
- Be careful with `mkfs` because it **formats the partition and permanently erases data**.
- Understand the difference between **`mount`** (attach a filesystem) and **`umount`** (detach a filesystem).
- Use `du` to locate large directories and `df` to check overall filesystem usage.
- In cloud environments (AWS, Azure, GCP), the usual workflow is: **attach disk → create filesystem → mount → update `/etc/fstab` for persistence**.
- In WSL, commands like `mkfs`, `fsck`, and partition management are primarily for learning; full practice should be done on a Linux VM or cloud server.

---

# Part 9.3 – Practice Exercises

This section provides hands-on exercises to help you practice **Linux Disk Management**. These exercises are suitable for **Linux Administration, DevOps, AWS, Cloud Computing, Technical Support, and System Administration**.

> **📌 Note for WSL Users**
>
> Commands such as `df`, `du`, `lsblk`, `findmnt`, `mount`, and `free` work well in WSL.
>
> Commands that modify disks (`fdisk`, `mkfs`, `fsck`, `swapon`, `swapoff`) should preferably be practiced on an **Ubuntu Server VM**, **CentOS VM**, or **AWS EC2** instance.

---

# ✅ Practice Exercise 1 – Check Disk Usage

### Objective

View the disk usage of all mounted filesystems.

### Command

```bash
df -h
```

### Expected Result

- Displays disk usage in a human-readable format.
- Shows total, used, and available space.

---

# ✅ Practice Exercise 2 – Check Root Filesystem Usage

### Objective

Display usage information only for the root filesystem.

### Command

```bash
df -h /
```

### Expected Result

Shows storage usage of the root (`/`) partition.

---

# ✅ Practice Exercise 3 – Check Home Directory Size

### Objective

Display the total size of your home directory.

### Command

```bash
du -sh ~
```

### Expected Result

Example:

```text
2.1G    /home/user
```

---

# ✅ Practice Exercise 4 – Find the Largest Directories

### Objective

Identify directories consuming the most disk space.

### Command

```bash
du -h ~ | sort -hr | head -10
```

### Expected Result

Lists the ten largest directories.

---

# ✅ Practice Exercise 5 – List Block Devices

### Objective

Display available storage devices.

### Command

```bash
lsblk
```

### Expected Result

Shows:

- Disks
- Partitions
- Mount points

---

# ✅ Practice Exercise 6 – Display Mounted Filesystems

### Objective

Display currently mounted filesystems.

### Command

```bash
findmnt
```

### Expected Result

Shows the filesystem hierarchy and mount points.

---

# ✅ Practice Exercise 7 – View Memory and Swap

### Objective

Display RAM and swap usage.

### Command

```bash
free -h
```

### Expected Result

Displays:

- Total RAM
- Used RAM
- Available RAM
- Swap usage

---

# ✅ Practice Exercise 8 – Check Inode Usage

### Objective

Display inode usage.

### Command

```bash
df -i
```

### Expected Result

Shows:

- Total inodes
- Used inodes
- Free inodes

---

# ✅ Practice Exercise 9 – View Filesystem UUID

### Objective

Display filesystem UUID information.

### Command

```bash
sudo blkid
```

### Expected Result

Displays UUID and filesystem type.

---

# ✅ Practice Exercise 10 – Analyze Entire Home Directory

### Objective

Display the size of every directory under `/home`.

### Command

```bash
du -h /home
```

### Expected Result

Shows recursive directory sizes.

---

# ✅ Practice Exercise 11 – Create a Disk Usage Report

### Objective

Save disk usage information to a file.

### Command

```bash
df -h > disk-report.txt
cat disk-report.txt
```

### Expected Result

Creates a report containing disk usage information.

---

# ✅ Practice Exercise 12 – Create a Storage Monitoring Script

### Objective

Automate disk usage reporting.

### Command

```bash
nano disk-monitor.sh
```

Paste:

```bash
#!/bin/bash

echo "===== Disk Usage ====="
df -h

echo
echo "===== Home Directory Size ====="
du -sh ~

echo
echo "===== Memory Usage ====="
free -h
```

Make executable:

```bash
chmod +x disk-monitor.sh
```

Run:

```bash
./disk-monitor.sh
```

### Expected Result

Displays:

- Disk usage
- Home directory size
- RAM and swap usage

---

# ✅ WSL-Friendly Exercises

The following exercises work correctly in WSL:

```bash
df -h
```

```bash
df -h /
```

```bash
du -sh ~
```

```bash
du -h ~ | sort -hr | head
```

```bash
lsblk
```

```bash
findmnt
```

```bash
mount
```

```bash
free -h
```

```bash
df -i
```

```bash
sudo blkid
```

> **Note:** `blkid` output may be limited depending on your WSL configuration.

---

# ✅ Ubuntu Server Exercises

Practice the following on an Ubuntu Server VM or AWS EC2 instance.

```bash
sudo fdisk -l
```

```bash
sudo mkfs.ext4 /dev/sdb1
```

```bash
sudo mount /dev/sdb1 /mnt/data
```

```bash
sudo umount /mnt/data
```

```bash
sudo fsck /dev/sdb1
```

```bash
sudo swapon /swapfile
```

```bash
sudo swapoff /swapfile
```

---

# ✅ CentOS Equivalents

Most commands are the same.

| Ubuntu | CentOS |
|---------|---------|
| `df -h` | `df -h` |
| `du -sh` | `du -sh` |
| `lsblk` | `lsblk` |
| `findmnt` | `findmnt` |
| `mount` | `mount` |
| `umount` | `umount` |
| `free -h` | `free -h` |
| `blkid` | `blkid` |
| `fdisk -l` | `fdisk -l` |
| `mkfs.ext4` | `mkfs.xfs` or `mkfs.ext4` (depending on the filesystem you want) |

---

# ✅ Screenshot Guide

Capture screenshots for the following commands:

### Disk Usage

```bash
df -h
```

### Root Filesystem

```bash
df -h /
```

### Directory Size

```bash
du -sh ~
```

### Recursive Directory Size

```bash
du -h /home
```

### Largest Directories

```bash
du -h ~ | sort -hr | head -10
```

### Block Devices

```bash
lsblk
```

### Mounted Filesystems

```bash
findmnt
```

### RAM and Swap

```bash
free -h
```

### Filesystem UUID

```bash
sudo blkid
```

### Inode Usage

```bash
df -i
```

### Disk Report

```bash
df -h > disk-report.txt
cat disk-report.txt
```

### Storage Monitoring Script

```bash
chmod +x disk-monitor.sh
./disk-monitor.sh
```

---

# ✅ Common Errors & Troubleshooting

## Error 1 – Permission Denied

```text
Permission denied
```

### Solution

Run the command with `sudo`.

```bash
sudo blkid
```

---

## Error 2 – Command Not Found

```text
Command 'fdisk' not found
```

### Solution

Install the required package.

Ubuntu:

```bash
sudo apt update
sudo apt install fdisk
```

CentOS:

```bash
sudo yum install util-linux
```

---

## Error 3 – Device Busy

```text
target is busy
```

### Cause

The filesystem is currently in use.

### Solution

Close all files and processes using the mount point, then retry:

```bash
sudo umount /mnt/data
```

---

## Error 4 – Filesystem Check on Mounted Device

```text
fsck: Device is mounted
```

### Solution

Unmount the filesystem first.

```bash
sudo umount /dev/sdb1
sudo fsck /dev/sdb1
```

---

## Error 5 – Filesystem Already Mounted

```text
already mounted
```

### Solution

Verify with:

```bash
findmnt
```

or

```bash
mount
```

---

## Error 6 – Limited Output in WSL

### Cause

WSL uses a virtual disk (`ext4.vhdx`).

### Solution

Use an Ubuntu Server VM or cloud instance for advanced disk management tasks.

---

# ✅ Best Practices

- Monitor disk usage regularly using `df -h`.
- Use `du` to locate large directories before deleting files.
- Always verify mounted filesystems with `findmnt`.
- Run `fsck` only on unmounted filesystems.
- Back up important data before formatting (`mkfs`) or partitioning disks.
- Use descriptive mount points such as `/mnt/data` or `/mnt/backup`.
- Monitor inode usage with `df -i`, especially on servers handling many small files.
- Use swap only when necessary and monitor its usage with `free -h`.
- Test storage scripts before scheduling them with Cron.
- Avoid modifying physical partitions from WSL.

---

# ✅ Cleanup Commands

Remove the practice report:

```bash
rm -f disk-report.txt
```

Remove the monitoring script:

```bash
rm -f disk-monitor.sh
```

Remove temporary mount directory (if created):

```bash
sudo rmdir /mnt/data
```

Clear temporary files (use carefully):

```bash
sudo rm -rf /tmp/*
```

---

# 🎯 Practice Checklist

| Task | Status |
|------|:------:|
| Check disk usage with `df -h` | ☐ |
| Check root filesystem usage | ☐ |
| Check directory size with `du` | ☐ |
| Find largest directories | ☐ |
| List block devices | ☐ |
| Display mounted filesystems | ☐ |
| Check memory and swap | ☐ |
| View filesystem UUID | ☐ |
| Check inode usage | ☐ |
| Create a disk usage report | ☐ |
| Create and run a storage monitoring script | ☐ |
| Capture screenshots for GitHub | ☐ |

> **💡 Interview Tip:** Before an interview, practice explaining the differences between **`df` vs `du`**, **`mount` vs `umount`**, and **`lsblk` vs `blkid`**. These comparisons are commonly asked in Linux Administration, DevOps, and Cloud interviews.

---

# Part 9.4A – Interview Questions & Answers (1–15)

This section covers the **most frequently asked Disk Management interview questions** for **Linux Administration, DevOps, AWS, Cloud Computing, Technical Support, and System Administration** roles.

---

# Question 1. What is Disk Management in Linux?

## ✅ Professional Answer

Disk Management is the process of managing storage devices, partitions, filesystems, and mounted storage in a Linux operating system. It involves creating partitions, formatting disks, mounting filesystems, monitoring disk usage, managing swap space, and maintaining storage health.

Proper disk management ensures efficient storage utilization, better system performance, and prevents data loss.

### ✅ Example

```bash
df -h
```

Displays available and used disk space.

---

# Question 2. Why is Disk Management important?

## ✅ Professional Answer

Disk Management is important because it:

- Organizes storage efficiently.
- Prevents disk full errors.
- Improves system performance.
- Supports backup and disaster recovery.
- Helps monitor storage usage.
- Ensures applications have enough disk space.
- Maintains filesystem integrity.

### ✅ Example

A production server can stop accepting new log files if the `/var` partition becomes full. Using `df -h` helps identify and resolve such issues before they affect services.

---

# Question 3. What is a Filesystem?

## ✅ Professional Answer

A **filesystem** is the method Linux uses to organize, store, and retrieve files on a storage device.

Without a filesystem, Linux cannot read or write data to a disk.

Common Linux filesystems include:

- ext4
- XFS
- Btrfs
- FAT32
- exFAT
- NTFS

### ✅ Example

```bash
sudo mkfs.ext4 /dev/sdb1
```

Creates an **ext4** filesystem on the partition.

---

# Question 4. What is a Partition?

## ✅ Professional Answer

A partition is a logical division of a physical disk. A single hard disk can contain multiple partitions, each with its own filesystem.

Partitions help organize data and isolate operating systems or applications.

### ✅ Example

```text
Disk
│
├── /dev/sda1
├── /dev/sda2
└── /dev/sda3
```

Each partition can be mounted separately.

---

# Question 5. What is a Mount Point?

## ✅ Professional Answer

A **mount point** is a directory where a filesystem is attached so that users and applications can access its contents.

In Linux, every mounted storage device becomes part of the single directory hierarchy.

### ✅ Example

```bash
sudo mount /dev/sdb1 /mnt/data
```

The partition `/dev/sdb1` becomes accessible through `/mnt/data`.

---

# Question 6. What is the `df` command?

## ✅ Professional Answer

The `df` (Disk Filesystem) command displays disk space usage for mounted filesystems.

It shows:

- Total space
- Used space
- Available space
- Usage percentage
- Mount point

### ✅ Example

```bash
df -h
```

Sample Output:

```text
Filesystem Size Used Avail Use% Mounted on
/dev/sda1 50G 20G 28G 42% /
```

---

# Question 7. What is the difference between `df` and `du`?

## ✅ Professional Answer

| `df` | `du` |
|------|------|
| Displays filesystem usage | Displays directory or file usage |
| Works at filesystem level | Works at directory/file level |
| Shows free disk space | Shows which folders consume space |

### ✅ Example

```bash
df -h
```

```bash
du -sh /home
```

`df` tells you how much free space is available, while `du` helps identify which directories are using that space.

---

# Question 8. What is the `du` command?

## ✅ Professional Answer

The `du` (Disk Usage) command displays the amount of disk space used by files and directories.

It is mainly used to locate directories consuming excessive storage.

### ✅ Example

```bash
du -sh /var/log
```

Sample Output:

```text
850M    /var/log
```

---

# Question 9. What is the `lsblk` command?

## ✅ Professional Answer

`lsblk` lists all available block devices such as:

- Hard disks
- SSDs
- NVMe drives
- USB drives
- Partitions

It also shows mount points and device hierarchy.

### ✅ Example

```bash
lsblk
```

Sample Output:

```text
NAME   SIZE TYPE MOUNTPOINT
sda     50G disk
└─sda1  50G part /
```

---

# Question 10. What is the `mount` command?

## ✅ Professional Answer

The `mount` command attaches a filesystem to a directory so that it becomes accessible.

Until a filesystem is mounted, users cannot access its data.

### ✅ Example

```bash
sudo mount /dev/sdb1 /mnt/data
```

Now the files on `/dev/sdb1` are available under `/mnt/data`.

---

# Question 11. What is the `umount` command?

## ✅ Professional Answer

The `umount` command safely disconnects a mounted filesystem from the directory tree.

Unmounting ensures that all pending data is written to disk before the device is removed.

### ✅ Example

```bash
sudo umount /mnt/data
```

---

# Question 12. What is Swap Space?

## ✅ Professional Answer

Swap space is a dedicated area on a disk used as **virtual memory** when physical RAM is fully utilized.

Linux temporarily moves inactive memory pages from RAM to swap to free up memory for active processes.

Although swap is slower than RAM, it helps prevent applications from crashing due to insufficient memory.

### ✅ Example

```bash
free -h
```

Sample Output:

```text
Swap: 2.0G
```

---

# Question 13. How can you check disk usage in Linux?

## ✅ Professional Answer

The most common command is:

```bash
df -h
```

It displays:

- Total disk size
- Used space
- Free space
- Percentage used
- Mounted filesystem

To check the size of a specific directory:

```bash
du -sh /home
```

---

# Question 14. How can you check mounted filesystems?

## ✅ Professional Answer

Use the following commands:

```bash
mount
```

or

```bash
findmnt
```

`findmnt` provides a cleaner and more structured view of mounted filesystems.

### ✅ Example

```bash
findmnt
```

---

# Question 15. Which Disk Management commands should every Linux Administrator know?

## ✅ Professional Answer

Every Linux Administrator should be comfortable with the following commands:

| Command | Purpose |
|----------|---------|
| `df -h` | Check filesystem usage |
| `du -sh` | Check directory size |
| `lsblk` | List block devices |
| `mount` | Mount a filesystem |
| `umount` | Unmount a filesystem |
| `findmnt` | Display mounted filesystems |
| `blkid` | Show filesystem UUID |
| `free -h` | Display RAM and swap usage |
| `fdisk -l` | View partition information |
| `df -i` | Check inode usage |

### ✅ Example

```bash
df -h
lsblk
findmnt
free -h
```

These commands are used daily by Linux Administrators and DevOps Engineers to monitor storage, troubleshoot issues, and manage disks.

---

# 🎯 Interview Tips

- Clearly explain the difference between a **disk**, **partition**, **filesystem**, and **mount point**.
- Remember that **`df`** checks overall filesystem usage, while **`du`** checks the size of files and directories.
- Know that **`mount`** attaches a filesystem, whereas **`umount`** safely detaches it.
- Be able to explain why **swap space** exists and when it is used.
- Mention that advanced commands like `fdisk`, `mkfs`, and `fsck` are generally practiced on a Linux VM or cloud server rather than in WSL due to its virtual disk architecture.

---

# 📂 Part 9.4B – Interview Questions & Answers (16–30)

This section covers **advanced Disk Management interview questions** commonly asked in **Linux Administration, DevOps, AWS, Cloud Computing, Technical Support, and System Administration** interviews.

---

# Question 16. What is the difference between a physical disk and a partition?

## ✅ Professional Answer

A **physical disk** is the actual storage device (HDD, SSD, or NVMe), while a **partition** is a logical division of that disk.

A single disk can contain multiple partitions, each with its own filesystem.

### ✅ Example

```
Physical Disk
   │
   ├── /dev/sda1
   ├── /dev/sda2
   └── /dev/sda3
```

---

# Question 17. What is a mount point?

## ✅ Professional Answer

A mount point is a directory where a filesystem is attached so that users and applications can access its contents.

Without mounting, Linux cannot access the data stored on a partition.

### ✅ Example

```bash
sudo mount /dev/sdb1 /mnt/data
```

---

# Question 18. How can you check mounted filesystems?

## ✅ Professional Answer

You can use:

```bash
mount
```

or

```bash
findmnt
```

`findmnt` provides a cleaner tree structure.

### ✅ Example

```bash
findmnt
```

---

# Question 19. What is the purpose of the `blkid` command?

## ✅ Professional Answer

`blkid` displays filesystem metadata such as:

- UUID
- Filesystem type
- Partition label

It is commonly used while configuring `/etc/fstab`.

### ✅ Example

```bash
sudo blkid
```

---

# Question 20. What is inode usage?

## ✅ Professional Answer

An inode stores metadata about a file such as ownership, permissions, timestamps, and pointers to the file's data blocks.

Even if free disk space is available, a filesystem can become full if all inodes are used.

### ✅ Example

```bash
df -i
```

---

# Question 21. What is swap space and why is it used?

## ✅ Professional Answer

Swap space is virtual memory stored on disk.

When RAM becomes full, Linux moves inactive memory pages to swap, allowing applications to continue running.

Although swap is slower than RAM, it helps prevent memory exhaustion.

### ✅ Example

```bash
free -h
```

---

# Question 22. What is the difference between RAM and Swap?

## ✅ Professional Answer

| RAM | Swap |
|------|------|
| Physical memory | Disk-based virtual memory |
| Very fast | Much slower |
| Used first | Used when RAM is insufficient |

### ✅ Example

```bash
free -h
```

---

# Question 23. What is `fsck`?

## ✅ Professional Answer

`fsck` (File System Check) scans and repairs filesystem inconsistencies.

It should generally be run on an **unmounted** filesystem.

### ✅ Example

```bash
sudo fsck /dev/sdb1
```

---

# Question 24. What is `mkfs`?

## ✅ Professional Answer

`mkfs` creates a new filesystem on a partition.

It prepares a storage device for use.

**Warning:** It permanently erases existing data on the target partition.

### ✅ Example

```bash
sudo mkfs.ext4 /dev/sdb1
```

---

# Question 25. What is `/etc/fstab`?

## ✅ Professional Answer

`/etc/fstab` is the Linux configuration file that defines filesystems to be mounted automatically during system startup.

It commonly uses UUIDs instead of device names.

### ✅ Example

```text
UUID=xxxx-xxxx  /data  ext4  defaults  0  2
```

---

# Question 26. How do you identify large directories?

## ✅ Professional Answer

The `du` command helps identify directories consuming the most disk space.

### ✅ Example

```bash
du -h /var | sort -hr | head -10
```

---

# Question 27. What should you do if a Linux server reports "No space left on device"?

## ✅ Professional Answer

Follow these troubleshooting steps:

1. Check filesystem usage.

```bash
df -h
```

2. Check inode usage.

```bash
df -i
```

3. Identify large directories.

```bash
du -h / | sort -hr | head
```

4. Remove unnecessary files or logs.

---

# Question 28. Why is `findmnt` preferred over `mount`?

## ✅ Professional Answer

`findmnt` presents mounted filesystems in a structured tree format, making them easier to read and troubleshoot.

`mount` displays the same information but in a longer text format.

### ✅ Example

```bash
findmnt
```

---

# Question 29. Why is disk monitoring important in production servers?

## ✅ Professional Answer

Disk monitoring helps:

- Prevent storage exhaustion
- Avoid application failures
- Monitor log growth
- Improve server performance
- Support capacity planning
- Detect abnormal storage usage

### ✅ Example

```bash
df -h
```

scheduled using **Cron Jobs**.

---

# Question 30. Which Disk Management commands are most commonly used in DevOps?

## ✅ Professional Answer

Frequently used commands include:

```bash
df -h
```

```bash
du -sh
```

```bash
lsblk
```

```bash
findmnt
```

```bash
mount
```

```bash
umount
```

```bash
blkid
```

```bash
free -h
```

```bash
df -i
```

These commands are essential for monitoring and managing Linux storage in production environments.

---

# 📊 df vs du Comparison Table

| Feature | `df` | `du` |
|----------|------|------|
| Full Form | Disk Filesystem | Disk Usage |
| Purpose | Shows filesystem usage | Shows directory/file usage |
| Scope | Entire filesystem | Individual directories/files |
| Shows Free Space | ✅ Yes | ❌ No |
| Shows Directory Size | ❌ No | ✅ Yes |
| Common Option | `df -h` | `du -sh` |
| Typical Use Case | Monitor disk capacity | Find large directories |

---

# 📊 mount vs umount Comparison Table

| Feature | `mount` | `umount` |
|----------|----------|----------|
| Purpose | Attach a filesystem | Detach a filesystem |
| Makes Data Accessible | ✅ Yes | ❌ No |
| Required Before Use | ✅ Yes | ❌ No |
| Safe Device Removal | ❌ No | ✅ Yes |
| Typical Command | `mount /dev/sdb1 /mnt/data` | `umount /mnt/data` |

---

# 📊 Filesystem Comparison Table

| Feature | ext4 | XFS | Btrfs |
|----------|------|-----|--------|
| Default On | Ubuntu | RHEL/CentOS | SUSE (common) |
| Stability | Excellent | Excellent | Good |
| Performance | Very Good | Excellent for large files | Good |
| Journaling | ✅ Yes | ✅ Yes | ✅ Yes |
| Snapshots | ❌ No | ❌ No | ✅ Yes |
| Resize | Yes | Grow only | Grow & Shrink |
| Best For | General Linux systems | Enterprise servers | Advanced storage features |

---

# 📋 Disk Management Cheat Sheet

| Command | Purpose |
|----------|---------|
| `df -h` | Check filesystem usage |
| `df -i` | Check inode usage |
| `du -sh directory` | Directory size |
| `lsblk` | List disks and partitions |
| `findmnt` | Display mounted filesystems |
| `mount` | Mount a filesystem |
| `umount` | Unmount a filesystem |
| `blkid` | Show UUID and filesystem type |
| `free -h` | Display RAM and swap |
| `fdisk -l` | List partitions |
| `mkfs.ext4` | Create ext4 filesystem |
| `fsck` | Check and repair filesystem |
| `swapon` | Enable swap |
| `swapoff` | Disable swap |

---

# 📝 Summary

- Disk Management is essential for organizing, monitoring, and maintaining Linux storage.
- Partitions divide physical disks into logical sections.
- Filesystems organize how data is stored and accessed.
- Mount points make storage devices accessible through the Linux directory tree.
- `df` monitors overall filesystem usage, while `du` identifies large files and directories.
- `lsblk`, `blkid`, and `findmnt` help inspect storage devices and mounted filesystems.
- `mount` and `umount` are used to attach and detach filesystems.
- `mkfs` creates filesystems, and `fsck` checks filesystem integrity.
- Swap space provides virtual memory when RAM is exhausted.
- These concepts are fundamental for Linux Administration, DevOps, AWS, Cloud Computing, and System Administration.

---

# ⚡ Quick Revision Notes

Remember these commands:

```bash
df -h
```

```bash
du -sh /home
```

```bash
lsblk
```

```bash
findmnt
```

```bash
mount
```

```bash
umount
```

```bash
blkid
```

```bash
free -h
```

```bash
df -i
```

```bash
sudo fdisk -l
```

```bash
sudo mkfs.ext4 /dev/sdb1
```

```bash
sudo fsck /dev/sdb1
```

---

# 💼 Interview Tips

- Explain the storage flow clearly: **Physical Disk → Partition → Filesystem → Mount Point → User Access**.
- Be prepared to differentiate **`df` vs `du`**, **`mount` vs `umount`**, and **ext4 vs XFS vs Btrfs**.
- Mention that `fsck` should generally be run on **unmounted filesystems**.
- Clarify that `mkfs` formats a partition and erases existing data.
- In WSL, explain that advanced disk operations are limited because WSL uses a virtual disk (`ext4.vhdx`), so tasks like partitioning and filesystem creation are better practiced on a Linux VM or cloud instance.
- In DevOps interviews, relate these commands to practical scenarios such as monitoring storage with `df -h`, finding large log directories with `du`, mounting cloud volumes, and automating disk checks with Cron Jobs.

---
