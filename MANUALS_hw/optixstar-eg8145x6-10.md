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
