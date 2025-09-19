# NFS File Sharing between servers
Redhat/Centos/Rocky-types

Install Software
```
sudo yum install nfs-utils
```

## Server
Configure share:
```
sudo mkdir -p /nfs/files
sudo chown nobody:nobody /nfs/files
sudo chmod 777 /nfs/files
```

Edit /etc/exports:
```
/nfs/files *{nfs,sync,no_subtree_check}(sync)
```

Restart service:
```
sudo exportfs -a
sudo systemctl restart nfs-server
```

## Client
Create local mount for share:
```
sudo mkdir /var/nfs-files
```

Mount:
```
sudo mount -t nfs 192.168.168.168:/nfs/files /var/nfs-files
```

/etc/fstab entry:
```
192.168.168.168:/nfs/files /var/nfs-files /var/nfs-files nfs defaults 0 0
```

## Firewall stuff
```
sudo firewall-cmd --add-service nfs --permanent # If using firewalld
sudo firewall-cmd --reload # If using firewalld
```
