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

# Part 7.2B – Advanced Practical Examples (Examples 11–20)

This section covers advanced SSH examples commonly used by **Linux Administrators, DevOps Engineers, Cloud Engineers, AWS Engineers, and System Administrators**.

> **Important**
>
> Some examples modify SSH configuration. If you are using **WSL**, you can safely read and understand these commands, but only make configuration changes if you know how to recover them. For production servers, always keep a backup of `sshd_config` before editing.

---

# Example 11 – Connect Using a Custom Port

## ✅ Practical Example

Connect to an SSH server running on a non-default port.

### ✅ Command

```bash
ssh -p 2222 ubuntu@192.168.1.100
```

### ✅ Command Explanation

- `ssh` → SSH client
- `-p` → Specify port number
- `2222` → Custom SSH port
- `ubuntu` → Username
- `192.168.1.100` → Remote server IP

### ✅ Expected Output

```text
ubuntu@192.168.1.100's password:
```

or, if key authentication is configured:

```text
Welcome to Ubuntu...
```

### ✅ Real-World Use Case

Many organizations change SSH from **Port 22** to another port (for example, **2222**) to reduce automated scanning and unauthorized login attempts.

### ✅ Screenshot Command

```bash
ssh -p 2222 ubuntu@192.168.1.100
```

---

# Example 12 – Use Verbose Mode (ssh -v)

## ✅ Practical Example

Display detailed SSH connection information.

### ✅ Command

```bash
ssh -v localhost
```

or

```bash
ssh -v ubuntu@192.168.1.100
```

### ✅ Command Explanation

The `-v` option enables **verbose mode**, showing:

- Connection process
- Key exchange
- Authentication steps
- Errors
- Debug information

### ✅ Expected Output

```text
OpenSSH_9.x
debug1: Connecting to...
debug1: Authentication succeeded.
```

### ✅ Real-World Use Case

Useful for troubleshooting authentication failures and connection problems.

### ✅ Screenshot Command

```bash
ssh -v localhost
```

---

# Example 13 – Passwordless Authentication

## ✅ Practical Example

Log in without entering a password.

### ✅ Command

Generate a key pair:

```bash
ssh-keygen
```

Copy the key:

```bash
ssh-copy-id ubuntu@192.168.1.100
```

Login:

```bash
ssh ubuntu@192.168.1.100
```

### ✅ Command Explanation

SSH authenticates using the private/public key pair instead of a password.

### ✅ Expected Output

```text
Welcome to Ubuntu...
```

(No password prompt.)

### ✅ Real-World Use Case

Commonly used in:

- DevOps automation
- CI/CD pipelines
- Jenkins
- Ansible
- GitHub Actions

### ✅ Screenshot Command

```bash
ssh-keygen
ssh-copy-id ubuntu@192.168.1.100
```

---

# Example 14 – Edit `sshd_config`

## ✅ Practical Example

Modify the SSH server configuration.

### ✅ Command

```bash
sudo nano /etc/ssh/sshd_config
```

### ✅ Command Explanation

Opens the main SSH server configuration file.

Common settings include:

- Port
- PermitRootLogin
- PasswordAuthentication
- PubkeyAuthentication

### ✅ Expected Output

Configuration file opens in the editor.

### ✅ Real-World Use Case

Administrators customize SSH security settings.

### ✅ Screenshot Command

```bash
sudo nano /etc/ssh/sshd_config
```

> **Tip:** Take a screenshot after opening the file, but avoid saving changes unless you intend to modify the configuration.

---

# Example 15 – Restart SSH After Configuration Changes

## ✅ Practical Example

Restart the SSH service after editing the configuration.

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

Reloads the SSH server so configuration changes take effect.

### ✅ Expected Output

No output if the restart succeeds.

Verify:

```bash
service ssh status
```

### ✅ Real-World Use Case

Required after changing any setting in `sshd_config`.

### ✅ Screenshot Command

```bash
sudo service ssh restart
service ssh status
```

---

# Example 16 – Disable Root Login

## ✅ Practical Example

Prevent direct SSH login as the root user.

### ✅ Command

Open:

```bash
sudo nano /etc/ssh/sshd_config
```

Find:

```text
PermitRootLogin yes
```

Change to:

```text
PermitRootLogin no
```

Restart SSH:

```bash
sudo service ssh restart
```

### ✅ Command Explanation

Disables direct root access over SSH.

