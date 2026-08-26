# 20. Boot Process & GRUB

## 20.1 Boot Stages

```
BIOS/UEFI -> Bootloader (GRUB2) -> Kernel + initramfs -> systemd (PID 1) -> Target (runlevel equivalent)
```

## 20.2 GRUB2 Configuration

- Edit `/etc/default/grub` (never edit `grub.cfg` directly, it's auto-generated).
- Regenerate the config after changes:
```bash
grub2-mkconfig -o /boot/grub2/grub.cfg          # BIOS systems
grub2-mkconfig -o /boot/efi/EFI/<distro>/grub.cfg  # UEFI systems
```

- Manage the default boot kernel:
```bash
grubby --default-kernel
```

## 20.3 Resetting the Root Password (Rescue Mode)

1. At the GRUB menu, select the kernel entry and press `e` to edit.
2. Find the line starting with `linux` (or `linux16`), append `rd.break` (RHEL) or `init=/bin/bash` at the end.
3. Press `Ctrl+X` (or `F10`) to boot with the edit.
4. Remount root as read-write:
   ```bash
   mount -o remount,rw /sysroot   # (in rd.break, then: chroot /sysroot)
   ```
5. Reset the password:
   ```bash
   passwd root
   ```
6. If SELinux is enabled, force a relabel on next boot:
   ```bash
   touch /.autorelabel
   ```
7. Exit chroot and reboot: `exit`, `exit`, then `reboot`.

## 20.4 Kernel Info

```bash
rpm -q kernel      # List installed kernel packages
ls /boot            # List boot files, including vmlinuz and initramfs images
```
