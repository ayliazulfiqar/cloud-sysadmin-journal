# Day 1 – Ubuntu Server Setup and User Management

## 1. Objective

The goal of Day 1 was to install Ubuntu Server 24.04 LTS inside VirtualBox and learn basic Linux administration, including user creation, groups, and sudo privileges.

## 2. Virtual Machine Setup

- Host OS: Linux Mint
- Guest OS: Ubuntu Server 24.04 LTS
- Virtualization software: Oracle VirtualBox
- CPU: 2 cores
- RAM: 2 GB
- Disk: 20 GB
- Network: NAT
- OpenSSH Server: Installed

## 3. Initial System Inspection

I used the following commands to understand my server:

| Command | Purpose |
|---|---|
| `hostnamectl` | Displays system and hostname information. |
| `ip a` | Displays network interfaces and IP addresses. |
| `df -h` | Shows available and used disk space. |
| `free -h` | Displays memory usage. |
| `uname -a` | Displays kernel and system information. |

## 4. Updating Ubuntu

Command:

```bash
sudo apt update && sudo apt upgrade -y
```

What I learned:

- `apt update` refreshes the package lists.
- `apt upgrade` installs available package updates.
- `sudo` allows authorized users to execute administrative commands.
- `-y` automatically confirms the installation prompts.

## 5. User Management

I learned how to create and delete Linux users.

Commands used:

```bash
sudo adduser alice
sudo adduser bob
```

To delete users and their home directories:

```bash
sudo deluser --remove-home alice
sudo deluser --remove-home bob
```

I recreated the accounts after forgetting Alice's password.

## 6. Groups and Sudo Privileges

I gave Alice administrator privileges using:

```bash
sudo usermod -aG sudo alice
```

I checked user information using:

```bash
id alice
id bob
groups alice
groups bob
```

What I learned:

- Alice belongs to the sudo group.
- Bob is a regular user.
- Alice can execute authorized administrator commands.
- Bob cannot execute sudo commands by default.

## 7. Testing User Permissions

I switched between accounts using:

```bash
su - alice
su - bob
```

I checked the current username using:

```bash
whoami
```

I tested administrator privileges using:

```bash
sudo whoami
```

Expected results:

- Alice: `root`
- Bob: sudo permission denied.

## 8. What I Learned

1. How to install Ubuntu Server in VirtualBox.
2. How to inspect Linux system resources.
3. How to update Ubuntu packages.
4. How to create and delete Linux users.
5. How Linux groups work.
6. How to grant sudo privileges.
7. How to switch between users.
8. How to test administrator permissions.

## 9. Things That Confused Me

- When entering passwords in the Linux terminal, nothing appears on the screen.
- I initially forgot Alice's password and had to recreate the account.
- I learned that being a regular Linux user is different from having sudo privileges.
- I am still learning how Linux user IDs, group IDs, and permissions work.

## 10. Day 1 Completion

Day 1 introduced me to Ubuntu Server installation and basic Linux user administration.

Next topic: Day 2 – Linux File Permissions and Ownership.
