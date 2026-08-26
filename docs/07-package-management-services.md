# 7. Package Management & Services

## 7.1 Package Management

- **Concept:** Installing, updating, removing, and managing software packages.
- **Package:** A collection of files (binaries, libraries, config, docs) needed for a piece of software.
- **Repository:** A central server storing packages.

### Debian-based (Ubuntu, Kali, Mint)

Tools: `apt`, `apt-get` (higher-level), `dpkg` (lower-level).

```bash
apt update                       # Refresh package lists from repositories
apt upgrade                      # Upgrade installed packages to newest versions
apt install <package_name>       # Install a package
apt remove <package_name>        # Remove a package (keeps config files)
apt purge <package_name>         # Remove package and config files
apt search <keyword>             # Search for packages
apt list --installed             # List installed packages
dpkg -i <package.deb>            # Install a downloaded .deb file
```
(`sudo` usually required)

### Red Hat-based (CentOS, Fedora, RHEL)

Tools: `dnf` (newer), `yum` (older), `rpm` (lower-level).

```bash
dnf update            # or: dnf upgrade
dnf install <package_name>
dnf remove <package_name>
dnf search <keyword>
dnf list installed
rpm -ivh <package.rpm>    # Install a downloaded .rpm file
```
(`sudo` usually required)

## 7.2 System Services (Systemd)

- **Concept:** Managing background processes (daemons) that provide system functionality (e.g., web server, SSH server).
- **Systemd:** The standard init system and service manager in most modern Linux distributions.
- **Control Tool (`systemctl`):** Used to manage services (`sudo` usually required).

```bash
systemctl status <service_name>   # Check if a service is running (e.g., systemctl status sshd)
systemctl start <service_name>    # Start a service
systemctl stop <service_name>     # Stop a service
systemctl restart <service_name>  # Stop and then start a service
systemctl enable <service_name>   # Make service start automatically on boot
systemctl disable <service_name>  # Prevent service from starting automatically on boot
```
