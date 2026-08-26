# 27. NFS & autofs — Bonus

## 27.1 NFS Server

```bash
dnf install nfs-utils         # or: apt install nfs-kernel-server
```

**Export config** — `/etc/exports`:
```
/path/to/share   192.168.1.0/24(rw,sync,no_root_squash)
```

```bash
exportfs -ra                  # Re-export all shares after editing /etc/exports
systemctl enable --now nfs-server
```

## 27.2 NFS Client

```bash
showmount -e server_ip        # List a server's available exports
mount -t nfs server_ip:/path /mnt      # Mount manually
```

**Persistent mount** — `/etc/fstab`:
```
server_ip:/path   /mnt   nfs   defaults   0   0
```

## 27.3 autofs (On-Demand Automounting)

- Mounts a share automatically the moment it's accessed, and unmounts it after a period of inactivity.

`/etc/auto.master`:
```
/mnt/nfs   /etc/auto.nfs
```

`/etc/auto.nfs` (the map file):
```
data   -rw,soft   server_ip:/path/to/share
```

```bash
systemctl enable --now autofs
```
