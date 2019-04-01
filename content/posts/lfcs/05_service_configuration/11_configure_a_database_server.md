---
title: "11 Configure a Database Server"
date: 2019-04-01T15:47:47-03:00
draft: true
---

When developers want to persist information, they'll usually ask for a database server. There are many to choose from with a variety of different features and niches, but the most popular would probably come down to a race between MySQL and MariaDB, which is good because MariaDB is a direct drop-in replacement for MySQL. In this lesson, we'll talk a little bit about some of the database servers available out there, and specifically install and configure MariaDB. We'll also take a brief look at the MySQL console, and explore one of MariaDB's biggest gotchas.
Note: systemctl can now be used to enable and start MariaDB. https://mariadb.com/kb/en/library/systemd/

```bash

yum install mariadb-server mariadb
# apt-get install mariadb-server mariadb-client

mysql_secure_installation

systemctl enable mariadb
systemctl start mariadb
```