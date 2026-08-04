# Part 7.1 – Introduction

# SSH (Complete Professional Notes)

SSH is one of the most important topics in **Linux Administration, DevOps, Cloud Computing, AWS, System Administration, and Cyber Security**.

It is the standard protocol used to securely connect to remote Linux servers over a network.

In this section, you will learn what SSH is, how it works, why it is used, and how to manage SSH services on **Ubuntu, WSL, CentOS, RHEL, and Amazon Linux**.

---

# What is SSH?

## ✅ Definition

**SSH (Secure Shell)** is a secure network protocol used to remotely access and manage another computer over an encrypted connection.

SSH allows administrators and developers to log in to remote Linux servers, execute commands, transfer files securely, and perform system administration tasks without physically accessing the machine.

Unlike older protocols such as Telnet, SSH encrypts all communication, making it safe to use over public networks.

---

## Real-World Example

Suppose your company hosts a website on an **AWS EC2 Ubuntu Server**.

Instead of visiting the data center, you simply connect from your laptop:

```bash
ssh ubuntu@54.210.120.50
```

Once connected, you can:

- Deploy applications
- Restart services
- Install software
- View logs
- Configure servers

This is one of the most common tasks performed by DevOps Engineers.

---

# Full Form of SSH

**SSH** stands for:

> **Secure Shell**

It provides encrypted communication between a client and a remote server.

---

# What is Remote Login?

## Definition

Remote Login means accessing another computer through a network without physically being present.

SSH enables secure remote login.

---

## Example

Laptop:

```text
192.168.1.10
```

Remote Server:

```text
192.168.1.20
```

Connection:

```bash
ssh user@192.168.1.20
```

Now you can control the remote machine from your local computer.

---

# What is an SSH Client?

## Definition

An **SSH Client** is the computer or application that initiates the SSH connection.

It sends the login request to the SSH server.

Examples:

- Linux Terminal
- Windows PowerShell
- OpenSSH Client
- PuTTY
- MobaXterm

---

## Example

```bash
ssh ubuntu@192.168.1.100
```

Your local machine acts as the SSH client.

---

# What is an SSH Server?

## Definition

The **SSH Server** is the remote machine running the **sshd (SSH daemon)** service.

It listens for incoming SSH connections and authenticates users.

---

## Example

Ubuntu:

```bash
systemctl status ssh
```

CentOS:

```bash
systemctl status sshd
```

---

# Difference Between SSH and Telnet

| SSH | Telnet |
|------|---------|
| Secure protocol | Insecure protocol |
| Encrypts all communication | Sends data as plain text |
| Uses Port 22 | Uses Port 23 |
| Recommended for production | Mostly obsolete |
| Supports key-based authentication | Password authentication only |
| Secure remote administration | Not recommended over public networks |

---

# Why SSH is Used

SSH is widely used because it provides secure remote access to Linux systems.

---

## 1. Secure Remote Login

Administrators securely access remote Linux servers.

Example:

```bash
ssh ubuntu@192.168.1.100
```

---

## 2. Remote Server Management

Manage servers from anywhere.

Tasks include:

- Installing packages
- Restarting services
- Creating users
- Checking logs
- Updating software

---

## 3. Secure File Transfer

Transfer files securely using:

- SCP
- SFTP

Example:

```bash
scp notes.txt ubuntu@192.168.1.100:/home/ubuntu
```

---

## 4. Remote Command Execution

Execute commands without logging in interactively.

Example:

```bash
ssh ubuntu@192.168.1.100 "uptime"
```

---

## 5. GitHub Authentication

SSH keys allow secure authentication with GitHub.

Example:

```bash
git clone git@github.com:user/project.git
```

No password is required after SSH keys are configured.

---

## 6. Cloud Server Management

SSH is commonly used to manage cloud servers.

Examples:

- AWS EC2
- Azure Virtual Machines
- Google Compute Engine

---

## 7. DevOps Automation

SSH is widely used by:

- Ansible
- Jenkins
- Shell scripts
- CI/CD pipelines

---

## 8. Secure Administration

Administrators perform tasks such as:

- Software installation
- Log monitoring
- Service management
- User management

without exposing passwords over the network.

---

# SSH in Different Linux Distributions

| Distribution | SSH Service | Management Command |
|--------------|------------|--------------------|
| Ubuntu | ssh | `systemctl` / `service` |
| Debian | ssh | `systemctl` / `service` |
| CentOS 7/8/9 | sshd | `systemctl` |
| RHEL | sshd | `systemctl` |
| Amazon Linux 2 | sshd | `systemctl` |
| WSL Ubuntu | ssh | `service ssh` |

