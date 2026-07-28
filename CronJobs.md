# Part 6.1 – Introduction

# Cron Jobs (Complete Professional Notes)

Cron Jobs are one of the most important Linux administration topics. They are widely used by **Linux Administrators, DevOps Engineers, Cloud Engineers, System Administrators, and Database Administrators** to automate repetitive tasks.

In this section, you will learn what Cron Jobs are, how they work, how to create and manage them, and how they are used in real-world production servers.

---

# What are Cron Jobs?

## Definition

A **Cron Job** is a scheduled task that runs automatically at a specified time or interval without requiring manual execution.

Cron Jobs help automate repetitive tasks such as:

- System backups
- Cleaning temporary files
- Sending email reports
- Database backups
- Monitoring server health
- Running shell scripts
- Rotating log files
- Updating applications

Instead of manually executing commands every day, Linux can run them automatically using Cron Jobs.

---

## Real-Life Example

Imagine you work as a Linux Administrator for an e-commerce company.

Every night at **2:00 AM**, you need to:

- Backup the MySQL database
- Compress log files
- Delete temporary files
- Generate server reports

Doing this manually every day is time-consuming and error-prone.

Instead, you create Cron Jobs, and Linux performs these tasks automatically every night.

---

# What is Cron?

## Definition

**Cron** is a background service (daemon) in Linux responsible for executing scheduled tasks automatically.

It continuously checks the configured schedule and runs commands when the specified time arrives.

Think of Cron as a scheduler or alarm clock for Linux.

---

## Why is Cron Important?

Cron allows administrators to automate routine system maintenance without manual intervention.

Examples include:

- Running backups every night
- Restarting services automatically
- Checking disk usage
- Cleaning old log files
- Monitoring system resources
- Running shell scripts
- Sending scheduled emails

---

# What is crontab?

## Definition

**crontab** (Cron Table) is a configuration file where users define their scheduled Cron Jobs.

Each user can have their own crontab file.

Linux reads these entries and executes the commands at the scheduled time.

---

## Example

Open the crontab editor:

```bash
crontab -e
```

View existing Cron Jobs:

```bash
crontab -l
```

---

## Real-World Example

A DevOps Engineer creates the following Cron Job:

```bash
0 2 * * * /home/devops/backup.sh
```

Every day at **2:00 AM**, Linux automatically runs the backup script.

---

# What is crond?

## Definition

**crond** is the Cron daemon process.

It runs continuously in the background and checks every minute whether any scheduled task needs to be executed.

---

## Ubuntu

Service name:

```text
cron
```

---

## CentOS / RHEL

Service name:

```text
crond
```

---

## Verify Process

Ubuntu:

```bash
ps aux | grep cron
```

CentOS:

```bash
ps aux | grep crond
```

---

# Difference between Cron and Cron Jobs

| Cron | Cron Job |
|-------|----------|
| Background service (daemon) | Scheduled task |
| Executes jobs | Gets executed by Cron |
| Runs continuously | Runs only at scheduled time |
| Service name: `cron` / `crond` | User-defined command |
| Managed using `systemctl` or `service` | Managed using `crontab` |

### Example

Cron Service:

```bash
sudo service cron status
```

Cron Job:

```bash
30 1 * * * /home/user/backup.sh
```

---

# Why Cron Jobs are Used

Cron Jobs are used to automate repetitive and scheduled tasks.

---

## 1. Task Automation

Automatically execute commands without manual intervention.

Example:

```bash
0 8 * * * echo "Good Morning"
```

---

## 2. Scheduled Backups

Automatically create backups every night.

Example:

```bash
0 2 * * * /home/user/backup.sh
```

---

## 3. Log Cleanup

Delete old log files automatically.

Example:

```bash
0 1 * * 0 rm -rf /var/log/oldlogs/*
```

---

## 4. Email Reports

Automatically send daily reports.

Example:

```bash
0 7 * * * /home/user/send_report.sh
```

---

## 5. System Monitoring

Run monitoring scripts every five minutes.

Example:

```bash
*/5 * * * * /home/user/monitor.sh
```

---

## 6. Database Backup

Backup MySQL or PostgreSQL automatically.

Example:

```bash
0 3 * * * mysqldump database > backup.sql
```

---

## 7. Running Shell Scripts

Execute automation scripts regularly.

Example:

```bash
30 10 * * * /home/user/script.sh
```

---

## 8. Server Maintenance

Clean cache and temporary files automatically.

Example:

```bash
0 4 * * * rm -rf /tmp/*
```

---

# Cron Service in Different Linux Distributions

