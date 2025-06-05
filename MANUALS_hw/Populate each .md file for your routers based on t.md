<img src="https://r2cdn.perplexity.ai/pplx-full-logo-primary-dark%402x.png" class="logo" width="120"/>

# Populate each .md file for your routers based on the above outlines, using only key unique configs/snippets per model.

Maintain a single README.md for architectural context and file navigation.

Use tag-based quicklinks or YAML metadata for fast lookup and LLM-powered Q\&A (topics: VPN, port forwarding, security).

Review each file for redundant info, referencing common configs rather than duplicating.

Below you'll find a **memory-optimized, query-ready Markdown documentation suite** for your three-router network and its dual-homed server, using the requested structure and referencing only unique details/configs per device. Tag-based quicklinks and YAML metadata enable fast topic-based lookup and LLM question answering. Redundant/common steps are referenced, not duplicated.

---

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

### 🏷 Tag Index (YAML Metadata)

```yaml
security:
  description: "Security hardening, firewall, firmware, access controls"
  files: [common-configs.md, archer-a6.md, tl-er6020.md, optixstar-eg8145x6-10.md]
port_forwarding:
  description: "NAT, Virtual Servers, DMZ, DDNS"
  files: [common-configs.md, archer-a6.md, tl-er6020.md]
vpn:
  description: "OpenVPN, IPSec, remote access"
  files: [common-configs.md, archer-a6.md, tl-er6020.md]
dhcp:
  description: "DHCP scope, reservations, server"
  files: [common-configs.md, archer-a6.md, tl-er6020.md]
monitoring:
  description: "Logs, health checks, maintenance"
  files: [common-configs.md, archer-a6.md, tl-er6020.md, optixstar-eg8145x6-10.md]
dual_homed_server:
  description: "NIC setup, static IP, policy routing"
  files: [server-integration.md, tl-er6020.md]
```


---

# /archer-a6.md

## TP-Link Archer A6 (Archer C6) – Edge Router

### Essentials

- **Model/Manufacturer:** TP-Link Archer A6/C6 v2.0
- **WAN:** Dynamic/Static (from ISP, Earth port)
- **LAN:** Default `192.168.0.1/24`
- **Role:** Internet Edge, main home/office Wi-Fi AP
- **Features:** Dual-band Wi-Fi (AC1200), basic firewall, NAT, OpenVPN/PPTP, basic DoS defense


### Functional Context

- NAT and DHCP for end-user devices
- Port forwarding for any exposed LAN services
- Connects to TL-ER6020 for WAN aggregation


### Key Unique Configs/Tasks

- 🔹 **Security Hardening**
    - Change admin password: `Advanced > System Tools > Administration`
    - Update firmware: `Advanced > System Tools > Firmware Upgrade`
    - Enable SPI firewall \& DoS protection: `Advanced > Security > Settings`
    - Disable remote/web mgmt if not needed
- 🔹 **Port Forwarding**
    - Add virtual server:
`Advanced > NAT Forwarding > Virtual Servers > Add`
        - Set External Port, Internal IP (server), Protocol
    - Enable DDNS:
`Advanced > Network > Dynamic DNS`
- 🔹 **VPN**
    - Enable OpenVPN server:
`Advanced > VPN Server > OpenVPN > Enable`
    - Export client profile after configuration
- 🔹 **DHCP**
    - Main DHCP for LAN:
`Advanced > Network > DHCP Server`
    - Set static reservations for critical hosts
- 🔹 **Monitoring**
    - Enable system logs:
`Advanced > System Tools > System Log`
    - Traffic stats:
`Advanced > System Tools > Traffic Statistics`

**Official User Guide ([PDF Link](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/58692800/96ca62ba-1e0c-4625-b9e1-bb61591e3443/Archer-A6-C6-US-2.0_User-Guide.pdf))**

---

# /optixstar-eg8145x6-10.md

## Huawei OptiXstar EG8145X6-10 (FTTH ONT/Gateway)

### Essentials

- **Model/Manufacturer:** Huawei EG8145X6-10
- **WAN:** GPON (fiber, SC/APC port)
- **LAN:** 4 x GbE ports, 1 x POTS, Wi-Fi 6
- **Role:** ISP uplink, bridge/router, feeds LAN and Archer A6/TL-ER6020
- **Features:** ONT, Wi-Fi 6, USB, basic firewall


### Functional Context

- Typically set in bridge or router mode as per ISP
- Provides fiber Internet to LAN or acts as fiber handoff


### Key Unique Configs/Tasks

- 🔹 **Wi-Fi Setup**
    - Change SSID/password:
`Login to web UI > Advanced > WLAN > 2.4G/5G Basic Network Settings > SSID/Password > Apply`
- 🔹 **Security**
    - Change web login password immediately after first login!
    - MAC filter:
`Advanced > WLAN > MAC Address Filtering` (to restrict Wi-Fi access)
- 🔹 **Factory Reset**
    - Hold `Reset` button >10s (Caution: may require ISP reconfig)
- 🔹 **Bridge Mode**
    - Ask ISP for bridge mode or VLAN settings if direct pass-through is required for TL-ER6020
- 🔹 **Monitoring**
    - Check port status/indicators: LEDs on top of device
    - Basic connection status in web UI

**Official Quick Guide ([PDF Link](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/58692800/bc309315-8d1b-4b02-8ee3-06ec050a37be/optixstar_eg8145x610.pdf))**

---

# /tl-er6020.md

## TP-Link TL-ER6020 – Dual-WAN VPN Router

### Essentials

- **Model/Manufacturer:** TP-Link TL-ER6020
- **WAN:** Dual-GbE WAN ports (load balancing, failover)
- **LAN:** Configurable, e.g. `192.168.2.1/24`
- **Role:** WAN aggregator, advanced firewall, VPN gateway for server
- **Features:** Dual WAN, policy routing, advanced firewall, multi-tunnel VPN (IPSec/PPTP/L2TP)


### Functional Context

- Aggregates/fails over two WAN links (from Archer A6 and OptiXstar)
- Connects to dual-homed server (dedicated subnet)
- Handles advanced routing, prioritization, site-to-site/remote VPNs


### Key Unique Configs/Tasks

- 🔹 **Security Hardening**
    - Change default admin password on first login
    - Restrict web mgmt to LAN only
    - Enable DoS/Attack Defense:
`Firewall > Attack Defense`
- 🔹 **WAN Aggregation**
    - Configure dual WANs:
`Network > WAN > WAN1 & WAN2 settings`
    - Enable load balancing/failover as needed
- 🔹 **Policy Routing**
    - `Transmission > Policy Routing`
Use to route server traffic via preferred WAN, with fallback
- 🔹 **VPN**
    - Add VPNs:
`VPN > IPSec/PPTP/L2TP`
    - For remote access or site-to-site, follow wizard and export config for peers
- 🔹 **DHCP**
    - Typically DHCP server for the server subnet
`Network > DHCP Server`
- 🔹 **Monitoring**
    - View logs:
`System Tools > System Log`
    - Health checks:
`Status > System Status`

**Official User Guide ([PDF Link](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/58692800/0e87dd5f-5319-40d6-ad4f-f7c16bdb3c3c/TL-ER6020_v1_User_Guide.pdf))**

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