---

# WSL Important Note

Check SSH service:

```bash
sudo service ssh status
```

If SSH is not installed:

```bash
sudo apt update
```

```bash
sudo apt install openssh-server
```

Start SSH:

```bash
sudo service ssh start
```

Verify again:

```bash
sudo service ssh status
```

---

## Why doesn't `systemctl` work in WSL?

Many WSL installations do not use **systemd** as the init system (PID 1).

Since `systemctl` depends on `systemd`, running:

```bash
systemctl status ssh
```

may display:

```text
System has not been booted with systemd as init system.
Can't operate.
```

Instead, use:

```bash
service ssh status
```

or

```bash
ps aux | grep sshd
```

If systemd has been enabled in WSL, `systemctl` commands will work.

---

# SSH Architecture

SSH communication follows this process:

```text
SSH Client
     │
     ▼
Encrypted Connection
     │
     ▼
SSH Server (sshd)
     │
     ▼
Authentication
     │
     ▼
Remote Shell
```

### Explanation

1. The SSH Client requests a connection.
2. The connection is encrypted.
3. The SSH Server (`sshd`) receives the request.
4. The user is authenticated.
5. A secure remote shell is established.

---

# SSH Default Port

SSH listens on **Port 22** by default.

---

## Verify Listening Port

```bash
ss -tlnp | grep :22
```

Example Output:

```text
LISTEN 0 128 *:22 *:*
```

---

## Alternative

```bash
netstat -tlnp | grep :22
```

---

# Important SSH Files

## `/etc/ssh/sshd_config`

Main configuration file for the SSH server.

Used to configure:

- Port number
- Root login
- Password authentication
- Public key authentication

---

## `/etc/ssh/ssh_config`

Configuration file for the SSH client.

Applies to outgoing SSH connections.

---

## `~/.ssh/`

User's SSH configuration directory.

Contains:

- SSH keys
- Known hosts
- Client configuration

---

## `~/.ssh/id_rsa`

Private SSH key.

> **Never share this file with anyone.**

---

## `~/.ssh/id_rsa.pub`

Public SSH key.

Safe to copy to remote servers or GitHub.

---

## `~/.ssh/authorized_keys`

Contains trusted public keys that are allowed to log in.

If your public key exists in this file, passwordless login is possible.

---

## `~/.ssh/known_hosts`

Stores fingerprints of previously connected SSH servers.

Helps prevent man-in-the-middle attacks.

---

# SSH Syntax

## Basic Login

```bash
ssh username@hostname
```

Example:

```bash
ssh rahul@server.example.com
```

---

## Using IP Address

```bash
ssh ubuntu@192.168.1.100
```

---

## Using a Custom Port

```bash
ssh -p 2222 user@server
```

Useful when the SSH server listens on a port other than **22**.

---

# Common SSH Commands

## Connect to a Server

```bash
ssh user@host
```

---

## Connect Using a Custom Port

```bash
ssh -p 2222 user@host
```

---

## Generate an SSH Key Pair

```bash
ssh-keygen
```

---

## Copy Public Key to a Server

```bash
ssh-copy-id user@host
```

---

## Secure Copy (SCP)

```bash
scp file.txt user@host:/home/user
```

Copies a file securely to the remote server.

---

## Secure File Transfer (SFTP)

```bash
sftp user@host
```

Starts an interactive secure file transfer session.

---

## Check SSH Version

```bash
ssh -V
```

Example Output:

```text
OpenSSH_9.x
```

---

## Verbose Mode

```bash
ssh -v user@host
```

Displays detailed connection and authentication information.

Useful for troubleshooting.

---

# Verify SSH Service

## Ubuntu

```bash
systemctl status ssh
```

---

## WSL Ubuntu

```bash
service ssh status
```

---

## CentOS / RHEL / Amazon Linux

```bash
systemctl status sshd
```

---

# Key Takeaways

- SSH (Secure Shell) is the standard protocol for secure remote administration.
- SSH encrypts all communication between the client and server.
- SSH uses **Port 22** by default.
- Ubuntu uses the **ssh** service, while CentOS and RHEL use **sshd**.
- WSL users typically manage SSH using the `service` command unless `systemd` is enabled.
- SSH supports password authentication and key-based authentication, with key-based authentication being the recommended and more secure method.
- SSH is widely used for Linux Administration, DevOps, Cloud Computing, GitHub authentication, and AWS EC2 server management.

---
