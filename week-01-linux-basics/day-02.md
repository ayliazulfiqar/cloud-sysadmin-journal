# Day 2 – Linux Permissions and Ownership

## 1. Objective

The goal of Day 2 was to understand Linux file permissions, ownership, groups, and shared directory access.

I practised using chmod, chown, umask, and setgid to control access to files and directories.

## 2. Understanding Linux Permissions

Linux uses three permission categories:

- User (owner)
- Group
- Others

The three main permissions are:

- r = Read (4)
- w = Write (2)
- x = Execute (1)

Examples:

| Permission | Meaning |
|---|---|
| 755 | Owner has full access; group and others can read and execute. |
| 644 | Owner can read/write; group and others can read. |
| 640 | Owner can read/write; group can read; others have no access. |
| 600 | Only the owner can read/write. |
| 770 | Owner and group have full access; others have no access. |

## 3. Practice with chmod

Commands used:

```bash
mkdir ~/perm-lab
cd ~/perm-lab
touch file.txt
ls -l file.txt
```

Changed permissions:

```bash
chmod 600 file.txt
chmod u+x,g+r file.txt
chmod 755 file.txt
```

What I learned:

- chmod changes file and directory permissions.
- Numeric permissions use values 4, 2, and 1.
- Symbolic permissions use letters such as u, g, o, r, w, and x.

## 4. Understanding chown

Command used:

```bash
sudo chown alice:alice file.txt
```

What I learned:

- chown changes file ownership.
- Alice becomes the file owner.
- Alice becomes the file's group.

I verified ownership using:

```bash
ls -l file.txt
```

## 5. Creating a Shared Folder

Created a third user:

```bash
sudo adduser carol
```

Created a development group:

```bash
sudo groupadd devteam
```

Added Alice and Bob to the group:

```bash
sudo usermod -aG devteam alice
sudo usermod -aG devteam bob
```

Created the shared directory:

```bash
sudo mkdir /srv/shared
```

Changed ownership:

```bash
sudo chown root:devteam /srv/shared
```

Set directory permissions:

```bash
sudo chmod 2770 /srv/shared
```

What I learned:

- Groups allow multiple users to share access.
- The setgid bit makes new files and directories inherit the parent directory's group.
- The permission 2770 gives the owner and group full access while denying access to others.

## 6. Testing Shared Folder Access

Alice created a file:

```bash
su - alice
touch /srv/shared/alice.txt
ls -l /srv/shared
exit
```

Bob attempted to modify Alice's file:

```bash
su - bob
echo "hello from bob" >> /srv/shared/alice.txt
exit
```

If Bob received Permission denied, I learned that group membership alone does not guarantee write access to an existing file.

I corrected the permissions using:

```bash
sudo chmod g+w /srv/shared/alice.txt
```

Carol tested access:

```bash
su - carol
ls /srv/shared
exit
```

Expected result: Permission denied.

## 7. Understanding umask

Commands used:

```bash
umask
umask 002
touch test2.txt
ls -l test2.txt
```

What I learned:

- umask controls which permissions are removed from newly created files and directories.
- A common default umask is 022.
- A umask of 002 allows group write permissions on newly created files and directories, subject to their creation defaults.
- umask 002 is useful for shared working environments.

## 8. Bonus: Sticky Bit

The sticky bit helps prevent users from deleting files belonging to other users in shared directories.

Example:

```bash
ls -ld /tmp
```

The final `t` in the permissions indicates that the sticky bit is enabled.

It can be enabled with:

```bash
sudo chmod +t directory
```

## 9. What I Learned

1. How to read Linux file permissions.
2. How numeric permissions such as 755, 644, and 600 work.
3. How to change permissions using chmod.
4. How to change file ownership using chown.
5. How Linux groups work.
6. How to create a shared directory.
7. How the setgid bit works.
8. Why group write permission is important.
9. How umask controls default permissions.
10. What the sticky bit does.

## 10. Things I Found Confusing

- Understanding the difference between file permissions and directory permissions.
- Understanding why Bob could not initially write to Alice's file.
- Understanding the difference between setgid and group write permissions.
- Understanding how umask calculates default permissions.
- Understanding the difference between chmod and chown.