### ✅ Expected Output

Root login via SSH is denied.

### ✅ Real-World Use Case

A security best practice on production Linux servers.

### ✅ Screenshot Command

```bash
grep PermitRootLogin /etc/ssh/sshd_config
```

---

# Example 17 – Disable Password Authentication

## ✅ Practical Example

Allow only SSH key authentication.

### ✅ Command

Open:

```bash
sudo nano /etc/ssh/sshd_config
```

Find:

```text
PasswordAuthentication yes
```

Change to:

```text
PasswordAuthentication no
```

Restart:

```bash
sudo service ssh restart
```

### ✅ Command Explanation

Disables password-based logins.

Only users with valid SSH keys can log in.

### ✅ Expected Output

Password authentication is disabled.

### ✅ Real-World Use Case

Improves server security against brute-force attacks.

### ✅ Screenshot Command

```bash
grep PasswordAuthentication /etc/ssh/sshd_config
```

> **Warning:** Ensure key-based authentication is working before disabling passwords, otherwise you may lock yourself out of the server.

---

# Example 18 – Configure Key-Based Authentication

## ✅ Practical Example

Set up secure login using SSH keys.

### ✅ Command

Generate keys:

```bash
ssh-keygen
```

Copy public key:

```bash
ssh-copy-id ubuntu@192.168.1.100
```

Login:

```bash
ssh ubuntu@192.168.1.100
```

### ✅ Command Explanation

Copies the public key into:

```text
~/.ssh/authorized_keys
```

The server authenticates the client using the key pair.

### ✅ Expected Output

Passwordless login succeeds.

### ✅ Real-World Use Case

Standard authentication method in cloud environments such as AWS EC2.

### ✅ Screenshot Command

```bash
ls ~/.ssh
cat ~/.ssh/id_rsa.pub
```

---

# Example 19 – Transfer Files with SCP

## ✅ Practical Example

Copy a file securely to a remote server.

### ✅ Command

```bash
scp notes.txt ubuntu@192.168.1.100:/home/ubuntu
```

Copy a directory:

```bash
scp -r project ubuntu@192.168.1.100:/home/ubuntu
```

### ✅ Command Explanation

- `scp` → Secure Copy
- `-r` → Copy directories recursively

### ✅ Expected Output

The file is transferred successfully.

### ✅ Real-World Use Case

Used for deploying application files, scripts, configuration files, and backups.

### ✅ Screenshot Command

```bash
scp notes.txt ubuntu@192.168.1.100:/home/ubuntu
```

---

# Example 20 – Connect Using SFTP

## ✅ Practical Example

Start a secure file transfer session.

### ✅ Command

```bash
sftp ubuntu@192.168.1.100
```

Common SFTP commands:

```bash
ls
pwd
get file.txt
put file.txt
exit
```

### ✅ Command Explanation

SFTP provides encrypted file transfer using the SSH protocol.

### ✅ Expected Output

```text
Connected to 192.168.1.100
sftp>
```

### ✅ Real-World Use Case

Administrators securely upload website files, backups, and configuration files to remote Linux servers.

### ✅ Screenshot Command

```bash
sftp ubuntu@192.168.1.100
```

---

# Summary of Advanced Commands

| Example | Command |
|----------|---------|
| Custom Port | `ssh -p 2222 user@host` |
| Verbose Mode | `ssh -v user@host` |
| Passwordless Login | `ssh-keygen`, `ssh-copy-id` |
| Edit SSH Config | `sudo nano /etc/ssh/sshd_config` |
| Restart SSH | `sudo service ssh restart` |
| Disable Root Login | `PermitRootLogin no` |
| Disable Password Login | `PasswordAuthentication no` |
| Key Authentication | `ssh-copy-id user@host` |
| Secure Copy | `scp file user@host:/path` |
| Secure FTP | `sftp user@host` |

---

## 📸 GitHub Screenshot Recommendation

You can easily capture screenshots for these examples in **WSL**:

- ✅ Example 12 (`ssh -v localhost`)
- ✅ Example 14 (`nano /etc/ssh/sshd_config`)
- ✅ Example 15 (`service ssh restart`)
- ✅ Example 18 (`ssh-keygen`, `ls ~/.ssh`)

Examples **11, 13, 19, and 20** require a remote Linux server (such as an AWS EC2 instance, Virtual Machine, or another Linux system) for full practical execution.

