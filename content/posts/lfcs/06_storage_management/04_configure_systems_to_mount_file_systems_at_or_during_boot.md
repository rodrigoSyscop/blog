---
title: "04 Configure Systems to Mount File Fystems at or During Boot"
date: 2019-04-01T21:04:44-03:00
draft: true
---

That file system isn't going to mount itself! This isn't Windows! File systems in Linux require intelligent, thoughtful, and responsible administrators to carefully consider which file systems should be available at boot and edit the fstab to reflect their wishes. In this lesson, we'll examine the /etc/fstab file, and we'll see how it's used to mount file systems at boot time. After this lesson, you'll be familiar with the format of the /etc/fstab file yourself and can finally mount that USB drive on your keychain. Or that SCSI disk. Or really, whatever you've got.

`/etc/fstab`:
```
UUID="asdfasdf-asdf-asdf-asdf-asdfasdf" /mnt/ext4 ext3 default 0 2
UUID="asdfasdf-asdf-asdf-asdf-asdfasdf" /mnt/btrfs btrfs default 0 2
```