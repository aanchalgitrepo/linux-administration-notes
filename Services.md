# Part 5.1 – Introduction

Linux Services are one of the most important topics in Linux Administration, Technical Support, DevOps, Cloud Computing, and System Administration. Services are responsible for running applications and system processes in the background without requiring user interaction.

> **Note for WSL Users:** These notes include commands for **WSL Ubuntu**, **Ubuntu Server**, and **CentOS/RHEL**. Since WSL behaves differently from a normal Linux server, some `systemctl` commands may not work unless `systemd` is enabled.

---

# What are Services in Linux?

## Definition

A **Service** is a background program or process that starts automatically (or manually) and performs specific tasks without direct user interaction.

Services are also known as **background services** because they continue running even when no user is actively using them.

Examples of Linux services include:

- SSH Server
- Web Server (Apache, Nginx)
- MySQL Database
- Docker
- Cron Scheduler
- Network Manager

Unlike normal applications, services continue running in the background and wait for requests from users or other programs.

---

## Example

When you access a website hosted on Linux:

```text
Browser
    │
    ▼
Nginx Service
    │
    ▼
Website Response
```

Here, **Nginx** is running as a service in the background.

---

## Real-World Example

Suppose an e-commerce website runs on an Ubuntu server.

Services running continuously:

- Nginx → Serves the website
- MySQL → Stores customer data
- SSH → Allows remote login
- Docker → Runs application containers
- Cron → Executes scheduled backup jobs

Even if no one is logged into the server, these services continue to run.

---

# What is a Daemon?

## Definition

A **Daemon** is a background process that starts automatically or manually and continuously waits for requests or events.

In Linux, most services run as daemon processes.

Daemon process names usually end with the letter **d**.

Examples:

| Daemon | Purpose |
|---------|----------|
| sshd | SSH Server |
| httpd | Apache Web Server (CentOS/RHEL) |
| crond | Cron Scheduler |
| mysqld | MySQL Database |
| systemd | System Manager |

---

## How Daemon Works

```text
System Starts
      │
      ▼
Daemon Starts
      │
      ▼
Runs in Background
      │
      ▼
Waits for Requests
      │
      ▼
Processes Requests
```

---

## Check Running Daemons (WSL Compatible)

```bash
ps aux
```

Search for a daemon:

```bash
ps aux | grep ssh
```

or

```bash
pgrep sshd
```

---

## Real-World Example

When you connect to a Linux server using SSH:

```text
Laptop
    │
SSH Request
    │
    ▼
sshd Daemon
    │
Authenticates User
    │
    ▼
Remote Login
```

---

# What is systemd?

## Definition

**systemd** is the modern initialization system (Init System) and service manager used by most Linux distributions.

It is responsible for:

- Starting the operating system
- Managing services
- Monitoring background processes
- Managing system startup
- Logging
- Managing dependencies

Most modern Linux distributions use **systemd**.

---

## Distributions Using systemd

| Distribution | Uses systemd |
|--------------|--------------|
| Ubuntu | ✅ Yes |
| Debian | ✅ Yes |
| CentOS 7/8/9 | ✅ Yes |
| RHEL | ✅ Yes |
| Fedora | ✅ Yes |
| Amazon Linux 2 | ✅ Yes |

---

## Responsibilities of systemd

- Starts services during boot
- Stops services
- Restarts services
- Enables services at boot
- Disables services
- Checks service status
- Manages dependencies between services

---

## Real-World Example

When Ubuntu boots:

```text
Computer Starts
      │
      ▼
systemd Starts
      │
      ▼
SSH
Docker
Cron
NetworkManager
MySQL
```

---

# What is systemctl?

## Definition

`systemctl` is the command-line utility used to interact with **systemd**.

It allows administrators to start, stop, restart, enable, disable, and monitor Linux services.

---

## Example

```bash
systemctl status ssh
```

Displays the current status of the SSH service.

---

## Common Tasks

Using `systemctl`, you can:

- Start services
- Stop services
- Restart services
- Reload configuration
- Enable startup at boot
- Disable startup
- Check status
- View running services

---

# Why Services are Used

Linux services are used to automate and manage system tasks efficiently.

---

## 1. Background Processes

Services run continuously in the background.

Examples:

- SSH
- Docker
- MySQL

---

## 2. Automatic Startup