---

# Part 7.3 – Practice Exercises

This section contains hands-on SSH practice exercises for **WSL Ubuntu, Ubuntu Server, CentOS/RHEL, Amazon Linux, AWS EC2, and DevOps environments**.

> **Prerequisites**
>
> Make sure OpenSSH is installed before starting the exercises.

---

# Install OpenSSH Server

## Ubuntu / WSL

```bash
sudo apt update
sudo apt install openssh-server
```

## CentOS / RHEL

```bash
sudo yum install openssh-server
```

or

```bash
sudo dnf install openssh-server
```

---

# Start SSH Service

## Ubuntu

```bash
sudo systemctl start ssh
```

## WSL

```bash
sudo service ssh start
```

## CentOS

```bash
sudo systemctl start sshd
```

---

# Practice Exercise 1 – Verify SSH Version

## Objective

Check whether the SSH client is installed.

### Command

```bash
ssh -V
```

### Expected Output

```text
OpenSSH_9.x
```

---

# Practice Exercise 2 – Check SSH Service Status

## Objective

Verify whether the SSH service is running.

### Ubuntu

```bash
systemctl status ssh
```

### WSL

```bash
service ssh status
```

### CentOS

```bash
systemctl status sshd
```

---

# Practice Exercise 3 – Start SSH Service

## Objective

Start the SSH server.

### Ubuntu

```bash
sudo systemctl start ssh
```

### WSL

```bash
sudo service ssh start
```

### CentOS

```bash
sudo systemctl start sshd
```

Verify:

```bash
service ssh status
```

---

# Practice Exercise 4 – Restart SSH Service

## Objective

Restart SSH after configuration changes.

### Ubuntu

```bash
sudo systemctl restart ssh
```

### WSL

```bash
sudo service ssh restart
```

### CentOS

```bash
sudo systemctl restart sshd
```

---

# Practice Exercise 5 – Connect to Localhost

## Objective

Test the SSH server.

### Command

```bash
ssh localhost
```

After login:

```bash
whoami
```

Exit:

```bash
exit
```

---

# Practice Exercise 6 – Generate SSH Keys

## Objective

Create a public/private key pair.

### Command

```bash
ssh-keygen
```

Verify:

```bash
ls ~/.ssh
```

Expected files:

```text
id_rsa
id_rsa.pub
```

---

# Practice Exercise 7 – View Public Key

## Objective

Display the public key.

### Command

```bash
cat ~/.ssh/id_rsa.pub
```

---

# Practice Exercise 8 – Check Listening Port

## Objective

Verify that SSH is listening on Port 22.

### Command

```bash
ss -tlnp | grep :22
```

Alternative:

```bash
netstat -tlnp | grep :22
```

---

# Practice Exercise 9 – View SSH Configuration

## Objective

Open the SSH server configuration file.

### Command

```bash
sudo nano /etc/ssh/sshd_config
```

Do **not** modify the file unless required.

---

# Practice Exercise 10 – Check Verbose Connection

## Objective

View detailed connection information.

### Command

```bash
ssh -v localhost
```

Observe:

- Authentication
- Key exchange
- Connection details

---

# Practice Exercise 11 – View Known Hosts

## Objective

Display trusted SSH servers.

### Command

```bash
cat ~/.ssh/known_hosts
```

---

# Practice Exercise 12 – Verify SSH Process

## Objective

Verify that the SSH daemon is running.

### Command

```bash
ps aux | grep ssh
```

or

```bash
pgrep sshd
```

---

# WSL-Friendly Exercises

Practice these commands in WSL.

```bash
ssh -V
```

```bash
sudo service ssh status
```

```bash
sudo service ssh start
```

```bash
sudo service ssh restart
```

```bash
ssh localhost
```

```bash
ssh -v localhost
```

```bash
ssh-keygen
```

```bash
ls ~/.ssh
```

```bash
cat ~/.ssh/id_rsa.pub
```

```bash
ss -tlnp | grep :22
```

---

# Ubuntu Server Exercises

Practice:

```bash
systemctl status ssh
```

```bash
systemctl restart ssh
```

```bash
systemctl enable ssh
```

```bash
journalctl -u ssh
```

```bash
ssh localhost
```

---

# CentOS / RHEL Equivalents

