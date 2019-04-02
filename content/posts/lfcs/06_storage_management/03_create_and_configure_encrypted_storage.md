---
title: "03 Create and Configure Encrypted Storage"
date: 2019-04-01T20:50:39-03:00
draft: true
---

Protecting your data can be a huge challenge. Configuring an entire drive can be helpful in situations where you need open access to data periodically, but need to be able to lock and unlock the data at will. In this lesson, we create encrypted storage using cryptsetup, and Chad seriously opens up his typing skills to worldwide ridicule. After this lesson, you will feel AMAZING about your own typing skills, and will be able to use them to set up an encrypted partition using cryptsetup.

```bash
grep -i dm_crypt /boot/config-$(uname -r)
# CONFIG_DM_CRYPT=m
yum install -y cryptsetup

cryptsetup -y luksFormat /dev/xvdf1
cryptsetup luksOpen /dev/xvdf1 xvdf1-crypted

mkfs -t ext4 /dev/mapper/xvdf1-crypted
mkdir -p /mnt/encrypted-storage
mount /dev/mapper/xvdf1-crypted /mnt/encrypted-storage

umount /mnt/encrypted-storage
cyptsetup luksClose xvdf1-crypted
```