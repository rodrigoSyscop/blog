---
title: "05 Configure and Manage Swap Space"
date: 2019-04-01T21:14:48-03:00
draft: true
---

Swap space is used when the kernel needs more RAM, but there is no more RAM. It "swaps" pages of memory out to disk in either a swap file or swap partition. In this lesson, we'll discuss more about what swap is, how much you need, how to turn it off and on (swapon and swapoff -- SURPRISE!) , and where and how it's defined. After this lesson, you should be able to create your own swap files and partitions and turn them on or off again as needed.

```
# swapfile
dd if=/dev/zero of=/root/extraswap.swp bs=1M count=512
chmod 0600 /root/extraswap.swp
mkswap /root/extraswap.swp

# swap disk
mkswap /dev/xvdf1

# put in /etc/fstab
/root/extraswap.swp     none    swap   defaults     0 0
/dev/xvdf1              none    swap   defaults     0 0

swapon -a
```