| Ubuntu | CentOS / RHEL |
|----------|---------------|
| ssh | sshd |
| systemctl status ssh | systemctl status sshd |
| systemctl start ssh | systemctl start sshd |
| systemctl restart ssh | systemctl restart sshd |
| systemctl enable ssh | systemctl enable sshd |
| journalctl -u ssh | journalctl -u sshd |

---

# Screenshot Guide

Capture screenshots for the following commands.

## WSL

```bash
ssh -V
```

```bash
sudo service ssh status
```

```bash
sudo service ssh start
```

```bash
sudo service ssh restart
```

```bash
ssh localhost
```

```bash
ssh -v localhost
```

```bash
ssh-keygen
```

```bash
ls ~/.ssh
```

```bash
cat ~/.ssh/id_rsa.pub
```

```bash
ss -tlnp | grep :22
```

---

## Ubuntu Server

```bash
systemctl status ssh
```

```bash
systemctl restart ssh
```

```bash
journalctl -u ssh
```

---

## CentOS

```bash
systemctl status sshd
```

```bash
systemctl restart sshd
```

```bash
journalctl -u sshd
```

---

# Common Errors & Troubleshooting

---

## Error 1

```text
ssh: command not found
```

### Reason

OpenSSH Client is not installed.

### Solution

Ubuntu / WSL

```bash
sudo apt install openssh-client
```

CentOS

```bash
sudo yum install openssh-clients
```

---

## Error 2

```text
ssh: connect to host localhost port 22: Connection refused
```

### Reason

SSH service is not running.

### Solution

WSL

```bash
sudo service ssh start
```

Ubuntu

```bash
sudo systemctl start ssh
```

CentOS

```bash
sudo systemctl start sshd
```

---

## Error 3

```text
Permission denied (publickey,password)
```

### Reason

- Wrong username
- Incorrect password
- SSH key not configured
- Public key missing from `authorized_keys`

### Solution

Verify:

```bash
ssh-keygen
```

```bash
ssh-copy-id user@server
```

---

## Error 4

```text
Host key verification failed
```

### Reason

The server's host key has changed.

### Solution

Remove the old key:

```bash
ssh-keygen -R hostname
```

Reconnect.

---

## Error 5

```text
System has not been booted with systemd
```

### Reason

WSL without systemd.

### Solution

Use:

```bash
service ssh status
```

instead of

```bash
systemctl status ssh
```

---

## Error 6

```text
Connection timed out
```

### Reason

- Wrong IP address
- Firewall blocking Port 22
- SSH service stopped
- Network issue

### Solution

Check:

```bash
ping server-ip
```

```bash
ss -tlnp | grep :22
```

---

# Best Practices

- Always use **SSH instead of Telnet**.
- Prefer **SSH key authentication** over passwords.
- Keep your **private key (`id_rsa`) secure**.
- Never share your private key.
- Disable root login on production servers.
- Disable password authentication after confirming key-based login works.
- Use strong passphrases for SSH keys.
- Restart SSH after configuration changes.
- Test configuration before logging out of a remote server.
- Back up `sshd_config` before editing.

---

# Cleanup Commands

Remove generated SSH keys (practice only):

```bash
rm -f ~/.ssh/id_rsa
```

```bash
rm -f ~/.ssh/id_rsa.pub
```

Remove known hosts:

```bash
rm -f ~/.ssh/known_hosts
```

Stop SSH service (optional):

### WSL

```bash
sudo service ssh stop
```

### Ubuntu

```bash
sudo systemctl stop ssh
```

### CentOS

```bash
sudo systemctl stop sshd
```

Verify cleanup:

```bash
ls ~/.ssh
```

```bash
service ssh status
```

---

# Quick Revision

## Most Important Commands

```bash
ssh -V
ssh localhost
ssh -v localhost
ssh-keygen
ssh-copy-id user@host
scp file.txt user@host:/home/user
sftp user@host
service ssh status
service ssh start
service ssh restart
systemctl status ssh
systemctl status sshd
ss -tlnp | grep :22
cat ~/.ssh/id_rsa.pub
```

---

# Practice Checklist

- ✅ Verify SSH version
- ✅ Start SSH service
- ✅ Check SSH status
- ✅ Restart SSH service
- ✅ Connect to localhost
- ✅ Generate SSH keys
- ✅ View public key
- ✅ Verify Port 22
- ✅ Open `sshd_config`
- ✅ Test verbose SSH connection

