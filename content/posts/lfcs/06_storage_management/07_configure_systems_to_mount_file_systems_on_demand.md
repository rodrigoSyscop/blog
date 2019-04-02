---
title: "07 Configure Systems to Mount File Systems on Demand"
date: 2019-04-01T21:31:52-03:00
draft: true
---

Linux can't really touch anything on disk until it's mounted up and ready. Never fear, though, we've got it covered. In this lesson, we'll show you how to use the mkdir command to create mount points and the mount and umount commands to mount and unmount devices, respectively. After this lesson, you'll be able to use the mount and umount commands, as well.

```bash
yum install -y samba-client samba-common cifs-utils

smbclient -I 192.168.0.123 -U user -L share

mkdir -p /mnt/samba

echo "username=user" > /mnt/.smbcredentials
echo "password=123" >> /mnt/.smbcredentials

```

`/etc/fstab`:
```
//192.168.0.123/share     /mnt/samba    cifs    credentials=/mnt/.smbcredentials,defaults 0 0
```

```bash
mount -a
df -h
```