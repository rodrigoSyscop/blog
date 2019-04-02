---
title: "06 Create and Manage RAID Devices"
date: 2019-04-01T21:18:54-03:00
draft: true
---

RAID (Redundant Array of Independent Disks) is a great way to not just present a single device from multiple devices, but also a way to use that storage space to guarantee file durability. In this lesson, we'll take a closer look at putting multiple physical devices together into a software RAID array using mdadm. Perfect for when you need one big device instead of the several smaller ones you have, or when you'd like some extra insurance against drive failure. After this lesson, you will be able to use mdadm, fdisk, and mkfs to create your own arrays for redundancy or device aggregation.

```bash
fdisk /dev/xvdf1
# t: fd
fdisk /dev/xvdf2
# t: fd

yum install -y mdadm

mdadm --create --verbose /dev/md0 --level=stripe --raid-devices=2 /dev/xvdf1 /dev/xvdf2
cat /proc/mdstat

mdadm --detail /dev/md0

mkfs -t ext4 /dev/md0


mdadm --detail --scan
# put the output of this command into /etc/mdadm/mdadm.conf

mdadm --assemble --scan
systemctl enable mdadm

vim /etc/sysconfig/mdadm
AUTOSTART=true

mdmonitor

mdadm /dev/md0 --add /dev/xvdf3
```