> **Interview Tip:** Interviewers often ask you to troubleshoot SSH issues. A strong answer is to check whether the SSH service is running, verify Port 22 is listening, confirm firewall rules, review `sshd_config`, and use `ssh -v` to diagnose authentication or connection problems.

---


# Part 7.4A – Interview Questions & Answers (1–15)

This section covers the most frequently asked **SSH interview questions** for **Linux Administration, DevOps, AWS, Cloud Computing, Technical Support, and System Administration** interviews.

---

# Interview Question 1

## ✅ Question

**What is SSH?**

### ✅ Professional Answer

**SSH (Secure Shell)** is a secure network protocol used to remotely connect to another computer over an encrypted connection.

It allows administrators to:

- Log in remotely
- Execute commands
- Transfer files securely
- Manage Linux servers

SSH encrypts all communication between the client and server, making it much more secure than older protocols like Telnet.

### ✅ Example

```bash
ssh ubuntu@192.168.1.100
```

This command connects securely to a remote Linux server.

---

# Interview Question 2

## ✅ Question

**What is the full form of SSH?**

### ✅ Professional Answer

SSH stands for:

> **Secure Shell**

It provides encrypted communication between an SSH client and an SSH server.

---

# Interview Question 3

## ✅ Question

**What is the difference between SSH and Telnet?**

### ✅ Professional Answer

SSH and Telnet are both remote login protocols, but SSH is secure while Telnet is not.

| SSH | Telnet |
|------|---------|
| Secure protocol | Insecure protocol |
| Encrypts all communication | Sends data in plain text |
| Uses Port 22 | Uses Port 23 |
| Supports key-based authentication | Password only |
| Recommended for production | Rarely used today |

### ✅ Example

SSH:

```bash
ssh user@server
```

Telnet:

```bash
telnet server 23
```

---

# Interview Question 4

## ✅ Question

**What is an SSH Client?**

### ✅ Professional Answer

An **SSH Client** is the application or computer that initiates an SSH connection to a remote server.

Common SSH clients include:

- OpenSSH
- PuTTY
- MobaXterm
- Windows PowerShell
- Linux Terminal

### ✅ Example

```bash
ssh ubuntu@192.168.1.100
```

The local machine running this command is the SSH client.

---

# Interview Question 5

## ✅ Question

**What is an SSH Server?**

### ✅ Professional Answer

An **SSH Server** is the remote system that accepts SSH connections.

It runs the **sshd (SSH daemon)** service, listens for incoming requests, authenticates users, and provides a secure shell session.

### ✅ Example

Ubuntu:

```bash
systemctl status ssh
```

CentOS:

```bash
systemctl status sshd
```

---

# Interview Question 6

## ✅ Question

**What is Port 22?**

### ✅ Professional Answer

**Port 22** is the default network port used by the SSH protocol.

When an SSH client connects to a remote server without specifying a port, it automatically uses Port 22.

### ✅ Example

```bash
ssh ubuntu@192.168.1.100
```

This connects using Port 22 by default.

Custom port:

```bash
ssh -p 2222 ubuntu@192.168.1.100
```

---

# Interview Question 7

## ✅ Question

**What is the `ssh` command?**

### ✅ Professional Answer

The `ssh` command is the Linux command-line utility used to establish a secure connection to a remote server.

It supports:

- Remote login
- Remote command execution
- SSH key authentication
- Secure tunneling

### ✅ Example

```bash
ssh user@server
```

---

# Interview Question 8

## ✅ Question

**What is `sshd`?**

### ✅ Professional Answer

`sshd` (Secure Shell Daemon) is the background service that listens for incoming SSH connections.

It authenticates users and creates secure remote sessions.

### ✅ Example

CentOS:

```bash
systemctl status sshd
```

Verify the process:

```bash
ps aux | grep sshd
```

---

# Interview Question 9

## ✅ Question

**What are SSH Keys?**

### ✅ Professional Answer

SSH keys are a pair of cryptographic keys used for secure authentication.

The key pair consists of:

- Private Key
- Public Key

SSH keys allow users to log in securely without entering a password.

### ✅ Example

Generate keys:

```bash
ssh-keygen
```

---

# Interview Question 10

## ✅ Question

**What is a Public Key?**

### ✅ Professional Answer

The **Public Key** is the part of the SSH key pair that can be safely shared.

It is copied to the remote server's:

```text
~/.ssh/authorized_keys
```

The server uses it to verify the identity of the client.

