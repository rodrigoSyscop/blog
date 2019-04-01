---
title: "02 Maintain a DNS Zone"
date: 2019-04-01T00:59:22-03:00
draft: true
---

Criando uma nova zona do zero:

No `named.conf` podemos ver que o diretório padrão é o `/var/lib/named` em options {}. Basta referenciar nossa nova zona no final do arquivo `named.conf`.

`/etc/named.conf`:
```
zone "operacionalti.com" in {
    type master;
    file "operacionalti.com.zone";
};
```

em seguida criar o arquivo de zona.

`/var/lib/named/operacionalti.com.zone`:
```
$ORIGIN operacionalti.com
$TTL 600

@       IN      SOA     dns1.operacionalti.com. mail.operacionalti.com. (
        2019033101  ; serial
        6H          ; refresh
        1H          ; retry
        1W          ; expiry
        1D          ; minimum TTL
);

www     IN      A       172.16.0.80
ftp     IN      A       172.16.0.21
mail    IN      A       172.16.0.25
mail2   IN      A       172.16.1.25
dns1    IN      A       172.16.0.53
dns2    IN      A       172.16.1.53

smtp    IN      CNAME   mail
pop     IN      CNAME   mail
imap    IN      CNAME   mail

        IN      MX 10   mail
        IN      MX 20   mail2

        IN      NS      dns1.operacionalti.com
        IN      NS      dns2.operacionalti.com
```

TODO: comando para verificar um arquivo de zona.