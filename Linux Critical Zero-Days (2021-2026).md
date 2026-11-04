# Critical Linux Zero-Day & Zero-Click Vulnerability Matrix (2021–2026)

This document provides a structured mapping of the most critical **zero-day and zero-click vulnerabilities** affecting the Linux kernel, core system daemons (`systemd`, `cups`), containers, and network subsystems.

---

## Vulnerability Overview Table

| Domain / Category | Vulnerability Name | Severity / CVSS | Primary Affected Component | Description & Attack Vector | Mapped Real-World CVE / Standard |
| :--- | :--- | :---: | :--- | :--- | :--- |
| **Print Subsystem** | CUPS Remote Code Execution | **CRITICAL** <br>`9.9` | `cups-browsed` / `cups-filters` | Zero-click unauthenticated RCE via UDP packet injection triggering malicious IPP printer discovery. | **CVE-2024-47176** / **CVE-2024-47177** *(CUPS RCE)* |
| **Network Stack** | Netfilter Out-of-Bounds Heap Writes | **CRITICAL** <br>`9.8` | Kernel `netfilter` Subsystem | Heap buffer overflow in Linux kernel packet filtering enabling remote code execution or local privilege escalation. | **CVE-2023-32233** / **CVE-2022-34918** |
| **Local Privilege Escalation** | Dirty Cred / Dirty Pipe LPE | **HIGH** <br>`7.8` | Linux Kernel Page Cache | Flaw in pipe buffer handling allowing unprivileged users to overwrite arbitrary read-only files and gain root privileges. | **CVE-2022-0847** *(Dirty Pipe)* |
| **System Daemon** | Polkit Pkexec Memory Corruption | **HIGH** <br>`7.8` | Polkit (`pkexec`) | Out-of-bounds memory corruption in `pkexec` allowing any local user to obtain root privileges instantly. | **CVE-2021-4034** *(Pkitexec / Pkexec)* |
| **Kernel Subsystem** | eBPF Memory Integrity Bypass | **HIGH** <br>`7.8` | Kernel eBPF Verifier | Flaws in eBPF verifier path analysis allowing local attackers to perform arbitrary kernel memory read/write operations. | **CVE-2023-2163** / **CVE-2021-3490** |
| **Container & Isolation** | runc Container Escape | **CRITICAL** <br>`8.6` | Container Runtime (`runc`) | Allows malicious containers to overwrite host `runc` binaries or access host file descriptors to achieve host root access. | **CVE-2024-21626** *(Leaky Vessels)* |
| **Crypto & SSH** | regreSSHion OpenSSH Pre-Auth RCE | **CRITICAL** <br>`8.1` | OpenSSH Server (`sshd`) | Signal handler race condition in OpenSSH daemon leading to unauthenticated remote code execution with root privileges. | **CVE-2024-6387** *(regreSSHion)* |
| **Filesystem / VFS** | OverlayFS Kernel Privilege Escalation | **HIGH** <br>`7.8` | OverlayFS Subsystem | Logic errors in OverlayFS file mapping allowing unprivileged local users to bypass security restrictions and escalate to root. | **CVE-2023-2640** / **CVE-2023-0386** |
| **Wireless / Bluetooth** | BlueZ / Wireless Subsystem Heap Overflow | **HIGH** <br>`7.8` | Kernel Wi-Fi & BlueZ Stack | Remote memory corruption via frame/packet processing in Linux Wi-Fi drivers and Bluetooth protocol stack. | **CVE-2022-41674** / **CVE-2020-12351** |
| **Supply Chain / Compression** | XZ Utils Backdoor | **CRITICAL** <br>`10.0` | `liblzma` / `sshd` integration | Malicious supply chain injection targeting `sshd` via `liblzma` to allow remote pre-authentication code execution. | **CVE-2024-3094** *(XZ Backdoor)* |

---

## Key Takeaways & Exploit Vector Trends

1. **System Service Exposure:** Zero-click vectors on Linux frequently target ambient network listeners (`cups-browsed`, `sshd`, Bluetooth/Wi-Fi drivers) rather than client-side media rendering engines.
2. **Local Privilege Escalation (LPE):** Unprivileged-to-root escalations heavily exploit kernel memory management features (eBPF, Page Cache, Netfilter) and ubiquitous setuid binaries (`pkexec`, `sudo`).
3. **Container Boundary Attacks:** Attacks against virtualization and container primitives (`runc`, OverlayFS) continue to be a primary focus for compromising cloud infrastructure and multi-tenant environments.