---
title: "01 Configuring a Cache DNS Server"
date: 2019-04-01T00:43:30-03:00
draft: true
---

Um servidor DNS de cache é utilizado para realizar consultas de DNS para requisições que receber e manter a resposta em cache para consultas futuras.

```bash
yum install -y bind bind-utils
```

Configuração de do bind em modo cache:

`/etc/named.conf`:
```
options {
    # ...
    allow-query { localhost; localnets; }
    allow-query-cache { localhost; localnets; }
    # ...
}
```

Se o SELinux estiver ativo, temos que verificar se o `named.conf` e o `named.rfc1912.zones` possuem o label correto definido:

```bash
ls -lZ /etc/named.conf
# -rw-r-----. root named system_u:object_r:named_conf_t:s0 named.conf
# se necessário: 
# semanage fcontext -a -t named conf t  /etc/named.conf 
```

Verifica por erros de sintaxe:

```bash
named-checkconf /etc/named.conf
```

Executar o serviço, ativar no boot e verificar o status:

```bash
systemctl restart named
systemctl enable named
systemctl status named
```