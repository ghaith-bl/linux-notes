# 25. Chrony / NTP (Time Synchronization)

## 25.1 Concept

- `chronyd` synchronizes the system clock with NTP time servers. It's the default time-sync daemon on modern RHEL/Fedora/Ubuntu (replaces the older `ntpd`).
- Config file: `/etc/chrony.conf`.

## 25.2 Commands

```bash
chronyc tracking        # Show current sync status (offset, drift, etc.)
chronyc sources -v      # List configured NTP sources and their state
chronyc makestep        # Force an immediate time correction
```

## 25.3 Service Management

```bash
systemctl status chronyd
systemctl enable --now chronyd
```