### ✅ Example

View the public key:

```bash
cat ~/.ssh/id_rsa.pub
```

---

# Interview Question 11

## ✅ Question

**What is a Private Key?**

### ✅ Professional Answer

The **Private Key** is the secret part of the SSH key pair.

It remains only on the client machine and is used to prove the user's identity.

The private key should **never** be shared.

### ✅ Example

Default private key:

```text
~/.ssh/id_rsa
```

---

# Interview Question 12

## ✅ Question

**How do you generate SSH keys?**

### ✅ Professional Answer

Use the `ssh-keygen` command to create a new public/private key pair.

### ✅ Example

```bash
ssh-keygen
```

Generated files:

```text
id_rsa
id_rsa.pub
```

---

# Interview Question 13

## ✅ Question

**Where are SSH keys stored in Linux?**

### ✅ Professional Answer

SSH keys are stored in the user's `.ssh` directory.

Common files include:

| File | Purpose |
|------|---------|
| `~/.ssh/id_rsa` | Private Key |
| `~/.ssh/id_rsa.pub` | Public Key |
| `~/.ssh/authorized_keys` | Authorized public keys |
| `~/.ssh/known_hosts` | Known server fingerprints |

### ✅ Example

```bash
ls ~/.ssh
```

---

# Interview Question 14

## ✅ Question

**How do you verify that the SSH service is running?**

### ✅ Professional Answer

The command depends on the Linux distribution.

**Ubuntu**

```bash
systemctl status ssh
```

**WSL**

```bash
service ssh status
```

**CentOS**

```bash
systemctl status sshd
```

A healthy service displays:

```text
Active: active (running)
```

---

# Interview Question 15

## ✅ Question

**Why is SSH important in DevOps and Cloud Computing?**

### ✅ Professional Answer

SSH is essential because it enables secure remote management of Linux servers.

It is widely used for:

- Managing AWS EC2 instances
- Deploying applications
- Running administrative commands
- Automating tasks with Ansible
- Accessing cloud virtual machines
- Secure file transfers
- Troubleshooting production servers

SSH provides encrypted communication, making it the standard protocol for Linux administration.

### ✅ Example

Connect to an AWS EC2 Ubuntu instance:

```bash
ssh -i mykey.pem ubuntu@54.210.120.50
```

This command securely connects to the EC2 server using an SSH private key.

---

# Quick Interview Tips

- Understand the difference between **SSH**, **SSH Client**, **SSH Server**, and **sshd**.
- Remember that **SSH uses Port 22** by default.
- Be able to explain the roles of the **public key** and **private key** in key-based authentication.
- Know common SSH commands such as `ssh`, `ssh-keygen`, `ssh-copy-id`, and `scp`.
- Be prepared to compare **SSH vs Telnet** and explain why SSH is preferred.
- Practice connecting to **localhost** in WSL and, if possible, to a remote server such as an AWS EC2 instance.

---

# Part 7.4B – Interview Questions & Answers (16–30)

This section contains **advanced SSH interview questions** frequently asked in **Linux Administration, DevOps, AWS Cloud, System Administration, Technical Support, and Cloud Engineer** interviews.

---

# Interview Question 16

## ✅ Question

**What is the difference between `ssh` and `sshd`?**

### ✅ Professional Answer

| ssh | sshd |
|------|-------|
| SSH Client | SSH Server Daemon |
| Initiates connection | Accepts connection |
| Used by users | Runs on server |
| Executed manually | Runs as a background service |

### ✅ Example

Client:

```bash
ssh ubuntu@192.168.1.100
```

Server:

```bash
systemctl status sshd
```

---

# Interview Question 17

## ✅ Question

**What is passwordless SSH authentication?**

### ✅ Professional Answer

Passwordless authentication uses an **SSH key pair** instead of a password.

The client keeps the **private key**, while the server stores the **public key** inside:

```text
~/.ssh/authorized_keys
```

This is more secure and is commonly used in automation.

### ✅ Example

```bash
ssh-keygen
ssh-copy-id ubuntu@server
```

---

# Interview Question 18

## ✅ Question

**What is the purpose of `authorized_keys`?**

### ✅ Professional Answer

`authorized_keys` contains the public keys that are allowed to log in to the server.

If the client's public key matches one in this file, SSH grants access.

### ✅ Example

```bash
cat ~/.ssh/authorized_keys
```

