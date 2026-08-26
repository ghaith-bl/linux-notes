# 21. Systemd Targets

## 21.1 Concept

- Targets are systemd's equivalent of old SysV **runlevels**, grouping related units (services) together as a synchronization point.

| Target | Old Runlevel | Meaning |
|---|---|---|
| `poweroff.target` | 0 | Shut down the system |
| `rescue.target` | 1 | Single-user / maintenance mode |
| `multi-user.target` | 3 | Full multi-user, no GUI |
| `graphical.target` | 5 | Multi-user + GUI |
| `reboot.target` | 6 | Reboot the system |

## 21.2 Commands

```bash
systemctl get-default                        # Show the current default target
systemctl set-default multi-user.target      # Set the default target (persists across reboots)
systemctl isolate multi-user.target          # Switch to a target right now (without changing default)
systemctl list-units --type=target           # List all active targets
```
