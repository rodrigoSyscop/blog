---
title: "06 Restrict Access to Http Proxy Servers"
date: 2019-04-01T10:30:56-03:00
draft: true
---

Something about that guy -- I don't trust him. How do we keep him off of our HTTP proxy? Protecting the software that keeps your users safe (and following appropriate network policies) is a no-brainer. In this lesson, we'll look at configuring squid to deny access to particular networks and hosts. After this lesson, THAT guy will pose no threat to you, because you'll be able to configure squid to allow appropriate hosts only and deny others based on client host or network.

`/etc/squid/squid.conf`:
```
# ...
acl localhost src 10.0.0.0/8
acl localhost src 172.16.0.0/12
acl localhost src 192.168.0.0/16
acl nochad src 10.9.185.155

# permite o uso do proxy para
# todos os clientes em localnet
# mas nega para nochad
acl allow localnet !nochad
```