---
title: "08 Configure Manage and Diagnose Advanced File System Permissions"
date: 2019-04-01T21:42:26-03:00
draft: true
---

Standard file permissions don't always cover all the bases. For the edge and corner cases, there are advanced file permissions like the sticky bit, setgid, and setuid. In this lesson, we'll demonstrate using chmod to set these additional permissions, and even how to find files with those permissions set on them. After this lesson, you'll be able to make use of advanced file permissions on your system.

```bash
# stick-bit: only owners can remove their own files
chmod 1755 /mnt/data

# SGID bit: will create files and directorys with the same group owner of /mnt/data
chmod 2770 /mnt/data

# stick-bit + SGID
chmod 3770 /mnt/data

# SUID bit: run apps with the owner permission
chmod 4770 /mnt/data/app.sh

```