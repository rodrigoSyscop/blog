---
title: "01 List Create Delete and Modify Physical Storage Partitions "
date: 2019-04-01T20:16:54-03:00
draft: true
---

The first step in provisioning block storage is usually to partition it. In this lesson, we'll demonstrate the proper use of fdisk and parted to partition hard drive space. After this lesson, you should feel comfortable repartitioning block storage devices, but remember to always have a backup.

```bash
# list block devices
lsblk

# 
fdisk /dev/xvdf
# p - print partition table
# m - show help menu

gparted
```