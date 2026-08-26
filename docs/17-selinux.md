# 17. SELinux

## 17.1 Concept

- **Mandatory Access Control (MAC)** layer on top of standard permissions (DAC). Even root is restricted by SELinux policy.
- Every process and file has a **security context**: `user:role:type:level` — for day-to-day work, the **type** is what matters most.

## 17.2 Modes

- **Enforcing** : Policy is enforced; violations are blocked and logged.
- **Permissive** : Violations are only logged, not blocked (useful for testing/debugging).
- **Disabled** : SELinux is off entirely.

```bash
getenforce                 # Show current mode
setenforce 0                # Switch to Permissive (temporary, until reboot)
setenforce 1                # Switch to Enforcing (temporary, until reboot)
```

Permanent change — edit `/etc/selinux/config`:
```
SELINUX=enforcing   # or permissive / disabled
```

## 17.3 Viewing & Changing Contexts

```bash
ls -Z file.txt              # View file context
ps -Z                        # View process contexts
id -Z                        # View current user context

chcon -t httpd_sys_content_t file.txt     # Change context temporarily (lost on relabel)
restorecon -Rv /path/to/dir               # Restore the context defined by policy
```

**Persistent custom context** (survives `restorecon`):
```bash
semanage fcontext -a -t httpd_sys_content_t "/web(/.*)?"
restorecon -Rv /web
```

## 17.4 Booleans (Toggle Policy Behavior)

```bash
getsebool -a                          # List all booleans
setsebool httpd_can_network_connect on         # Temporary
setsebool -P httpd_can_network_connect on      # Permanent (-P)
```

## 17.5 Troubleshooting

```bash
sealert -a /var/log/audit/audit.log   # Human-readable analysis (needs setroubleshoot)
ausearch -m avc -ts recent            # Search audit log for AVC denials
journalctl -t setroubleshoot          # SELinux-related journal entries
```

Useful packages: `policycoreutils`, `policycoreutils-python-utils` (provides `semanage`).
