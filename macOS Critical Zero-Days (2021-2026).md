# Critical macOS Zero-Day & Zero-Click Vulnerability Matrix (2021–2026)

This document provides a structured mapping of the most critical **zero-day and zero-click vulnerabilities** affecting Apple's macOS ecosystem over the past five years. It highlights high-impact exploit vectors across WebKit, System Subsystems, TCC (Transparency, Consent, and Control) Bypasses, Gatekeeper, and Kernel Drivers.

---

## Vulnerability Overview Table

| Domain / Category | Vulnerability Name | Severity / CVSS | Primary Affected Component | Description & Attack Vector | Mapped Real-World CVE / Standard |
| :--- | :--- | :---: | :--- | :--- | :--- |
| **System Subsystem** | macOS WindowServer Sandbox Escape | **HIGH** <br>`7.8` | WindowServer IPC Subsystem | Local privilege escalation via WindowServer IPC handling, allowing arbitrary code execution with root privileges from a sandboxed app context. | **CVE-2023-26818** / **CVE-2022-42864** |
| **Security Bypasses** | Gatekeeper Malformed Archive Bypass | **HIGH** <br>`7.8` | Gatekeeper / Archive Utility | Bypasses Gatekeeper security verification via malformed ZIP archives or uncurated unsigned payloads, allowing unsigned execution. | **CVE-2022-42821** *(Achilles)* / **CVE-2021-30657** |
| **Privacy & Access Control** | TCC Permission Bypass via System Tools | **HIGH** <br>`7.8` | TCC Subsystem / System Events | Allows sandboxed applications to bypass Privacy (TCC) prompt requirements to access camera, microphone, or disk files without user consent. | **CVE-2023-32413** / **CVE-2021-30713** |
| **Kernel / Driver** | IOHIDKit & GPU Driver Kernel LPE | **CRITICAL** <br>`8.8` | IOHIDFamily / Apple GPU Drivers | Out-of-bounds read/write in input handling drivers leading to arbitrary kernel code execution and System Integrity Protection (SIP) bypass. | **CVE-2023-32434** / **CVE-2021-30807** |
| **Graphics & Rendering** | ImageIO / CoreGraphics Heap Overflow | **CRITICAL** <br>`8.8` | ImageIO / CoreGraphics Framework | Heap buffer overflow when processing malformed images (e.g., inside Safari, Preview, or Messages) leading to arbitrary code execution. | **CVE-2023-41064** / **CVE-2021-30860** *(FORCEDENTRY)* |
| **Web Browser** | WebKit JIT Type Confusion | **CRITICAL** <br>`8.8` | Safari WebKit JIT Compiler | Type confusion in WebKit allowing remote code execution via malicious web content, bypassing browser process isolation. | **CVE-2023-32373** / **CVE-2023-28205** |
| **Core Utilities** | Finder & Archive Utility Code Execution | **HIGH** <br>`7.5` | Finder / LaunchServices | Execution of untrusted code via double-clicking crafted `.inetloc` files or manipulated mount paths bypassing execution prompts. | **CVE-2021-30853** / **CVE-2020-9861** |
| **Proximity & Wireless** | AirDrop / AWDL Proximity RCE | **HIGH** <br>`7.8` | Apple Wireless Direct Link (AWDL) | Zero-click payload delivery via AWDL protocol manipulation, exploiting memory corruption in proximity-based wireless transfers. | **CVE-2021-30839** *(AWDL proximity exploit)* |
| **Screen Sharing & IPC** | Screen Sharing / Remote Management LPE | **HIGH** <br>`7.8` | Apple Remote Desktop / ScreenSharing | Local and remote privilege escalation via malformed IPC calls to Screen Sharing daemons. | **CVE-2022-32832** / **CVE-2023-27930** |
| **Hardware & Firmware** | Apple Silicon BootROM / Secure Enclave | **MEDIUM** <br>`6.8` | Secure Enclave / Boot Controller | Side-channel timing attacks and memory corruption in chip firmware allowing extraction of encryption keys or secure storage access. | **CVE-2022-22583** / **CVE-2021-30735** |

---

## Key Takeaways & Exploit Vector Trends

1. **Gatekeeper & TCC Bypasses:** Unlike iOS, where the app sandbox is rigid, macOS attackers frequently exploit logic flaws in Gatekeeper and TCC to execute untrusted code or steal user data without needing zero-click kernel chains.
2. **Shared Ecosystem Vectors:** Vulnerabilities in shared components (WebKit, ImageIO, CoreGraphics, AWDL) affect both macOS and iOS, allowing attackers to retarget zero-click iMessage or web exploits across both mobile and desktop platforms.
3. **Privilege Escalation via IPC:** Flaws in system daemons (`WindowServer`, `IOHIDFamily`, `ScreenSharing`) are heavily relied upon to escalate privileges from standard sandboxed application contexts to `root` or kernel permissions.