---

# Interview Question 19

## ✅ Question

**What is `known_hosts`?**

### ✅ Professional Answer

`known_hosts` stores fingerprints of SSH servers that the client has connected to previously.

It helps detect server identity changes and protects against **man-in-the-middle attacks**.

### ✅ Example

```bash
cat ~/.ssh/known_hosts
```

---

# Interview Question 20

## ✅ Question

**What is the default SSH configuration file?**

### ✅ Professional Answer

Server configuration:

```text
/etc/ssh/sshd_config
```

Client configuration:

```text
/etc/ssh/ssh_config
```

User-specific client configuration:

```text
~/.ssh/config
```

---

# Interview Question 21

## ✅ Question

**How do you change the default SSH port?**

### ✅ Professional Answer

Edit:

```bash
sudo nano /etc/ssh/sshd_config
```

Change:

```text
Port 22
```

to

```text
Port 2222
```

Restart SSH:

Ubuntu

```bash
sudo systemctl restart ssh
```

WSL

```bash
sudo service ssh restart
```

CentOS

```bash
sudo systemctl restart sshd
```

---

# Interview Question 22

## ✅ Question

**Why should root login be disabled?**

### ✅ Professional Answer

Direct root login increases security risks because attackers often target the root account.

A better approach is:

- Login using a normal user.
- Use `sudo` when administrative privileges are required.

### ✅ Example

```text
PermitRootLogin no
```

---

# Interview Question 23

## ✅ Question

**Why is key-based authentication more secure than passwords?**

### ✅ Professional Answer

SSH keys use cryptographic authentication, making them much harder to compromise than passwords.

Advantages include:

- Strong encryption
- Resistant to brute-force attacks
- Suitable for automation
- Eliminates password reuse

---

# Interview Question 24

## ✅ Question

**How do you troubleshoot SSH connection problems?**

### ✅ Professional Answer

Common troubleshooting steps:

1. Check the SSH service status.
2. Verify Port 22 (or the configured port) is listening.
3. Confirm firewall rules.
4. Verify IP address and hostname.
5. Use verbose mode.
6. Review SSH logs.

### ✅ Example

```bash
ssh -v user@server
```

---

# Interview Question 25

## ✅ Question

**How do you verify that SSH is listening on Port 22?**

### ✅ Professional Answer

Use:

```bash
ss -tlnp | grep :22
```

Alternative:

```bash
netstat -tlnp | grep :22
```

Expected Output:

```text
LISTEN 0 128 *:22 *:*
```

---

# Interview Question 26

## ✅ Question

**What is SCP?**

### ✅ Professional Answer

**SCP (Secure Copy Protocol)** is used to securely transfer files between systems using SSH.

### ✅ Example

```bash
scp file.txt ubuntu@server:/home/ubuntu
```

---

# Interview Question 27

## ✅ Question

**What is SFTP?**

### ✅ Professional Answer

**SFTP (SSH File Transfer Protocol)** is an interactive file transfer protocol that operates over SSH.

Unlike FTP, all communication is encrypted.

### ✅ Example

```bash
sftp ubuntu@server
```

---

# Interview Question 28

## ✅ Question

**Why is SSH important in AWS?**

### ✅ Professional Answer

SSH is the primary method for securely accessing Linux EC2 instances.

Common tasks include:

- Deploying applications
- Installing software
- Monitoring logs
- Managing services
- Troubleshooting

### ✅ Example

```bash
ssh -i mykey.pem ubuntu@54.x.x.x
```

---

# Interview Question 29

## ✅ Question

**Can SSH be used for automation?**

### ✅ Professional Answer

Yes.

SSH is widely used in:

- Ansible
- Jenkins
- GitHub Actions
- Shell Scripts
- CI/CD Pipelines

Passwordless authentication enables secure automation without manual password entry.

---

# Interview Question 30

## ✅ Question

**How would you secure an SSH server in a production environment?**

### ✅ Professional Answer

Best practices include:

- Disable root login.
- Use SSH keys instead of passwords.
- Disable password authentication after verifying key-based access.
- Change the default port if required by organizational policy.
- Keep OpenSSH updated.
- Limit user access with `AllowUsers` or `AllowGroups`.
- Enable logging and monitor login attempts.
- Restrict access using firewalls or security groups.
- Regularly audit SSH configuration.

---

# SSH vs Telnet Comparison

