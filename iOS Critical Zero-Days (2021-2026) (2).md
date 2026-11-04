# Critical iOS Zero-Day & Zero-Click Vulnerability Matrix (2021–2026)

This document provides a structured mapping of the most critical **zero-day and zero-click vulnerabilities** affecting Apple's iOS ecosystem over the last five years, including exploit vectors used by advanced commercial spyware chains.

| Domain / Category | Vulnerability Name | Severity | Primary Affected Component | Description & Attack Vector | Mapped Real-World CVE / Standard |
| :--- | :--- | :---: | :--- | :--- | :--- |
| **Coproc & Kernel** | RTKit & Kernel Out-of-Bounds | **CRITICAL** | RTKit Coprocessor / iOS Kernel | Out-of-bounds write allowing attackers with memory access to bypass kernel protections. | **CVE-2024-23225** / **CVE-2024-23296** |
| **iMessage Parsing** | BLASTPASS Exploit Chain | **CRITICAL** | ImageIO / PassKit Processing | Zero-click buffer overflow via malicious iMessage attachments, bypassing BlastDoor sandbox. | **CVE-2023-41064** / **CVE-2023-41061** |
| **Messaging & Fonts** | Operation Triangulation | **CRITICAL** | WebKit / FontParser / Kernel | Multi-stage zero-click chain using PDF/Font parsing and MMIO hardware register bypasses. | **CVE-2023-41993** / **CVE-2023-41991** |
| **WebKit Security** | WebKit Sandbox Escape | **CRITICAL** | WebKit Engine | Type confusion vulnerability enabling a remote attacker to break out of WebKit process boundaries. | **CVE-2023-32409** |
| **Graphics & Acceleration** | SurfaceRender UAF | **HIGH** | WebKit / IOSurfaceAccelerator | Use-after-free vulnerability leading to arbitrary code execution and kernel privilege escalation. | **CVE-2023-28205** / **CVE-2023-28206** |
| **Input / Hardware** | IOHIDKit Race Condition | **HIGH** | IOHIDKit Driver Subsystem | Race condition and UAF flaw enabling arbitrary code execution with kernel-level privileges. | **CVE-2022-42864** |
| **CoreGraphics / PDF** | FORCEDENTRY iMessage Exploit | **CRITICAL** | CoreGraphics / BlastDoor Sandbox | Zero-click integer overflow in CoreGraphics decoding malformed JBIG2 images inside PDFs. | **CVE-2021-30860** |
| **Wireless & Radio** | AWDL Proximity Over-the-Air | **HIGH** | Apple Wireless Direct Link (AWDL) | Buffer overflow in AWDL driver processing proximity Wi-Fi packets without user interaction. | **CVE-2021-30839** |
| **Kernel Subsystem** | Kernel Type Confusion LPE | **HIGH** | iOS Kernel Core | Type confusion vulnerability allowing sandboxed apps to execute code with kernel privileges. | **CVE-2021-1782** |
| **Mail Client** | MobileMail Sync Processing | **CRITICAL** | iOS MobileMail Client | Zero-click heap overflow in MIME parser triggered during automatic background email fetching. | **CVE-2020-9844** |