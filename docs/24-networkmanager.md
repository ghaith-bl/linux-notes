# 24. NetworkManager (`nmcli`)

## 24.1 Concept

- Default network configuration service on modern distributions. Unlike raw `ip` commands (which are lost on reboot), NetworkManager connections **persist**.

## 24.2 Viewing Status

```bash
nmcli device status         # List devices and their state
nmcli connection show       # List all configured connections
nmcli connection show eth0  # Show details of a specific connection
```

## 24.3 Configuring a Static IP

```bash
nmcli con add type ethernet con-name static-eth0 ifname eth0 ip4 192.168.1.50/24 gw4 192.168.1.1

# Or modify an existing connection:
nmcli con mod eth0 ipv4.addresses 192.168.1.50/24
nmcli con mod eth0 ipv4.gateway 192.168.1.1
nmcli con mod eth0 ipv4.dns "8.8.8.8 8.8.4.4"
nmcli con mod eth0 ipv4.method manual

nmcli con up eth0            # Apply the changes
```

## 24.4 Hostname

```bash
hostnamectl set-hostname newhostname
hostnamectl                  # Show current hostname info
```

## 24.5 `nmtui`

- Text-based UI alternative to `nmcli` for interactive configuration.
```bash
nmtui
```

- Connection files are stored under `/etc/NetworkManager/system-connections/`.
