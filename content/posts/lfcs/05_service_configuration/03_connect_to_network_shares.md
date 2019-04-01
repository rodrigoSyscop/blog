---
title: "03 Connect To Network Shares"
date: 2019-04-01T01:11:23-03:00
draft: true
---

## No servidor NFS

```bash
# instalar pacotes
yum install -y nfs-utils
# criar a pasta a compartilhar e dar permissões
mkdir /share
chmod -R 755 /share
chown -R nfsnobody.nfsnobody /share

# levantar serviços
systemctl enable rpcbind
systemctl enable nfs-server
systemctl enable nfs-idmap

systemctl start rpcbind
systemctl start nfs-server
systemctl start nfs-idmap

```

`/etc/exports`:
```
/shares     10.0.0.0/0,172.16.0.0/12,192.168.0.0/16(rw,sync,no_root_squash,no_all_squash)
```

```bash
systemctl restart nfs-server
```

## No cliente NFS

```bash
# instalar pacotes
yum install -y nfs-utils

# criar ponto de montagem
mkdir -p /mnt/nfsshare

# montar e verificar
mount -t nfs 172.16.0.10:/share /mnt/nfsshare
df -h /mnt/nfsshare
```
