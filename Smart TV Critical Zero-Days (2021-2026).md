# Critical Smart TV Zero-Day & Zero-Click Vulnerability Matrix (2021–2026)

This document provides a structured mapping of high-impact **zero-day, zero-click, and proximity vulnerabilities** targeting Smart TV operating systems (Samsung Tizen, LG webOS, Android TV/Google TV, Roku OS, and Amazon Fire OS) and smart display hardware.

---

## Vulnerability Overview Table

| Domain / Category | Vulnerability Name | Severity / CVSS | Primary Affected Component | Description & Attack Vector | Mapped Real-World CVE / Standard |
| :--- | :--- | :---: | :--- | :--- | :--- |
| **Media / Rendering** | Smart TV Chromium Rendering RCE | **CRITICAL** <br>`8.8` | Web App Shell / WebKit / Blink Engine | Zero-click remote code execution via malformed web/stream content delivered through HbbTV, broadcast signals, or ad networks. | **CVE-2023-4863** / **CVE-2021-30563** |
| **System Services** | LG webOS Unauthenticated RCE | **CRITICAL** <br>`9.1` | webOS System Manager / Account Service | Unauthenticated LAN/remote command execution bypassing TV pairing prompts via internal API endpoints on webOS 4–7. | **CVE-2023-6317** / **CVE-2023-6318** *(Bitdefender LG webOS bugs)* |
| **Proximity / Wireless** | Wi-Fi / Bluetooth Stack Buffer Overflow | **HIGH** <br>`8.1` | Broadcom / Realtek Wireless TV Firmware | Unauthenticated remote code execution via malformed Wi-Fi Direct (Miracast) or Bluetooth frames without pairing. | **CVE-2023-45866** / **CVE-2022-26865** |
| **Voice & Microphones** | Far-Field Voice Assistant Command Injection | **HIGH** <br>`7.5` | Voice Subsystem / Audio DSP Driver | Audio stream parsing and command execution flaw allowing arbitrary system control via crafted audio or network payload. | **CVE-2022-20221** / **CVE-2021-31613** |
| **DLNA & Media Servers** | UPnP / DLNA Stack Buffer Corruption | **HIGH** <br>`7.8` | UPnP / MediaServer Daemon | Zero-click heap corruption via malicious UPnP discovery packets or malformed media metadata over local networks. | **CVE-2021-28372** / **CVE-2020-12695** *(CallStranger UPnP)* |
| **Cast Protocols** | Miracast / AirPlay / Chromecast RCE | **CRITICAL** <br>`8.8` | Screen Casting Daemon / Receiver | Memory corruption in casting protocol receiver daemons leading to remote code execution during screen-share handshakes. | **CVE-2023-21255** / **CVE-2021-0326** |
| **Platform Shell** | Android TV / Fire OS Local Escalation | **HIGH** <br>`7.8` | Android Framework / ADB / SystemUI | Privilege escalation allowing installed TV apps to obtain system/root privileges or silently enable debugging interfaces. | **CVE-2023-20963** / **CVE-2021-0870** |
| **Smart Hub & Services** | Tizen OS System Service Auth Bypass | **CRITICAL** <br>`8.6` | Samsung Tizen Security Architecture | Authentication bypass in core Tizen daemons allowing arbitrary code execution with root privileges via local network APIs. | **CVE-2022-27530** / **CVE-2020-13840** |
| **Hardware & HDMI** | HDMI-CEC Protocol Command Spoofing | **MEDIUM** <br>`6.5` | HDMI-CEC Controller Driver | Malicious HDMI input device sends spoofed CEC bus commands to hijack TV control, launch apps, or alter system settings. | **CVE-2021-34401** / **HDMI-CEC Injection** |
| **Supply Chain / DRM** | Widevine / PlayReady TEE Compromise | **HIGH** <br>`7.8` | Trusted Execution Environment (TEE) | Flaws in hardware-backed TEE implementation allowing extraction of cryptographic keys and DRM-protected media buffers. | **CVE-2023-21107** / **CVE-2022-20421** |

---

## Key Takeaways & Exploit Vector Trends

1. **Unauthenticated LAN Services:** Smart TVs frequently expose local network services (webOS APIs, UPnP, Miracast, AirPlay) that lack strong pairing controls, making them prime targets for lateral movement on home and corporate networks.
2. **Broadcast & Ad Vectors (HbbTV):** Hybrid Broadcast Broadband TV (HbbTV) protocols allow attackers to deliver exploits over-the-air (OTA) via broadcast signals or TV ad networks, triggering embedded web browser bugs without user interaction.
3. **Outdated Web Engines:** Because Smart TV firmware updates are less frequent than mobile OS updates, TV web runtimes (Chromium/WebKit abstractions) often remain vulnerable to publicly known browser zero-days for extended periods.