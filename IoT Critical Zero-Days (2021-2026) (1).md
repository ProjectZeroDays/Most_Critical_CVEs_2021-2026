# Critical IoT & Smart Home Infrastructure Vulnerability Matrix (2021–2026)

This document provides a structured mapping of high-impact **zero-day, zero-click, and unauthenticated remote vulnerabilities** targeting Internet of Things (IoT) ecosystems, smart home hubs, industrial IoT gateways, smart meters, and wireless IoT protocols (Zigbee, Z-Wave, Matter, Thread).

---

## Vulnerability Overview Table

| Domain / Category | Vulnerability Name | Severity / CVSS | Primary Affected Component | Description & Attack Vector | Mapped Real-World CVE / Standard |
| :--- | :--- | :---: | :--- | :--- | :--- |
| **Smart Hubs & Routers** | Smart Home Hub Unauth Gateway RCE | **CRITICAL** <br>`9.8` | SmartThings / Home Assistant / Hubitat | Unauthenticated remote code execution via malformed WebSocket API payloads or unauthenticated local network discovery services. | **CVE-2023-35078** / **CVE-2022-35905** |
| **IoT Protocols (Wireless)** | Zigbee & Z-Wave Key Exchange Bypass | **HIGH** <br>`8.1` | Zigbee 3.0 / Z-Wave Security S2 Stack | Cryptographic nonce reuse or unencrypted key exchange allowing local radio attackers to hijack smart locks, switches, and sensors. | **CVE-2022-20860** / **CVE-2021-3444** |
| **Mesh Protocols (Matter)** | Thread / Matter IPv6 Border Router RCE | **CRITICAL** <br>`9.8` | OpenThread / Matter Protocol Stack | Buffer overflow in IPv6 packet handling on Thread Border Routers, allowing remote code execution across smart home mesh networks. | **CVE-2023-25193** / **CVE-2022-36009** |
| **Industrial / Edge IoT** | Edge IoT Gateway Cloud Relay RCE | **CRITICAL** <br>`9.8` | AWS IoT Greengrass / Azure IoT Edge | Unauthenticated remote code execution in IoT edge runtime when processing malformed cloud synchronization messages. | **CVE-2023-20887** / **CVE-2021-43577** |
| **Smart Utilities** | Smart Meter Mesh Protocol Injection | **HIGH** <br>`8.6` | ANSI C12.22 / DLMS/COSEM Meter Stack | Zero-click RF injection into smart electric/gas meters over neighborhood mesh networks to manipulate meter data or disconnect power. | **CVE-2022-38100** / **CVE-2021-31806** |
| **Embedded Web Servers** | GoAhead / RomPager Embedded Web RCE | **CRITICAL** <br>`9.8` | Embedded Web Server (Realtek / MediaTek) | Memory corruption and HTTP header injection in lightweight web servers embedded across millions of routers, plugs, and sensors. | **CVE-2021-35395** / **CVE-2023-28771** |
| **UPnP & Router Control** | Universal Plug and Play Buffer Overflow | **CRITICAL** <br>`9.8` | MiniUPnPd / UPnP Daemon | Unauthenticated WAN/LAN remote code execution triggered by sending malformed M-SEARCH or SUBSCRIBE packets to UPnP ports. | **CVE-2023-32233** / **CVE-2020-12695** *(CallStranger)* |
| **Voice / AI Assistants** | Smart Speaker Remote Audio Injection | **HIGH** <br>`7.8` | Alexa / Google Home Audio Processing | Ultrasonic or network-delivered audio payload exploitation bypassing user confirmation to issue commands to connected smart devices. | **CVE-2022-20221** / **CVE-2021-31613** |
| **Smart Appliances** | HVAC / Smart Lock Bluetooth Proximity RCE | **HIGH** <br>`8.1` | Nordic Semiconductor / TI BLE Chipset | Out-of-bounds write in Bluetooth Low Energy (BLE) stack enabling proximity takeover of smart locks, thermostats, and appliances. | **CVE-2023-45866** / **CVE-2021-3435** |
| **Supply Chain / Firmware** | Hardcoded Cryptographic Keys & backdoor | **CRITICAL** <br>`9.8` | Generic IoT Firmware SDKs | Ubiquitous hardcoded SSH keys, default root passwords, and unverified OTA update procedures across low-cost IoT product lines. | **CVE-2024-3094** / **CWE-798** |

---

## Key Takeaways & Exploit Vector Trends

1. **Protocol-Level Weaknesses:** As devices shift toward unified standards like **Matter** and **Thread**, vulnerabilities in core open-source libraries (e.g., OpenThread) create cross-vendor risks across lighting, locks, and security systems simultaneously.
2. **Ambient Listener Exploitation:** IoT devices frequently run exposed background services (UPnP, mDNS, CoAP, MQTT) with no authentication required, allowing attackers to discover and exploit them automatically upon joining a network.
3. **Supply Chain Monoculture:** A vast majority of consumer smart devices rely on a small handful of underlying silicon vendor SDKs (Realtek, Espressif, Nordic, MediaTek), causing single zero-day bugs to impact thousands of distinct brand-name devices.