---
title: "02 Manage and Configure LVM Storage"
date: 2019-04-01T20:32:51-03:00
draft: true
---

Logical Volume Management allows you to join multiple physical disks together in such a way that the aggregated device is presented to the operating system as a single device. Think of it like Software RAID0. In this lesson, we'll show you how to partition your devices for Logical Volume Management, how to create the physical volumes (pv-create), set up the logical volumes (lv-create), and then create the volume groups(vg-create) to format(mkfs). We'll even show you how to expand the whole system once it's in place. Albeit with a teeny tiny disk. After this lesson, you'll be able to partition your own (hopefully larger) block devices, create the physical volumes, logical volumes, volume groups, and write file systems to the whole thing. You will also be able to add or remove physical devices from the array as needed.

```
yum install -y lvm2

# tag partitions with LVM type: 8e
fdisk /dev/xvdf
# t: 8e

# create the phisical volumes
pvcreate /dev/xvdf1
pvcreate /dev/xvdf2

# create de volume group
vgcreate tinydata /dev/xvdf1 /dev/xvdf2

# create a logical volume in the volume group
lvcreate --name logical-tiny1 --size 596M  tinydata

# list all logical volumes
lvdisplay
# /dev/tinydata/logical-tiny

# create a filesystem on top of the logical volume and mount it
mkfs -t ext3 /dev/tinydata/logical-tiny
mkdir -p /mnt/tinystorage
mount /dev/tinydata/logical-tiny /mnt/tinystorage

echo "some content" > /mnt/tinystorage/somefile.txt

pvscan
vgscan
lvscan

# expanding your logical volume
fdisk /dev/xvdf3
# t: 8e
pvcreate /dev/xvdf3

# add it to the volume group
vgextend tinydata /dev/xvdf3

# extend your logical volume
lvextend -L100% /dev/tinydata/logical-tiny

# resize the filesystem
e2fsck -f /dev/tinydata/logical-tiny
resize2fs /dev/tinydata/logical-tiny

# check it out
df -h 
```