# Critical Smart Camera, PTZ/PoE & Baby Monitor Vulnerability Matrix (2021–2026)

This document provides a structured mapping of high-impact **zero-day, zero-click, and unauthenticated remote vulnerabilities** targeting smart cameras, Flock LPR (License Plate Reader) networks, PTZ (Pan-Tilt-Zoom) & PoE industrial cameras, baby monitors, and cloud-connected surveillance hardware.

---

## Vulnerability Overview Table

| Category / Device Type | Vulnerability Name | Severity / CVSS | Primary Affected Component | Description & Attack Vector | Mapped Real-World CVE / Standard |
| :--- | :--- | :---: | :--- | :--- | :--- |
| **Flock & LPR Cameras** | License Plate Reader Unauth API & Command Injection | **CRITICAL** <br>`9.8` | Flock Safety Gateway / Web API | Unauthenticated remote code execution and credential bypass in ALPR (Automatic License Plate Reader) edge processing units. | **CVE-2024-33821** / **CVE-2022-46888** *(LPR Edge RCE)* |
| **Cloud Smart Cameras** | Ring & Cloud Cam Account / Audio Stream Interception | **HIGH** <br>`8.1` | Ring Android App / Intent Redirection | Intent redirection and SIP token theft allowing unauthorized remote access to live video/audio feeds and camera controls. | **CVE-2022-30740** *(Ring Android App Flaw)* |
| **PoE / Industrial Cameras** | Dahua & Hikvision ONVIF Auth Bypass | **CRITICAL** <br>`9.8` | ONVIF Protocol Stack / Web Server | Unauthenticated admin access and arbitrary code execution via forged ONVIF WS-Security headers over PoE networks. | **CVE-2021-33044** / **CVE-2021-36260** *(Hikvision RCE)* |
| **PTZ Cameras** | PTZ Control Protocol & Web Server Command Injection | **CRITICAL** <br>`9.8` | Axis / Hanwha / Sunell PTZ Firmware | Zero-click unauthenticated RCE via buffer overflows in Web/RTSP/ONVIF parsing engines controlling pan-tilt-zoom units. | **CVE-2023-21415** / **CVE-2021-31986** *(Axis PTZ RCE)* |
| **Baby Monitors** | Smart Baby Monitor Cloud & P2P Stream Hijacking | **CRITICAL** <br>`9.1` | Owlet / Nanit / VTech P2P Gateway | Hardcoded cryptographic keys and unauthenticated P2P (ThroughTek Kalay) protocol flaw enabling unauthorized live stream eavesdropping. | **CVE-2021-28372** *(Kalay P2P SDK RCE)* / **CVE-2022-26330** |
| **Streaming Protocols** | RTSP / SIP Media Stack Buffer Overflow | **CRITICAL** <br>`9.8` | `live555` / Embedded RTSP Server | Zero-click heap buffer overflow triggered by sending malformed RTSP setup requests or malicious SDP payloads to camera endpoints. | **CVE-2023-29471** / **CVE-2021-32563** |
| **Local / Mesh Wireless** | Wi-Fi Direct & Cloud Edge Relay Bypass | **HIGH** <br>`8.6` | Battery Camera Wireless Daemon | Memory corruption in proximity Wi-Fi setup services allowing local attackers to extract Wi-Fi passwords and gain camera shell access. | **CVE-2023-45866** / **CVE-2022-22515** |
| **Firmware & Supply Chain** | Realtek / MediaTek SDK Pre-Auth RCE | **CRITICAL** <br>`9.8` | Realtek Jungle SDK / SoC Firmware | Stack-based buffer overflow in embedded web management interface shared across hundreds of OEM IP camera vendors. | **CVE-2021-35395** *(Realtek SDK RCE)* |
| **Cloud Bridge / NVR** | Network Video Recorder Remote Arbitrary Command Execution | **CRITICAL** <br>`9.8` | Reolink / Lorex / Amcrest NVR Gateway | Unauthenticated command injection in NVR cloud pairing daemons allowing total network compromises via cloud relay. | **CVE-2022-29490** / **CVE-2021-4045** |
| **Hardware & Debugging** | Unprotected UART / JTAG & Flash Memory Extraction | **HIGH** <br>`7.5` | Camera PCB Debug Headers / SPI Flash | Physical/Proximity hardware exploit extracting root credentials, AWS tokens, and firmware encryption keys directly from flash memory. | **CWE-1277** / **CWE-1188** *(Hardcoded Credentials)* |

---

## Key Takeaways & Exploit Vector Trends

1. **Shared Supply Chain SDKs:** A significant portion of IP camera zero-days stem from underlying chip/SDK vendors (e.g., Realtek, ThroughTek Kalay P2P, Live555) rather than the camera branding, making hundreds of distinct models vulnerable simultaneously.
2. **Unauthenticated Protocol Handshakes:** RTSP, ONVIF, and UPnP services routinely run with elevated permissions without requiring strong initial authentication, leaving PoE and PTZ industrial cameras vulnerable to automated network scanners.
3. **P2P & Cloud Relay Risks:** Consumer cameras and baby monitors often rely on third-party P2P mesh SDKs to bypass home firewalls, creating zero-click attack paths where remote attackers can hijack video streams over the internet.