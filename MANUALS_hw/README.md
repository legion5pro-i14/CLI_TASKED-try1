# /README.md

## Network Documentation Overview

This documentation provides a condensed, tag-indexed guide for a three-router network integrating a dual-homed server.
**Use the tag quicklinks below or search by tags for topic-based retrieval.**
Device-specific files are linked for fast access to unique configuration details.

---

### 🔗 Quicklinks

- [TP-Link Archer A6 (Edge Router)](archer-a6.md)
- [Huawei OptiXstar EG8145X6-10 (ONT/Fiber Gateway)](optixstar-eg8145x6-10.md)
- [TP-Link TL-ER6020 (Dual-WAN Aggregator)](tl-er6020.md)
- [Dual-Homed Server Integration](server-integration.md)
- [Common Configs By Tag](common-configs.md)

---

# /server-integration.md

## Dual-Homed Server Integration

- **NIC1:** Connects to Archer A6 LAN (e.g., `192.168.0.x`)
- **NIC2:** Connects to TL-ER6020 LAN (e.g., `192.168.2.x`)
- **IP Config:**
    - Set static IPs, DNS as needed
- **Routing:**
    - TL-ER6020: Policy/rule-based routing to select primary WAN, failover to backup
    - System routing table on server: Default gateway typically on TL-ER6020 NIC


### Key Steps

- Server receives failover connectivity via TL-ER6020’s advanced routing
- DDNS configured on routers for remote access if dynamic WAN IPs
- Only enable firewall exceptions/port forwards as explicitly required

---

# /common-configs.md

## Common Config Snippets \& Tag Index

*Reference these for shared config tasks—do not duplicate in device-specific files unless syntax/path differs!*

---

### 🔹 Security Hardening

- **Admin Password/Firmware**
    - Change default admin password on first login (web UI location varies)
    - Update to latest stable firmware from vendor site
- **Firewall/DoS**
    - Enable SPI firewall, DoS protection, disable remote mgmt/web UI from WAN (if possible)
    - Use MAC filtering for Wi-Fi access where available

---

### 🔹 Port Forwarding

- **Port Forwarding / Virtual Server**
    - Add rule: Specify external port → internal host (static IP) and port
- **DDNS** (if dynamic WAN IP)
    - Register and enable DDNS on each router as appropriate

---

### 🔹 VPN

- **OpenVPN (Archer A6)**
    - Enable server, set protocol/port, export .ovpn config for clients
- **IPSec (TL-ER6020)**
    - Create tunnel, configure pre-shared key, set allowed networks

---

### 🔹 DHCP

- Only ONE DHCP server per subnet!
- Reserve static IPs for critical devices (e.g., server NICs)

---

### 🔹 Monitoring

- Enable logging on all routers
- Enable mail alerts if available for log/health events
- Schedule periodic firmware check \& planned reboots

---

### 🔹 Maintenance

- Backup configuration after initial setup and before any major change
- Document all static/DHCP IP assignments and port forwards in a table

---

# Usage Guidance

- To find config info by topic, search for the 🔹tag in this suite or use the YAML index in /README.md.
- For unique device steps, see the corresponding device markdown file.
- For workflow or commands common to multiple routers, see /common-configs.md.

---

**This suite is designed for optimal LLM-powered retrieval and technical admin usage—compact, quick to query, and easy to maintain.**

<div style="text-align: center">⁂</div>

[^1]: Archer-A6-C6-US-2.0_User-Guide.pdf

[^2]: optixstar_eg8145x610.pdf

[^3]: TL-ER6020_v1_User_Guide.pdf
