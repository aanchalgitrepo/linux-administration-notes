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


# Part 7.2A – Practical Examples (Examples 1–10)

This section contains **beginner-to-professional SSH practical examples** for **Linux Administration, DevOps, AWS, Cloud Computing, and Technical Support**.

> **Note for WSL Users**
>
> Most SSH commands work in WSL after installing the OpenSSH Server.
>
> ```bash
> sudo apt update
> sudo apt install openssh-server
> sudo service ssh start
> ```

---

# Example 1 – Check SSH Version

## ✅ Practical Example

Check the installed SSH client version.

### ✅ Command

```bash
ssh -V
```

### ✅ Command Explanation

- `ssh` → SSH client
- `-V` → Display SSH version

### ✅ Expected Output

```text
OpenSSH_9.xp1 Ubuntu-3ubuntu0.x
```

(The exact version may differ.)

### ✅ Real-World Use Case

Before connecting to production servers, administrators verify that the SSH client is installed and supported.

### ✅ Screenshot Command

```bash
ssh -V
```

### ✅ Ubuntu

```bash
ssh -V
```

### ✅ CentOS

```bash
ssh -V
```

### ✅ WSL Note

Works directly if OpenSSH Client is installed.

---

# Example 2 – Check SSH Service Status

## ✅ Practical Example

Verify whether the SSH service is running.

### ✅ Ubuntu

```bash
systemctl status ssh
```

### ✅ CentOS

```bash
systemctl status sshd
```

### ✅ WSL

```bash
service ssh status
```

### ✅ Command Explanation

Displays:

- Running status
- Service PID
- Startup information

### ✅ Expected Output

```text
Active: active (running)
```

### ✅ Real-World Use Case

Always verify the SSH service before attempting remote login.

### ✅ Screenshot Command

**Ubuntu**

```bash
systemctl status ssh
```

**WSL**

```bash
service ssh status
```

---

# Example 3 – Start SSH Service

## ✅ Practical Example

Start the SSH server.

### ✅ Ubuntu

```bash
sudo systemctl start ssh
```

### ✅ CentOS

```bash
sudo systemctl start sshd
```

### ✅ WSL

```bash
sudo service ssh start
```

### ✅ Command Explanation

Starts the SSH daemon so it can accept incoming connections.

### ✅ Expected Output

Normally no output is displayed if the command succeeds.

Verify:

```bash
service ssh status
```

### ✅ Real-World Use Case

Required after installing OpenSSH Server or after stopping the service.

### ✅ Screenshot Command

```bash
sudo service ssh start
service ssh status
```

---

# Example 4 – Stop SSH Service

## ✅ Practical Example

Stop the SSH server.

### ✅ Ubuntu

```bash
sudo systemctl stop ssh
```

### ✅ CentOS

```bash
sudo systemctl stop sshd
```

### ✅ WSL

```bash
sudo service ssh stop
```

### ✅ Command Explanation

Stops the SSH daemon.

### ✅ Expected Output

Verify:

```bash
service ssh status
```

Output:

```text
inactive (dead)
```

### ✅ Real-World Use Case

Useful during maintenance or troubleshooting.

### ✅ Screenshot Command

```bash
sudo service ssh stop
service ssh status
```

> **⚠️ Note:** Do **not** stop SSH on a remote production server if you are connected through SSH, as it will disconnect your session.

---

# Example 5 – Restart SSH Service

## ✅ Practical Example

Restart SSH after configuration changes.

### ✅ Ubuntu

```bash
sudo systemctl restart ssh
```

### ✅ CentOS

```bash
sudo systemctl restart sshd
```

### ✅ WSL

```bash
sudo service ssh restart
```

### ✅ Command Explanation

Stops and starts the SSH service to apply configuration changes.

### ✅ Expected Output

Usually no output if successful.

Verify:

```bash
service ssh status
```

### ✅ Real-World Use Case

After editing `/etc/ssh/sshd_config`, restart SSH to apply new settings.

### ✅ Screenshot Command

```bash
sudo service ssh restart
service ssh status
```

---

# Example 6 – Connect to Localhost

## ✅ Practical Example

Connect to your own machine using SSH.

