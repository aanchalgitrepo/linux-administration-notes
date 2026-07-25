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

---

# Part 5.2A – Practical Examples (Examples 1–10)

This section contains the most commonly used Linux service management commands. Since these notes are designed for **WSL Ubuntu**, **Ubuntu Server**, **CentOS/RHEL**, and **Amazon Linux**, each example includes commands for different environments.

> **Important:** If `systemctl` does not work in your WSL, use the WSL alternatives provided below.

---

# Example 1 – Check Service Status

## Practical Example

Check whether the SSH service is running.

### Ubuntu (systemd)

```bash
systemctl status ssh
```

### CentOS / RHEL / Amazon Linux

```bash
systemctl status sshd
```

### Older CentOS 6

```bash
service sshd status
```

### WSL

```bash
service ssh status
```

### Command Explanation

- `status` displays the current state of a service.
- Shows whether the service is active, inactive, or failed.

### Expected Output

```text
Active: active (running)
```

or

```text
Active: inactive (dead)
```

### Real-World Use Case

Before connecting remotely, a Linux administrator checks whether the SSH service is running.

### Screenshot Command

```bash
service ssh status
```

> **WSL Note:** If `systemctl` shows:
>
> ```text
> System has not been booted with systemd...
> ```
>
> use:
>
> ```bash
> service ssh status
> ```

---

# Example 2 – Start a Service

## Practical Example

Start the SSH service.

### Ubuntu

```bash
sudo systemctl start ssh
```

### CentOS

```bash
sudo systemctl start sshd
```

### Older CentOS

```bash
sudo service sshd start
```

### WSL

```bash
sudo service ssh start
```

### Command Explanation

Starts the service if it is currently stopped.

### Expected Output

Normally no output appears if successful.

Verify:

```bash
service ssh status
```

### Real-World Use Case

Start SSH before allowing remote access to a server.

### Screenshot Command

```bash
sudo service ssh start
service ssh status
```

### WSL Note

Use `service` instead of `systemctl`.

---

# Example 3 – Stop a Service

## Practical Example

Stop the SSH service.

### Ubuntu

```bash
sudo systemctl stop ssh
```

### CentOS

```bash
sudo systemctl stop sshd
```

### Older CentOS

```bash
sudo service sshd stop
```

### WSL

```bash
sudo service ssh stop
```

### Command Explanation

Stops the running service.

### Expected Output

```text
Active: inactive (dead)
```

### Real-World Use Case

Stop SSH temporarily for maintenance or security.

### Screenshot Command

```bash
sudo service ssh stop
service ssh status
```

### WSL Note

Restart the service afterward if you still need SSH.

---

# Example 4 – Restart a Service

## Practical Example

Restart the SSH service.

### Ubuntu

```bash
sudo systemctl restart ssh
```

### CentOS

```bash
sudo systemctl restart sshd
```

### Older CentOS

```bash
sudo service sshd restart
```

### WSL

```bash
sudo service ssh restart
```

### Command Explanation

Stops and immediately starts the service.

### Expected Output

Usually no output if successful.

### Real-World Use Case

Restart a service after changing its configuration.

### Screenshot Command

```bash
sudo service ssh restart
service ssh status
```

### WSL Note

Recommended after modifying SSH configuration files.

---

# Example 5 – Reload a Service

## Practical Example

Reload a service without completely restarting it.

### Ubuntu

```bash
sudo systemctl reload nginx
```

### CentOS

```bash
sudo systemctl reload nginx
```

### Older CentOS

```bash
sudo service nginx reload
```

### WSL

Only if Nginx is installed:

```bash
sudo service nginx reload
```

### Command Explanation

Reloads configuration while keeping the service running.

### Expected Output

No output if successful.

### Real-World Use Case

Reload Nginx after updating website configuration.

### Screenshot Command

```bash
sudo service nginx reload
```

### WSL Note

Skip this example if Nginx is not installed.

---

# Example 6 – Enable a Service

## Practical Example

Enable SSH to start automatically during system boot.

