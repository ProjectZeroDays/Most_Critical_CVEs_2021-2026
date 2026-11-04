# Critical Android Zero-Day & Zero-Click Vulnerability Matrix (2021–2026)

This document provides a comprehensive overview of the most critical **zero-day and zero-click vulnerabilities** affecting the Android ecosystem over the past five years. It highlights high-impact exploits spanning kernel drivers, framework services, media decoders, and radio stacks.

---

## Vulnerability Overview Table

| CVE ID | Severity / Score | Vulnerability Title & Description | Affected Component | Attack Vector / Execution Context |
| :--- | :---: | :--- | :--- | :--- |
| **CVE-2025-48595** | **CRITICAL** <br>`8.4` | **Framework Integer Overflow**<br>Bypasses system boundary controls to elevate local process access to `system`-level permissions. | Android Framework <br>*(Android 14–16)* | **Zero-Click / Local LPE:** Exploited in wild attack chains to silently escalate privileges. |
| **CVE-2024-53197** | **HIGH** <br>`7.8` | **Linux Kernel USB Audio Exploit**<br>Heap buffer corruption in the USB audio subsystem allowing kernel privilege escalation and memory disclosure. | Linux Kernel / Audio Subsystem | **Zero-Click:** Bypasses app sandboxes without user interaction when handling audio streams. |
| **CVE-2024-53150** | **HIGH** <br>`7.1` | **USB Kernel Subcomponent Flaw**<br>Out-of-bounds memory read/write in USB kernel driver allowing information disclosure and system escalation. | Linux Kernel | **Zero-Click / Hardware:** Exploited in targeted surveillance spyware chains via physical/emulated interfaces. |
| **CVE-2023-4863** /<br>**CVE-2023-38606** | **CRITICAL** <br>`8.8` | **libwebp Heap Buffer Overflow**<br>Zero-day flaw in WebP image parsing utilized by commercial spyware vendors across mobile platforms. | Google Chrome / Android System Graphics | **Zero-Click:** Triggered silently via image rendering in messaging applications or web browsers. |
| **CVE-2023-21255** | **CRITICAL** <br>`9.8` | **System Service RCE**<br>Remote code execution vulnerability in the core Android System component without requiring additional privileges. | Android System Core | **Zero-Click RCE:** Bypasses app permissions over network boundaries. |
| **CVE-2023-21268** | **HIGH** <br>`7.8` | **MediaCodec Heap Corruption**<br>Out-of-bounds write during video stream decoding enabling memory access control bypass. | MediaCodec Subsystem | **Zero-Click:** Malformed media file processing during background indexing or messaging preview. |
| **CVE-2023-45866** | **HIGH** <br>`8.1` | **Bluetooth Unauthenticated HID Injection**<br>Allows remote attackers to inject keystrokes over Bluetooth without pairing or user approval. | Android Bluetooth Stack <br>*(Android 4.4–14)* | **Zero-Click Remote Injection:** Operates over proximity wireless signals silently. |
| **CVE-2022-20186** | **CRITICAL** <br>`8.8` | **Mali GPU Driver Use-After-Free**<br>UAF vulnerability in Arm Mali GPU kernel driver leading to full kernel privilege escalation. | Vendor GPU Kernel Driver | **Zero-Day LPE:** Actively exploited by commercial exploit vendors for sandbox escapes. |
| **CVE-2021-0393** | **HIGH** <br>`7.8` | **Intent Redirection Privilege Escalation**<br>Flaw in `ActivityManager` allowing malicious background processes to hijack elevated system intents. | Android Framework | **Zero-Click LPE:** Background intent manipulation without requiring user confirmation. |
| **CVE-2020-0022** | **CRITICAL** <br>`8.8` | **BlueFrag Bluetooth Stack RCE**<br>Remote code execution via malformed Bluetooth L2CAP packets without pairing or user interaction. | Bluetooth Stack <br>*(Android 8.0–10)* | **Zero-Click Proximity RCE:** Broad-spectrum silent exploitation via unauthenticated RF packets. |

---

## Key Takeaways & Vector Analysis

1. **Media & Image Decoders as Zero-Click Vectors:** Processing untrusted media assets (such as WebP graphics via `libwebp` or video via `MediaCodec`) remains a primary entry point for zero-click surveillance toolkits.
2. **Kernel Driver Escalation:** GPU drivers (such as Arm Mali) and kernel subsystems (USB, Audio) are frequently leveraged after initial entry to escape application sandboxes and gain root/kernel access.
3. **Proximity Attacks:** Unauthenticated wireless stacks (Bluetooth L2CAP parsing, HID keystroke injection) represent critical threat vectors that operate without requiring any user interaction or device pairing.