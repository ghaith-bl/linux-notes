# 6. Networking

## 6.1 Network Configuration

- **Concept:** Viewing IP addresses, interfaces, and routing.
- **Modern Tool (`ip`):**
  - `ip addr show` or `ip a` : Display IP addresses and network interfaces.
  - `ip route show` : Display the routing table.
- **Older Tool (`ifconfig`):** Still common, may need installation (`sudo apt install net-tools`). Shows interface configuration.

## 6.2 Connectivity Testing

- **Concept:** Checking if network hosts are reachable.
- **Ping (`ping`):** `ping <hostname_or_IP>` (e.g., `ping google.com`, `ping 8.8.8.8`). Sends ICMP Echo Request packets. Use `Ctrl+C` to stop.

## 6.3 Network Connections & Sockets

- **Concept:** Seeing active network connections and listening ports.
- **Modern Tool (`ss`):** Socket Statistics.
  - `ss -tulnp` : Show TCP (`t`), UDP (`u`), listening (`l`), numeric ports/IPs (`n`), process owning socket (`p`). Very useful.
- **Older Tool (`netstat`):** May need installation (`net-tools`). Similar options (e.g., `netstat -tulnp`).

## 6.4 DNS Lookup

- **Concept:** Resolving domain names to IP addresses.
- **Dig (`dig`):** Detailed DNS information. `dig <domain_name>` (e.g., `dig example.com`).
- **Host (`host`):** Simpler DNS lookup. `host <domain_name>`.

## 6.5 Data Transfer

- **Concept:** Downloading or interacting with web resources.
- **Curl (`curl`):** Versatile tool for transferring data with URLs. Can GET, POST, etc.
  - `curl <URL>` (displays content)
  - `curl -O <URL>` (saves to file)
- **Wget (`wget`):** Non-interactive network downloader. `wget <URL>` (downloads file).
