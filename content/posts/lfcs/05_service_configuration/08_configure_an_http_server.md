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
```
<VirtualHost *:80>
	ServerName www.transapi.com
	ServerAlias www
	DocumentRoot /var/www/html/transapi
	#ErrorLog /var/www/html/transapi/logs/error.log
	#CustomLog /var/www/html/transapi/logs/access.log combined
</VirtualHost>
```

```bash
yum install -y mod_ssl
openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/certs/transapi.key -out /etc/ssl/certs/transapi.crt
```

```
<VirtualHost *:443>
	ServerName www.transapi.com
	ServerAlias www
    SSLEngine on
    SSLCertificateFile /etc/ssl/certs/transapi.crt
    SSLCertificateKeyFile /etc/ssl/certs/transapi.key
	DocumentRoot /var/www/html/transapi
	#ErrorLog /var/www/html/transapi/logs/error.log
	#CustomLog /var/www/html/transapi/logs/access.log combined
</VirtualHost>