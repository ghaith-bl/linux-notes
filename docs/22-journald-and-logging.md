# 22. journald & Logging

## 22.1 Concept

- `systemd-journald` collects and manages system logs in a structured binary format.
- Traditional plain-text logs (`/var/log/messages`, `/var/log/secure`, etc.) may still exist via `rsyslog` on many distributions.

## 22.2 `journalctl`

```bash
journalctl                              # View all logs
journalctl -f                           # Follow live (like tail -f)
journalctl -u sshd                      # Logs for a specific service/unit
journalctl -b                           # Logs since the current boot
journalctl -b -1                        # Logs from the previous boot
journalctl --since "2026-08-01" --until "2026-08-02"
journalctl -p err                       # Filter by priority (e.g., err, warning, crit)
```

## 22.3 Persistent Journal Storage

By default the journal may be volatile (in-memory, lost on reboot). To make it persistent:

```bash
mkdir -p /var/log/journal
```
And set in `/etc/systemd/journald.conf`:
```
Storage=persistent
```
Then restart the service:
```bash
systemctl restart systemd-journald
```