| Distribution | Service Name | Management Command |
|--------------|--------------|--------------------|
| Ubuntu | cron | `systemctl` / `service` |
| Debian | cron | `systemctl` / `service` |
| CentOS 7/8/9 | crond | `systemctl` |
| RHEL | crond | `systemctl` |
| Amazon Linux 2 | crond | `systemctl` |
| WSL Ubuntu | cron | `service cron` |

---

# WSL Important Note

If you are using **WSL Ubuntu**, checking the Cron service with:

```bash
sudo service cron status
```

may show whether the service is running.

If the service is stopped:

```bash
sudo service cron start
```

---

## Why doesn't `systemctl` work in WSL?

Many WSL installations do not use **systemd** as the init system (PID 1).

Since `systemctl` communicates with `systemd`, commands such as:

```bash
systemctl status cron
```

may display:

```text
System has not been booted with systemd as init system.
Can't operate.
```

Instead, use:

```bash
service cron status
```

or

```bash
ps aux | grep cron
```

---

# Cron Architecture

Cron works in the following sequence:

```text
User
   │
   ▼
crontab
   │
   ▼
Cron Daemon (cron / crond)
   │
   ▼
Scheduled Time
   │
   ▼
Execute Command
```

### Explanation

1. User creates a Cron Job.
2. It is saved in the crontab file.
3. The Cron daemon checks the schedule every minute.
4. When the scheduled time arrives, Cron executes the command automatically.

---

# Crontab File Locations

## `/etc/crontab`

System-wide Cron configuration file.

Used for scheduled tasks that affect the entire system.

---

## `/var/spool/cron/`

Stores individual user crontab files.

Each user has a separate Cron configuration.

---

## `/etc/cron.hourly`

Scripts inside this directory run every hour.

---

## `/etc/cron.daily`

Scripts run once every day.

---

## `/etc/cron.weekly`

Scripts run once every week.

---

## `/etc/cron.monthly`

Scripts run once every month.

---

# Cron Syntax

Basic syntax:

```bash
* * * * * command
```

---

## Cron Fields

| Field | Description |
|--------|-------------|
| 1st | Minute (0–59) |
| 2nd | Hour (0–23) |
| 3rd | Day of Month (1–31) |
| 4th | Month (1–12) |
| 5th | Day of Week (0–7, where 0 or 7 = Sunday) |
| 6th | Command to execute |

---

## Example

```bash
30 2 * * * /home/user/backup.sh
```

Meaning:

- Minute → 30
- Hour → 2 AM
- Every day
- Every month
- Every weekday
- Execute `backup.sh`

---

# Cron Special Characters

## `*` (Asterisk)

Means **every possible value**.

Example:

```bash
* * * * *
```

Runs every minute.

---

## `,` (Comma)

Specifies multiple values.

Example:

```bash
1,15,30 * * * *
```

Runs at minute **1**, **15**, and **30** of every hour.

---

## `-` (Hyphen)

Specifies a range.

Example:

```bash
1-5 * * * *
```

Runs during minutes **1 to 5**.

---

## `/` (Slash)

Specifies intervals.

Example:

```bash
*/5 * * * *
```

Runs every **5 minutes**.

---

# Common crontab Commands

## Edit Cron Jobs

```bash
crontab -e
```

Opens the crontab editor.

---

## List Cron Jobs

```bash
crontab -l
```

Displays all scheduled Cron Jobs for the current user.

---

## Remove Cron Jobs

```bash
crontab -r
```

Deletes all Cron Jobs for the current user.

> **Warning:** This command permanently removes all scheduled Cron Jobs for the user.

---

## View Another User's Cron Jobs

```bash
sudo crontab -u username -l
```

Displays the Cron Jobs of the specified user.

---

## Edit Another User's Cron Jobs

```bash
sudo crontab -u username -e
```

Allows an administrator to edit another user's crontab.

---

# Verify Cron Service

## Ubuntu

```bash
systemctl status cron
```

---

## WSL Ubuntu

```bash
service cron status
```

---

## CentOS / RHEL

```bash
systemctl status crond
```

---

# Key Takeaways

- **Cron** is the service that schedules tasks.
- **crontab** is the configuration file used to define scheduled tasks.
- **crond** is the daemon process (mainly on CentOS/RHEL).
- Cron Jobs automate repetitive tasks such as backups, monitoring, log cleanup, and maintenance.
- WSL users should use `service cron` instead of `systemctl` unless `systemd` has been enabled.
- Understanding Cron syntax and special characters is essential for Linux Administration, DevOps, AWS, and Cloud Computing roles.
