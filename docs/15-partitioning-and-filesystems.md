# 15. Partitioning & Filesystems

## 15.1 Viewing Disks & Partitions

```bash
lsblk           # Tree view of block devices
blkid           # Show UUIDs and filesystem types
df -h           # Disk usage per mounted filesystem
du -sh <dir>    # Size of a directory
```

## 15.2 Partitioning Tools

**`fdisk`** (MBR, and GPT support in modern versions):
```bash
fdisk /dev/sdb
# n = new partition, p = print table, d = delete, w = write & exit
```

**`parted`** (preferred for GPT / large disks):
```bash
parted /dev/sdb
# mklabel gpt
# mkpart primary ext4 0% 100%
```

## 15.3 Creating Filesystems

```bash
mkfs.ext4 /dev/sdb1
mkfs.xfs  /dev/sdb1
```

## 15.4 Mounting

**Temporary mount:**
```bash
mount /dev/sdb1 /mnt/data
umount /mnt/data
```

**Permanent mount (`/etc/fstab`):**
```
<device_or_UUID>   <mountpoint>   <fstype>   <options>   <dump>   <pass>
UUID=xxxxxxxx-xxxx   /mnt/data      ext4       defaults      0        2
```
- Prefer `UUID=` (from `blkid`) over `/dev/sdX` since device names can change between boots.
- Test the fstab entry without rebooting: `mount -a`.

## 15.5 Swap

```bash
mkswap /dev/sdb2       # Format partition as swap
swapon /dev/sdb2       # Activate it
swapoff /dev/sdb2      # Deactivate it
free -h                # View memory & swap usage
```

Persistent entry in `/etc/fstab`:
```
/dev/sdb2   none   swap   sw   0   0
```