### Ubuntu

```bash
sudo systemctl enable ssh
```

### CentOS

```bash
sudo systemctl enable sshd
```

### Older CentOS

```bash
chkconfig sshd on
```

### WSL

Not applicable in most WSL installations because there is no traditional Linux boot process.

### Command Explanation

Registers the service to start automatically after boot.

### Expected Output

```text
Created symlink...
```

### Real-World Use Case

Ensure SSH starts automatically whenever the server boots.

### Screenshot Command

Ubuntu Server:

```bash
sudo systemctl enable ssh
```

### WSL Note

Usually cannot be demonstrated on standard WSL.

---

# Example 7 – Disable a Service

## Practical Example

Prevent SSH from starting automatically.

### Ubuntu

```bash
sudo systemctl disable ssh
```

### CentOS

```bash
sudo systemctl disable sshd
```

### Older CentOS

```bash
chkconfig sshd off
```

### WSL

Not applicable.

### Command Explanation

Disables automatic startup during boot.

### Expected Output

```text
Removed symlink...
```

### Real-World Use Case

Disable unused services to improve security.

### Screenshot Command

Ubuntu Server:

```bash
sudo systemctl disable ssh
```

### WSL Note

Cannot normally be demonstrated on WSL.

---

# Example 8 – Check if a Service is Active

## Practical Example

Verify whether SSH is currently active.

### Ubuntu

```bash
systemctl is-active ssh
```

### CentOS

```bash
systemctl is-active sshd
```

### WSL

```bash
service ssh status
```

or

```bash
pgrep sshd
```

### Command Explanation

Checks whether a service is running.

### Expected Output

Ubuntu/CentOS

```text
active
```

WSL

Displays SSH status or the process ID of `sshd`.

### Real-World Use Case

Monitoring scripts often verify whether important services are active.

### Screenshot Command

```bash
service ssh status
```

### WSL Note

`pgrep sshd` is another quick way to confirm that the SSH daemon is running.

---

# Example 9 – List Running Services

## Practical Example

Display all running services.

### Ubuntu

```bash
systemctl list-units --type=service
```

### CentOS

```bash
systemctl list-units --type=service
```

### Older CentOS

```bash
service --status-all
```

### WSL

```bash
ps aux
```

### Command Explanation

Displays running services or processes.

### Expected Output

A list of active services or running processes.

### Real-World Use Case

Useful when troubleshooting or auditing a server.

### Screenshot Command

```bash
ps aux
```

### WSL Note

`ps aux` is the preferred alternative on WSL.

---

# Example 10 – WSL Alternatives (service, ps, pgrep)

## Practical Example

Use alternative commands to monitor services in WSL.

### Commands

Check service:

```bash
service ssh status
```

View all processes:

```bash
ps aux
```

Find SSH daemon:

```bash
pgrep sshd
```

Search for SSH process:

```bash
ps aux | grep ssh
```

### Command Explanation

- `service` → Basic service management
- `ps aux` → Shows all running processes
- `pgrep` → Finds a process ID by name
- `grep` → Filters command output

### Expected Output

Examples:

```text
sshd is running
```

```text
1234
```

```text
root     1234 ... sshd
```

### Real-World Use Case

System administrators use these commands to verify that critical background services are running when `systemctl` is unavailable.

### Screenshot Command

```bash
service ssh status

ps aux | grep ssh

pgrep sshd
```

### WSL Note

These commands are the most useful service-management alternatives for WSL users and are commonly used during troubleshooting.

---

# Key Learning Points

- `systemctl` is the standard tool for managing services on modern Linux distributions.
- WSL may not support `systemctl` unless `systemd` is enabled.
- Use `service`, `ps aux`, and `pgrep` as alternatives in WSL.
- Ubuntu uses the `ssh` service name, while CentOS/RHEL typically use `sshd`.
- Always verify service status after starting, stopping, or restarting a service.
- Knowing both `systemctl` and `service` commands is valuable for Linux Administration, DevOps, AWS, and Technical Support interviews.
