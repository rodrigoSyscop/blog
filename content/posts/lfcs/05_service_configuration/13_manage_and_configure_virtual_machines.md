---
title: "13_manage_and_configure_virtual_machines"
date: 2019-04-01T16:13:15-03:00
draft: true
---

Long before containers, virtual machines were the Linux administrator's ace in the hole when it came to process isolation. Sure, they're a bit more resource heavy, but they're stable and have a lot of options when it comes to managing them. In this lesson, we'll take a look at creating, managing, and configuring virtual machines running on a Linux host using KVM and a variety of command line and graphical tools. After this lesson, you'll be able to use KVM related tools like vm-manager, vm-install, and virsh to create, manage, start, and stop your own virtual machines.

```bash
yum install -y qemu-kvm libvirt libvirt-client virt-install virt-viewer

# check for virtualization flags
grep "vmx|svm" /proc/cpuinfo

virt-install \
    --name=tinyalpine \
    --vcpus=1  \
    --memory=1024  \
    --disk size=5 \
    --cdrom=alpine-standard-3.7.0-x86.iso 

virsh list --all
virsh edit tinyalpine
virsh autostart tinyalpine
virsh autostart --disable tinyalpine

virt-manager
```