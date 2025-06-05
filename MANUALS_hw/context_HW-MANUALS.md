Network Routers: Condensed Documentation Suite
Overview
This documentation provides structured, condensed summaries for three routers deployed in a network with a dual-homed server. It’s designed for efficient LLM context retrieval, query-based navigation, and minimal memory footprint.

1. Hardware Overview (Essentials)
Router 1: TP-Link Archer A6 (Archer C6)
Manufacturer: TP-Link

Model: Archer A6/C6 v2.0

WAN IP: (example) DHCP (from ISP)

LAN IP: Default 192.168.0.1

Role: Primary Internet Edge Router

Features:

Gigabit Ethernet, dual-band Wi-Fi (AC1200)

SPI firewall, basic DoS protection, Access Control

NAT, DHCP server, basic VPN server (OpenVPN, PPTP)

Router 2: Huawei OptiXstar EG8145X6-10
Manufacturer: Huawei

Model: OptiXstar EG8145X6-10

WAN: Fiber (SC/APC Optical port)

LAN: 4 x Gigabit, 1 x POTS, Wi-Fi 6

Role: Fiber Gateway/ONT + Wi-Fi AP

Features:

GPON ONT, Wi-Fi 6, USB, WPS/Wi-Fi buttons

IP config via Web UI, acts as bridge/endpoint

Router 3: TP-Link TL-ER6020
Manufacturer: TP-Link

Model: TL-ER6020

WAN IPs: Dual-WAN, configurable

LAN IP: Configurable (e.g., 192.168.2.1)

Role: Dual-WAN Aggregation/Load Balancer/VPN Gateway (for the dual-homed server)

Features:

Dual Gigabit WAN, load balancing/failover

Advanced routing, robust firewall, extensive VPN support (IPSec, PPTP, L2TP)

2. Functional Context (Usage & Integration)
Network Roles/Interactions:

Archer A6 serves as the main Internet access point for branch/home users, handling guest Wi-Fi, NAT, and port forwarding for public services. Connects via WAN to ISP, LAN to local switch, and to TL-ER6020.

OptiXstar EG8145X6-10 acts as the main fiber uplink/router, feeding the local network; LAN ports connect to user devices or uplink to Archer A6 and/or TL-ER6020 as required.

TL-ER6020 manages dual WAN (from Archer A6 and OptiXstar), aggregating both links for the dual-homed server. Handles advanced routing, prioritizes server traffic, and provides VPN tunnels for remote management.

Integration with Dual-Homed Server:

Server has two NICs: one to Archer A6 subnet, one to TL-ER6020 subnet.

TL-ER6020 provides dual path/failover for server, firewall separation, and VPN endpoint.

Routing tables configured to prioritize mission-critical traffic on preferred WAN.

3. Key Configuration Steps (Tag System)
🔹 Security Hardening
Factory reset each router before deployment.

Set strong admin passwords; update firmware.

Configure SPI firewall (Archer A6), enable DoS protection.

Disable unused services (WPS, remote mgmt as needed).

On TL-ER6020, restrict management to internal subnet only.

🔹 Port Forwarding
Use Archer A6 for "Virtual Servers" to expose external services.

Set up DDNS on Archer A6 if WAN IP is dynamic.

For server-specific access, configure port forwarding NAT rules on both Archer A6 and TL-ER6020 as appropriate.

Ensure OptiXstar is in bridge or routed mode as required by the ISP.

🔹 Server Connectivity
Assign static IPs to the server’s two NICs.

TL-ER6020: Use policy routing to prefer primary WAN, with fallback to secondary.

On Archer: set routing rules or static routes if server needs to reach opt-in subnets or remote management.

🔹 VPN Capabilities & Remote Access
Enable OpenVPN server on Archer A6 for secure remote access.

TL-ER6020: Use IPSec VPN for site-to-site or advanced remote management.

Use strong pre-shared keys or certificates.

🔹 DHCP & Firewall
Only one router should run DHCP per subnet.

Use Archer’s DHCP for main user devices; TL-ER6020 for server subnet.

TL-ER6020: Create inbound/outbound firewall rules for server access control.

🔹 Monitoring & Maintenance
Enable logging on all routers (system log, traffic stats).

Set automated firmware update checks (Archer A6, OptiXstar).

Schedule regular reboots (night maintenance window).

Use router-side traffic stats to monitor bandwidth usage.

4. Memory Load Optimization
Deduplication: Only list unique router features/configs; shared steps referenced by tag.

Config Examples: Provide only one syntax example per task; reference routers by model where command/UI path differs.

Index by Tag: Tag lines (as above) allow for fast LLM retrieval and answer composition by topic.

5. Example: File Breakdown for LLM/MD Structure
/docs/aracher-a6.md (TP-Link edge router summary)

/docs/optixstar-eg8145x6.md (Huawei ONT/fiber gateway summary)

/docs/tl-er6020.md (Dual-WAN router/aggregation summary)

/docs/server-integration.md (Dual-homed server & routing)

/docs/common-configs.md (Tag-indexed config snippets for hardening, forwarding, VPN, DHCP, etc.)

/docs/README.md (Network overview and structure)

6. Example MD File: Archer A6
text
# Archer A6 – Condensed Router Overview

## Essentials
- Model: TP-Link Archer A6/C6
- WAN: DHCP/static (typ. ISP)
- LAN: 192.168.0.1/24
- Main Features: Dual-band Wi-Fi, SPI firewall, DoS protection, VPN (OpenVPN/PPTP), NAT

## Usage Context
- Role: Internet edge, primary Wi-Fi AP, NAT, DHCP for user devices
- Connected To: ISP (WAN), user LAN, TL-ER6020 (aggregation)

## Key Configs
- 🔹 Security Hardening: Change admin, enable firewall, update firmware, disable remote management
- 🔹 Port Forwarding: Advanced > NAT Forwarding > Virtual Servers (e.g., map WAN 8080 → LAN 192.168.0.10:80)
- 🔹 VPN: Advanced > VPN Server > OpenVPN (export config for clients)
- 🔹 DHCP: Advanced > Network > DHCP Server (set IP pool, reservations for critical devices)
- 🔹 Logs: Advanced > System Tools > System Log (enable, set mail notification if needed)

## References
- [Official User Guide PDF](link/to/manual)
7. Metadata/Index for Query-Based Retrieval
text
- tag: security
  routers: [Archer A6, OptiXstar, TL-ER6020]
  steps: [hardening, password, firewall, firmware]
- tag: port_forwarding
  routers: [Archer A6, TL-ER6020]
- tag: vpn
  routers: [Archer A6, TL-ER6020]
- tag: dual-homed_server
  details: [NIC setup, static IPs, routing, failover]