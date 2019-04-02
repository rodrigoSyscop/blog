---
title: "10 Create and Configure Filesystems"
date: 2019-04-01T22:03:38-03:00
draft: true
---

File systems lay at the very heart of Linux. "Everything in Linux is a file." And file systems control it all. In this lesson, we'll create two different file systems on the same hard drive (but different partitions) using fdisk and mkfs and then mount them on the host machine using mount.

```bash
mkfs -t ext4 /dev/xvdf1 
```