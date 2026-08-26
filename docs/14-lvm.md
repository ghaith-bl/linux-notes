# 14. LVM (Logical Volume Manager)

## 14.1 Concept

- Flexible disk management layer that allows resizing storage dynamically, spanning multiple physical disks, without traditional partition size limits.
- **Layers:** Physical Volume (PV) -> Volume Group (VG) -> Logical Volume (LV).

## 14.2 Physical Volumes (PV)

```bash
pvcreate /dev/sdb1          # Initialize a disk/partition as a PV
pvs                          # Quick summary of PVs
pvdisplay                    # Detailed PV info
pvremove /dev/sdb1           # Remove PV
```

## 14.3 Volume Groups (VG)

```bash
vgcreate vg_data /dev/sdb1 /dev/sdc1   # Create VG from one or more PVs
vgs                                     # Quick summary of VGs
vgdisplay                               # Detailed VG info
vgextend vg_data /dev/sdd1              # Add a PV to an existing VG
vgremove vg_data                        # Remove VG
```

## 14.4 Logical Volumes (LV)

```bash
lvcreate -n lv_web -L 10G vg_data       # Create a 10G LV
lvcreate -n lv_web -l 100%FREE vg_data  # Use all remaining free space in the VG
lvs                                      # Quick summary of LVs
lvdisplay                                # Detailed LV info
lvremove /dev/vg_data/lv_web             # Remove LV
```

## 14.5 Extending a Logical Volume

```bash
lvextend -L +5G /dev/vg_data/lv_web           # Extend LV by 5G (filesystem NOT resized yet)
lvextend -r -L +5G /dev/vg_data/lv_web        # Extend LV AND resize the filesystem in one step

# Resize the filesystem manually (if not using -r):
resize2fs /dev/vg_data/lv_web    # for ext4
xfs_growfs /path/to/mountpoint   # for xfs (must be mounted; xfs can only grow, not shrink)
```

## 14.6 Reducing a Logical Volume

- Only possible with **ext4** (xfs cannot be shrunk).
```bash
umount /dev/vg_data/lv_web
e2fsck -f /dev/vg_data/lv_web
resize2fs /dev/vg_data/lv_web 5G
lvreduce -L 5G /dev/vg_data/lv_web
mount /dev/vg_data/lv_web /mountpoint
```

## 14.7 Typical Full Workflow

```bash
pvcreate /dev/sdb1
vgcreate vg_data /dev/sdb1
lvcreate -n lv_web -L 10G vg_data
mkfs.xfs /dev/vg_data/lv_web
mount /dev/vg_data/lv_web /mnt/web
```
