---
title: "10 Restrict Access to a Web Page"
date: 2019-04-01T15:10:39-03:00
draft: true
---

```
<Directory /var/www/html/test/>
    Order allow,deny
    Allow from 127.0.0.0/8
    Allow from 10.0.0.0/8
    Allow from 172.16.0.0/12
    Allow from 192.168.0.0/16
    Allow from ::1
    Deny from all
</Directory>
```