Important services automatically start whenever the system boots.

Example:

```text
Computer Boot
      │
      ▼
SSH Starts Automatically
```

---

## 3. Web Servers

Services host websites and web applications.

Examples:

- Apache
- Nginx

---

## 4. Databases

Database services store application data.

Examples:

- MySQL
- PostgreSQL
- MariaDB

---

## 5. SSH

SSH service enables secure remote administration.

---

## 6. Cron

Cron service automatically executes scheduled tasks.

Examples:

- Daily backups
- Log cleanup
- Email reports

---

## 7. Docker

Docker service manages containers.

Without the Docker service, containers cannot run.

---

## 8. Networking

Network services manage:

- Internet connectivity
- IP addresses
- DNS
- Routing

---

# Service Management in Different Linux Distributions

| Distribution | Service Manager | Main Command |
|--------------|-----------------|--------------|
| Ubuntu 16+ | systemd | `systemctl` |
| Debian | systemd | `systemctl` |
| CentOS 7/8/9 | systemd | `systemctl` |
| RHEL | systemd | `systemctl` |
| Amazon Linux 2 | systemd | `systemctl` |
| CentOS 6 | SysVinit | `service` |

---

# WSL Important Note

If you execute:

```bash
systemctl status ssh
```

you may receive:

```text
System has not been booted with systemd as init system (PID 1).
Can't operate.
Failed to connect to bus: Host is down
```

## Why does this happen?

By default, many WSL installations do **not** start Linux with `systemd` as the init system. As a result, `systemctl` cannot manage services unless `systemd` has been explicitly enabled in your WSL configuration.

---

## Alternative Commands for WSL

Check SSH service:

```bash
service ssh status
```

View running processes:

```bash
ps aux
```

Search SSH process:

```bash
ps aux | grep ssh
```

Check SSH daemon PID:

```bash
pgrep sshd
```

These commands are useful for checking services on WSL when `systemctl` is unavailable.

---

# Syntax

## Modern Linux (Ubuntu, Debian, CentOS 7+, RHEL, Amazon Linux)

```bash
systemctl [OPTION] SERVICE
```

Example:

```bash
systemctl restart nginx
```

---

## Older CentOS (SysVinit)

```bash
service SERVICE COMMAND
```

Example:

```bash
service sshd restart
```

---

# Common `systemctl` Commands

| Command | Purpose |
|----------|---------|
| `systemctl status nginx` | View service status |
| `systemctl start nginx` | Start a service |
| `systemctl stop nginx` | Stop a service |
| `systemctl restart nginx` | Restart a service |
| `systemctl reload nginx` | Reload configuration without full restart |
| `systemctl enable nginx` | Start automatically at boot |
| `systemctl disable nginx` | Disable automatic startup |
| `systemctl is-active nginx` | Check if service is active |
| `systemctl is-enabled nginx` | Check boot startup status |
| `systemctl list-units --type=service` | List running services |

---

# CentOS 6 (SysVinit) Commands

Check status:

```bash
service sshd status
```

Start service:

```bash
service sshd start
```

Stop service:

```bash
service sshd stop
```

Restart service:

```bash
service sshd restart
```

---

# WSL Alternatives

If:

```bash
systemctl status ssh
```

does not work, use:

Check service:

```bash
service ssh status
```

Search process:

```bash
ps aux | grep ssh
```

Find daemon process:

```bash
pgrep sshd
```

---

# Common Linux Services

| Ubuntu | CentOS/RHEL | Purpose |
|----------|-------------|----------|
| ssh | sshd | Secure Remote Login |
| cron | crond | Schedule automated tasks |
| nginx | nginx | Web Server |
| apache2 | httpd | Web Server |
| mysql | mysqld | MySQL Database |
| docker | docker | Container Engine |
| NetworkManager | NetworkManager | Network Management |

---

# Key Points

- A **service** is a background process that performs specific tasks.
- Most Linux services run as **daemon processes**.
- **systemd** is the modern service manager used in most Linux distributions.
- **systemctl** is the command used to manage services with systemd.
- Older Linux systems use the `service` command instead of `systemctl`.
- WSL may not support `systemctl` unless `systemd` is enabled.
- Learn both `systemctl` and `service` commands because interviews may cover Ubuntu, CentOS, RHEL, Amazon Linux, and WSL.