| Feature | SSH | Telnet |
|---------|-----|---------|
| Full Form | Secure Shell | Telecommunication Network |
| Security | Encrypted | Plain text |
| Default Port | 22 | 23 |
| Authentication | Password & SSH Keys | Password only |
| Encryption | Yes | No |
| File Transfer | SCP, SFTP | Not Supported |
| Production Ready | Yes | No |
| Cloud Support | Yes | Rarely Used |
| DevOps Usage | Standard | Obsolete |
| Recommended | ✅ Yes | ❌ No |

---

# SSH Cheat Sheet

| Command | Description |
|----------|-------------|
| `ssh user@host` | Connect to remote server |
| `ssh -p 2222 user@host` | Connect using custom port |
| `ssh -v user@host` | Verbose mode |
| `ssh -V` | Display SSH version |
| `ssh localhost` | Connect to local machine |
| `ssh-keygen` | Generate SSH key pair |
| `ssh-copy-id user@host` | Copy public key to server |
| `scp file user@host:/path` | Securely copy file |
| `scp -r dir user@host:/path` | Copy directory recursively |
| `sftp user@host` | Start SFTP session |
| `service ssh status` | Check SSH status (WSL) |
| `systemctl status ssh` | Check SSH status (Ubuntu) |
| `systemctl status sshd` | Check SSH status (CentOS) |
| `ss -tlnp \| grep :22` | Verify SSH listening port |
| `cat ~/.ssh/id_rsa.pub` | View public key |
| `cat ~/.ssh/authorized_keys` | View authorized keys |
| `cat ~/.ssh/known_hosts` | View known hosts |

---

# Summary

- SSH is the industry-standard protocol for secure remote access.
- It encrypts all communication between client and server.
- SSH uses **Port 22** by default.
- `ssh` is the client, while `sshd` is the server daemon.
- SSH keys provide secure, passwordless authentication.
- SCP and SFTP enable encrypted file transfers.
- SSH is essential for Linux Administration, AWS, DevOps, Cloud Computing, and System Administration.
- Understanding SSH configuration, authentication, and troubleshooting is a core skill for infrastructure engineers.

---

# Quick Revision Notes

## Remember These Commands

```bash
ssh user@host
ssh localhost
ssh -p 2222 user@host
ssh -v user@host
ssh -V
ssh-keygen
ssh-copy-id user@host
scp file.txt user@host:/path
scp -r project user@host:/path
sftp user@host
systemctl status ssh
systemctl status sshd
service ssh status
ss -tlnp | grep :22
cat ~/.ssh/id_rsa.pub
cat ~/.ssh/authorized_keys
cat ~/.ssh/known_hosts
```

## Remember These Files

```text
/etc/ssh/sshd_config
/etc/ssh/ssh_config
~/.ssh/id_rsa
~/.ssh/id_rsa.pub
~/.ssh/authorized_keys
~/.ssh/known_hosts
```

## Remember These Ports

| Service | Port |
|----------|------|
| SSH | 22 |
| Telnet | 23 |

---

# Interview Tips

### ✅ Explain concepts before commands.

For example, if asked **"What is SSH?"**, first explain that it is a secure protocol for remote administration, then give a command example.

---

### ✅ Use real-world examples.

Mention scenarios such as:

- Connecting to an AWS EC2 instance
- Managing Ubuntu or CentOS servers
- Deploying applications remotely
- Using Ansible or Jenkins for automation

---

### ✅ Know the difference between Ubuntu, CentOS, and WSL.

| Ubuntu | CentOS | WSL |
|----------|---------|-----|
| `systemctl status ssh` | `systemctl status sshd` | `service ssh status` |

---

### ✅ Demonstrate troubleshooting skills.

If SSH fails:

1. Check the service status.
2. Verify Port 22 is listening.
3. Test with `ssh -v`.
4. Check firewall rules.
5. Review `sshd_config`.
6. Examine SSH logs.

---

### ✅ Common Commands to Memorize

```bash
ssh
ssh-keygen
ssh-copy-id
scp
sftp
ssh -v
ssh -p
systemctl status ssh
systemctl status sshd
service ssh status
```

> **Pro Tip for Interviews:** If you mention that you've practiced SSH in **WSL** and also know the equivalent commands for **Ubuntu Server**, **CentOS/RHEL**, and **AWS EC2**, it demonstrates practical, cross-platform Linux administration skills.

---
