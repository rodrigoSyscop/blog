---
title: "05 Configure SSH Servers and Clients"
date: 2019-04-01T10:21:10-03:00
draft: true
---

Secure Shell is the de facto standard by which Linux Administrators connect to servers all over the world. In this lesson, we'll take a closer look at some of the configuration options on SSH, as well as go through the process of generating a key with keygen and distributing it with ssh-copy-id to allow users to log in securely without a password. After this lesson, you should feel comfortable doing the same.

Configurações do servidor SSH em `/etc/ssh/sshd_config`.

```bash
# cria um novo par de chaves ssh
ssh-keygen

# copia chave pública para usere em remote-host
ssh-copy-id user@remote-host
```


```
cat ~/.ssh/id_rsa.pub | ssh user@remote-host "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"
```