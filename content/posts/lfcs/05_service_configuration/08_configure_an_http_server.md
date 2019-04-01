---
title: "08 Configure an HTTP Server"
date: 2019-04-01T12:42:26-03:00
draft: true
---

There's this little fad called the web, and even though it's all likely to blow over in a few more months, we'll join in the hoopla and say that installing and configuring a web server is still considered a rite of passage to many, and you're about to see it done. In this lesson, we'll demonstrate installing and setting up Apache2 on RHEL and CentOS systems. After this lesson, you'll have the know-how to install your own web server on CentOS and RHEL systems, and you should use it.

```bash
yum install -y httpd lynx
systemctl enable httpd
systemctl start httpd
```

`/etc/httpd/conf/httpd.conf`:
```
# at the end
IncludeOptional vhosts.d/*.conf
```

```bash
mkdir -p /etc/httpd/vhosts.d
```
