---
title: "09 Setup User and Group Disk Quotas for File Systems"
date: 2019-04-01T21:56:50-03:00
draft: true
---

Often, you'll need to limit the amount of disk space a certain user or group of users can make use of. In this lesson, we'll explore limiting particular users or groups in their usage of block storage using the Linux quota command. After this lesson, you'll be able to set hard and soft limits and set grace periods for users to clean up their files.

```bash
yum install -y quota
```

Add `quota` option to fstab
`/etc/fstab`:
```
/dev/xvdf1  /mnt/data   ext4    defaults,quota 0 0 
```

```bash
mount -o remount /mnt/data

quotacheck -cugm /mnt/data
edquota user
```

in kilobytes?
```
filesystem      blocks  soft    hard    inodes  soft    hard
/dev/xvdf1      24      0       0       8       0       0   
```

```bash
# report quota usage
repquota -a

# time in grace period
edquota -t
```

