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