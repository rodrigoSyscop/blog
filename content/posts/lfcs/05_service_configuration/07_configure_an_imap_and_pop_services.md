---
title: "07 Configure an IMAP and POP Services"
date: 2019-04-01T10:37:29-03:00
draft: true
---

But what if your boss won't PAY for Gmail?! Not to worry, Linux admins have been running email servers for a LONG TIME and have it down to a science. In this lesson, we'll demonstrate installing Dovecot and configuring it to be our IMAP and IMAPS service. Then, because everyone loves a challenge, we'll add Pop3 and Pop3S functionality just to show off. After this lesson, you'll be able to install Dovecot and set up your own email server, too!

Verificar o grupo do postfix
```
egrep "mail|postfix" /etc/group
ls -l /var/mail
```

```bash
yum install -y dovecot dovecot-pop3d dovecot-imapd
```

`/etc/dovecot/conf.d/10-mail.conf`:
```
# ...
mail_location = mbox:~/mail:INBOX=/var/mail/%u
# ...
mail_privileged_user = mail
```

`/etc/dovecot/conf.d/20-imap.conf` 
`/etc/dovecot/conf.d/20-pop3.conf`

## Certificados

`/etc/dovecot/mkcert.sh`

`/etc/dovecot/private/dovecot.pem`

`/etc/dovecot/conf.d/10-ssl.conf` deve apontar para o dovecot.pem

```
ssl = yes
ssl_cert = </etc/dovecot/dovecot.pem
ssl_key = </etc/dovecot/private/dovecot.pem
```

```bash
sudo systemctl restart dovecot

netstat -nptlu |grep dovecot
```

