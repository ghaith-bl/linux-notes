# 19. SSH & Key-Based Authentication

## 19.1 Concept

- Secure protocol for remote login and administration.
- Server config: `/etc/ssh/sshd_config`. Client config: `~/.ssh/config`.

## 19.2 Key-Based Authentication

```bash
ssh-keygen -t ed25519                 # Generate a new keypair (or -t rsa)
ssh-copy-id user@remote_host          # Copy your public key to a remote server
ssh user@remote_host                  # Connect
ssh -p 2222 user@remote_host          # Connect on a custom port
```

## 19.3 Hardening `sshd_config`

```
PermitRootLogin no
PasswordAuthentication no
Port 2222
AllowUsers alice bob
```

Apply changes:
```bash
systemctl restart sshd
```

## 19.4 Copying Files Over SSH

```bash
scp file.txt user@host:/remote/path/
scp -r dir/ user@host:/remote/path/
rsync -avz dir/ user@host:/remote/path/
```