### ✅ Command

```bash
ssh localhost
```

or

```bash
ssh username@localhost
```

### ✅ Command Explanation

Creates an SSH connection to the local computer.

### ✅ Expected Output

First connection:

```text
Are you sure you want to continue connecting (yes/no)?
```

Type:

```text
yes
```

Then enter your password.

### ✅ Real-World Use Case

Useful for testing the SSH server before allowing remote access.

### ✅ Screenshot Command

```bash
ssh localhost
```

### ✅ Ubuntu

Works if the SSH server is running.

### ✅ CentOS

Works if `sshd` is active.

### ✅ WSL Note

Works after installing and starting OpenSSH Server.

---

# Example 7 – Connect to a Remote Server

## ✅ Practical Example

Connect to another Linux server.

### ✅ Command

```bash
ssh ubuntu@192.168.1.100
```

### ✅ Command Explanation

- `ubuntu` → Remote username
- `192.168.1.100` → Server IP address

### ✅ Expected Output

```text
ubuntu@192.168.1.100's password:
```

After authentication, you receive a remote shell prompt.

### ✅ Real-World Use Case

DevOps engineers use SSH to manage AWS EC2, Azure VMs, Google Compute Engine, and on-premises Linux servers.

### ✅ Screenshot Command

```bash
ssh ubuntu@192.168.1.100
```

---

# Example 8 – Generate an SSH Key Pair

## ✅ Practical Example

Create a public/private SSH key pair.

### ✅ Command

```bash
ssh-keygen
```

### ✅ Command Explanation

Creates:

- Private key
- Public key

Default location:

```text
~/.ssh/
```

### ✅ Expected Output

```text
Generating public/private rsa key pair...
```

Files created:

```text
id_rsa
id_rsa.pub
```

### ✅ Real-World Use Case

Used for passwordless authentication and GitHub access.

### ✅ Screenshot Command

```bash
ssh-keygen
ls ~/.ssh
```

---

# Example 9 – Copy SSH Key to a Server

## ✅ Practical Example

Copy your public key to a remote server.

### ✅ Command

```bash
ssh-copy-id ubuntu@192.168.1.100
```

### ✅ Command Explanation

Adds your public key to the remote server's:

```text
~/.ssh/authorized_keys
```

### ✅ Expected Output

```text
Number of key(s) added: 1
```

### ✅ Real-World Use Case

Enables secure passwordless login, commonly used in DevOps automation and CI/CD pipelines.

### ✅ Screenshot Command

```bash
ssh-copy-id ubuntu@192.168.1.100
```

> **Note:** If you don't have another Linux machine or VM, you may skip executing this command in WSL and simply document it in your notes.

---

# Example 10 – Verify SSH Connection

## ✅ Practical Example

Confirm that SSH login works correctly.

### ✅ Command

```bash
ssh localhost
```

After login:

```bash
hostname
```

or

```bash
whoami
```

### ✅ Command Explanation

Checks whether an SSH session has been successfully established.

### ✅ Expected Output

Example:

```text
ubuntu
```

or

```text
DESKTOP-XXXX
```

### ✅ Real-World Use Case

System administrators verify connectivity after configuring SSH or deploying new servers.

### ✅ Screenshot Command

```bash
ssh localhost
hostname
whoami
exit
```

---

# Summary of Commands

| Example | Command |
|----------|---------|
| Check Version | `ssh -V` |
| Service Status | `service ssh status` / `systemctl status ssh` |
| Start Service | `sudo service ssh start` |
| Stop Service | `sudo service ssh stop` |
| Restart Service | `sudo service ssh restart` |
| Local Connection | `ssh localhost` |
| Remote Connection | `ssh user@server` |
| Generate Keys | `ssh-keygen` |
| Copy Keys | `ssh-copy-id user@server` |
| Verify Login | `ssh localhost` |

> **Interview Tip:** For your GitHub repository, you can perform and capture screenshots for Examples **1, 2, 3, 5, 6, 8, and 10** directly in WSL. Examples **7** and **9** require another Linux machine or cloud VM (such as AWS EC2), so it's acceptable to document them without screenshots if you don't have a remote server available.

---

