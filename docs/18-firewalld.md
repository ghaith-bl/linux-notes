# 18. firewalld

## 18.1 Concept

- Dynamic firewall management daemon. Rules are organized into **zones**, each representing a trust level for network connections/interfaces.
- Default zones: `public`, `home`, `work`, `trusted`, `internal`, `external`, `dmz`, `block`, `drop`.

## 18.2 Status & Zones

```bash
firewall-cmd --state                    # Check if firewalld is running
firewall-cmd --get-default-zone         # Show default zone
firewall-cmd --get-active-zones         # Show zones currently in use
firewall-cmd --set-default-zone=home    # Change default zone
```

## 18.3 Managing Rules

```bash
firewall-cmd --zone=public --list-all                    # List all rules for a zone

firewall-cmd --zone=public --add-service=http --permanent   # Allow a known service
firewall-cmd --zone=public --add-port=8080/tcp --permanent  # Allow a specific port

firewall-cmd --zone=public --remove-service=http --permanent
firewall-cmd --zone=public --remove-port=8080/tcp --permanent

firewall-cmd --reload                                     # Apply --permanent changes
firewall-cmd --get-services                                # List all known service names
```

- Without `--permanent`, changes are **runtime only** and lost on `--reload` or reboot.
- Always pair a permanent change with `--reload` (or add `--permanent` and re-run without it to apply immediately too).

## 18.4 Rich Rules (Advanced)

```bash
firewall-cmd --zone=public --add-rich-rule='rule family="ipv4" source address="192.168.1.10" accept' --permanent
```
