# Critical Windows Zero-Day & Zero-Click Vulnerability Matrix (2021–2026)

This document provides a structured mapping of the most critical **zero-day and zero-click vulnerabilities** affecting Microsoft Windows client and server platforms over the last 5 years, highlighting high-impact exploit vectors across network protocols, core kernel drivers, security controls, and system services.

---

## Vulnerability Matrix

| Domain / Category | Vulnerability Name | Severity / CVSS | Primary Affected Component | Description & Attack Vector | Mapped Real-World CVE / Standard |
| :--- | :--- | :---: | :--- | :--- | :--- |
| **Network Protocols** | Pragmatic General Multicast RCE | **CRITICAL** <br>`9.8` | Windows PGM Driver (`pgm.sys`) / MSMQ | Zero-click remote code execution via malformed network packets sent to MSMQ service endpoints. | **CVE-2023-21554** *(QueueJumper)* |
| **Email & Office** | Outlook NTLM Credential Leak | **CRITICAL** <br>`9.8` | Microsoft Outlook / MAPI | Zero-click credential theft and authentication bypass via malformed email sound notification triggers. | **CVE-2023-23397** |
| **Remote Access** | RDP Gateway Service RCE | **CRITICAL** <br>`9.8` | Remote Desktop Gateway | Unauthenticated zero-click RCE via specially crafted connection requests to RDP services. | **CVE-2022-21893** / **CVE-2021-34535** |
| **File System / Web** | Windows HTTP Protocol Stack RCE | **CRITICAL** <br>`9.8` | `HTTP.sys` Web Server Driver | Unauthenticated zero-click RCE via malformed HTTP request headers processed by `HTTP.sys`. | **CVE-2022-21907** / **CVE-2021-31166** |
| **Print Spooler** | PrintNightmare RCE & LPE | **CRITICAL** <br>`8.8` | Windows Print Spooler Service | Remote code execution and system privilege escalation via RPC interface file execution. | **CVE-2021-34527** / **CVE-2021-1675** |
| **Authentication** | Kerberos KDC Privilege Escalation | **CRITICAL** <br>`8.8` | Active Directory / KDC | Unauthenticated privilege escalation allowing Domain Admin takeover via Kerberos ticket spoofing. | **CVE-2022-38023** / **CVE-2021-42278** |
| **Kernel / Driver** | Windows CLFS Driver LPE | **HIGH** <br>`7.8` | Common Log File System (`clfs.sys`) | Out-of-bounds write in `clfs.sys` enabling local privilege escalation from unprivileged user to `SYSTEM`. | **CVE-2023-28252** / **CVE-2022-24521** |
| **Diagnostics / Shell** | Follina MSDT Remote Code Execution | **HIGH** <br>`7.8` | Windows Diagnostics Tool (MSDT) | Remote code execution via malicious Office documents calling MSDT URIs without macro permissions. | **CVE-2022-30190** *(Follina)* |
| **Virtualization** | Hyper-V Host Compute Guest Escape | **CRITICAL** <br>`8.8` | Hyper-V VMM / Host Service | Virtual machine escape allowing arbitrary code execution in host kernel context via hypercalls. | **CVE-2023-21561** / **CVE-2021-31195** |
| **Security Bypasses** | SmartScreen / MOTW Bypass | **HIGH** <br>`7.5` | Windows SmartScreen / Mark-of-the-Web | Bypasses SmartScreen warning dialogs and MOTW security controls via malformed signatures or JS files. | **CVE-2023-26801** / **CVE-2022-44698** |

---

## Key Takeaways & Exploit Vector Trends

1. **Unauthenticated Zero-Click Attack Surface:** Drivers like `HTTP.sys`, `pgm.sys`, and services like Outlook/MSMQ represent the highest risk for zero-click compromises on Windows network perimeters.
2. **Kernel LPE Exploit Chains:** Local Privilege Escalation zero-days targeting `clfs.sys` and win32k drivers are heavily weaponized alongside browser and document-based initial access vectors.
3. **Identity & Active Directory Threats:** Vulnerabilities within Kerberos and domain authentication protocols continue to be the primary target for rapid enterprise post-exploitation domain compromise.