# InQtel Critical CVE Index (2021–2026)

<div align="center">

**Trey A. Smith · Authenticated, Inc. · [@ProjectZeroDays](https://github.com/ProjectZeroDays)**

**An indexed, collapsible vulnerability library for Windows, MacOS, Linux, Android, iOS, iPadOS, IoT, Automobiles, Residential/Commercial/Military Drones, Network Infrastructure, Industrial/Power/Nuclear Control Systems, Medical/Weaponized/Military Nano-Swarms, Commercial/Military Aircraft, Personal/Military Vehicles, and Air-Gapped Facilities (NIST 800-172 CMMC L3 enclaves).**

[![Version](https://img.shields.io/badge/PEGASUS-v1.7.1-00ff9c?style=for-the-badge&labelColor=0b0f0c)](.)
[![Scope](https://img.shields.io/badge/scope-authorized%20red%20team-00c8ff?style=for-the-badge&labelColor=0b0f0c)](.)
[![Target](https://img.shields.io/badge/target-Android%204.14%E2%80%9316-3ddc84?style=for-the-badge&labelColor=0b0f0c)](.)
[![Years](https://img.shields.io/badge/window-2021%E2%80%932026-ffd166?style=for-the-badge&labelColor=0b0f0c)](.)
[![Entries](https://img.shields.io/badge/entries-96-ff4d6d?style=for-the-badge&labelColor=0b0f0c)](.)
[![Frameworks](https://img.shields.io/badge/NIST-SP%20800--171%20%7C%20172-8a7dff?style=for-the-badge&labelColor=0b0f0c)](.)
[![License](https://img.shields.io/badge/license-research%20only-9aa0a6?style=for-the-badge&labelColor=0b0f0c)](.)

</div>

---

## ▸ Introduction

Pegasus is a host-side Android console. It enumerates USB, `adb`, `adbh`, mDNS and TCP transports, negotiates an authorised shell, drives `fastboot` with stock-partition rollback, and carries a payload set built around kernel correlation, an adb-TLS authentication bypass, and image-carrier delivery.

This document is the project's vulnerability library. It exists because the tool's detection logic is only as good as the CVE data behind it, and because operators running Pegasus against government and infrastructure targets kept asking the same question: *what else is on the board that the tool does not name yet?*

So the library holds three bodies of work in one place:

| Body | Origin | Purpose |
|---|---|---|
| **Mapped** | `KERNEL_CVES`, `f_exploit_payloads`, `f_notes` | Every CVE the console can already detect, generate for, or gate on |
| **Gap** | 2021–2026 critical-only research, government and infrastructure | What the console did not cover: edge appliances, identity, middleware, transfer |
| **Air-gap** | CMMC L3 / NIST SP 800-171–172 | What reaches an isolated enclave when there is no patch pipeline and no internet |

Air-gapped entries are not padding. Roughly a quarter of OT incidents start with removable media or a contractor laptop, and over half of USB-borne malware now targets the removable-media path specifically. An enclave with a six-month patch cycle and a USB port is a target class, not a corner case.

Nothing here is a PoC archive. It is a triage index: what the flaw is, what it touches, how bad it is, and whether the console already has a button for it.

---

## ▸ How to use this library

**Navigation.** Every row in the table of contents below is collapsible. Click the `▸` to unfold a section, click it again to fold it back. Click any CVE link inside a section to jump straight to that entry. Section headers and CVE entries in the body are collapsible too — same arrow, same behaviour.

**Reading an entry.**

```
▸ CVE-2022-0847 — DirtyPipe
   Severity   Critical / 7.8
   Affected   Linux 5.8 – 5.16.11 (Android 12–13 kernels)
   Impact     Arbitrary file write through a poisoned pipe buffer → root
   In tool    Option 114 — version gate plus on-device PoC build
```

**Status vocabulary.**

| Tag | Meaning |
|---|---|
| `MAPPED` | Detection or generation already implemented in Pegasus |
| `GAP` | Missing from the tool; reference entry, manual verification |
| `AIRGAP` | Reaches or persists in an isolated enclave |
| `KEV` | On the CISA Known Exploited Vulnerabilities catalog |

**Severity.** CVSS v3.1 or v4.0 as published. Entries with no score carry `—` and are ranked on exploitability and blast radius only.

**Rules of engagement.** Pegasus is written for authorised testing. Every kernel PoC compiles on-device and runs unprivileged; nothing here needs a signed boot image unless stated.

---

## ▸ Table of contents

<details>
<summary><b>▸ 1. Android platform &amp; media parsers</b> — 4 entries</summary>

- [CVE-2023-21268](#cve-2023-21268) — MediaCodec OOB read
- [CVE-2023-21282](#cve-2023-21282) — MediaCodec heap overflow
- [CVE-2023-45866](#cve-2023-45866) — Bluetooth HID injection, unauthenticated
- [CVE-2020-0022](#cve-2020-0022) — BlueFrag L2CAP ACL fragmentation

</details>

<details>
<summary><b>▸ 2. Android kernel local privilege escalation</b> — 6 entries</summary>

- [CVE-2022-0847](#cve-2022-0847) — DirtyPipe
- [CVE-2023-0386](#cve-2023-0386) — overlayfs copy-up ownership confusion
- [CVE-2024-1086](#cve-2024-1086) — nf_tables double free
- [CVE-2020-0423](#cve-2020-0423) — binder transaction UAF
- [CVE-2019-2215](#cve-2019-2215) — binder waitqueue UAF
- [CVE-2022-2588](#cve-2022-2588) — cls_route double free

</details>

<details>
<summary><b>▸ 3. Transport &amp; authentication layer</b> — 1 entry</summary>

- [CVE-2026-0073](#cve-2026-0073) — adbd TLS auth bypass via EVP_PKEY_cmp

</details>

<details>
<summary><b>▸ 4. Messaging &amp; zero-click delivery</b> — 10 entries</summary>

- [CVE-2023-34048](#cve-2023-34048) — malformed GIF / iMessage
- [CVE-2024-36991](#cve-2024-36991) — MP4 header corruption / WhatsApp
- [CVE-2023-41064](#cve-2023-41064) — WAV parsing / Facebook Messenger
- [CVE-2023-2569](#cve-2023-2569) — WhatsApp media parser
- [CVE-2023-47081](#cve-2023-47081) — iMessage attachment parser
- [CVE-2023-41991](#cve-2023-41991) — BlastDoor sandbox escape
- [CVE-2021-30860](#cve-2021-30860) — FORCEDENTRY PDF integer overflow
- [CVE-2023-32409](#cve-2023-32409) — WebKit sandbox escape
- [CVE-2022-42864](#cve-2022-42864) — WindowServer
- [CVE-2023-26818](#cve-2023-26818) — macOS TCC bypass

</details>

<details>
<summary><b>▸ 5. Browser &amp; rendering engines</b> — 6 entries</summary>

- [CVE-2022-3075](#cve-2022-3075) — WebKit JIT type confusion
- [CVE-2023-32373](#cve-2023-32373) — WebKit use-after-free
- [CVE-2023-28205](#cve-2023-28205) — WebKit type confusion
- [CVE-2023-4863](#cve-2023-4863) — libwebp heap overflow
- [CVE-2026-85046](#cve-2026-85046) — Chromium sandbox RCE
- [CVE-2026-20841](#cve-2026-20841) — Notepad Markdown command injection

</details>

<details>
<summary><b>▸ 6. Bluetooth, Wi-Fi &amp; radio</b> — 4 entries</summary>

- [CVE-2017-13077](#cve-2017-13077) — KRACK four-way handshake replay
- [CVE-2024-20023](#cve-2024-20023) — MediaTek Wi-Fi driver
- [CVE-2023-23392](#cve-2023-23392) — OBD-II CAN injection
- [CVE-2024-36946](#cve-2024-36946) — Ring / Nest authentication bypass

</details>

<details>
<summary><b>▸ 7. Industrial control &amp; OT</b> — 8 entries</summary>

- [CVE-2022-29951](#cve-2022-29951) — Modbus/TCP stack RCE
- [CVE-2021-32563](#cve-2021-32563) — Asterisk SIP INVITE heap overflow
- [CVE-2023-6448](#cve-2023-6448) — Unitronics PLC default credentials
- [CVE-2021-22681](#cve-2021-22681) — Rockwell Logix secret key recovery
- [CVE-2026-12569](#cve-2026-12569) — PTC Windchill / FlexPLM input validation
- [CVE-2026-110936](#cve-2026-110936) — Siemens Software Center search path
- [CVE-2026-106931](#cve-2026-106931) — EG SiteGuard OS command injection
- [AA26-097A](#aa26-097a) — water-sector PLC campaign (advisory)

</details>

<details>
<summary><b>▸ 8. Enterprise edge &amp; VPN appliances</b> — 19 entries</summary>

- [CVE-2026-88771](#cve-2026-88771) — NetScaler DTLS memory overflow
- [CVE-2026-88772](#cve-2026-88772) — NetScaler DTLS memory overflow
- [CVE-2026-88779](#cve-2026-88779) — NetScaler SAML memory overflow
- [CVE-2026-20349](#cve-2026-20349) — Cisco ASA / FTD heap inspection
- [CVE-2026-20122](#cve-2026-20122) — Cisco Catalyst SD-WAN Manager
- [CVE-2024-55591](#cve-2024-55591) — FortiOS / FortiProxy auth bypass
- [CVE-2025-24472](#cve-2025-24472) — FortiOS / FortiProxy spoofing
- [CVE-2022-42475](#cve-2022-42475) — FortiOS SSL-VPN heap overflow
- [CVE-2023-27997](#cve-2023-27997) — FortiGate XORtigate
- [CVE-2024-3400](#cve-2024-3400) — PAN-OS GlobalProtect command injection
- [CVE-2025-0108](#cve-2025-0108) — PAN-OS auth bypass
- [CVE-2025-0282](#cve-2025-0282) — Ivanti Connect Secure stack overflow
- [CVE-2024-21887](#cve-2024-21887) — Ivanti Connect Secure command injection
- [CVE-2023-4966](#cve-2023-4966) — Citrix Bleed
- [CVE-2025-5777](#cve-2025-5777) — CitrixBleed 2
- [CVE-2022-1388](#cve-2022-1388) — F5 BIG-IP iControl auth bypass
- [CVE-2023-36845](#cve-2023-36845) — Juniper Junos EX PHP variable
- [CVE-2024-24919](#cve-2024-24919) — Check Point Security Gateway
- [CVE-2024-40766](#cve-2024-40766) — SonicWall SSL-VPN

</details>

<details>
<summary><b>▸ 9. Identity, directory &amp; authentication services</b> — 8 entries</summary>

- [CVE-2026-54121](#cve-2026-54121) — AD CS "Certighost" domain takeover
- [CVE-2026-25177](#cve-2026-25177) — AD DS SPN/UPN validation
- [CVE-2026-27912](#cve-2026-27912) — Windows Kerberos privilege escalation
- [CVE-2026-41089](#cve-2026-41089) — Windows Netlogon RCE
- [CVE-2026-41096](#cve-2026-41096) — Windows DNS Client RCE
- [CVE-2026-32201](#cve-2026-32201) — Windows exploited-in-wild, CVSS 9.0
- [CVE-2022-26923](#cve-2022-26923) — Certifried
- [CVE-2021-42287](#cve-2021-42287) — sAMAccountName spoofing

</details>

<details>
<summary><b>▸ 10. Web, middleware &amp; file transfer</b> — 20 entries</summary>

- [CVE-2026-109618](#cve-2026-109618) — PHP unauthenticated RCE
- [CVE-2026-109619](#cve-2026-109619) — PHP unauthenticated RCE
- [CVE-2026-20253](#cve-2026-20253) — Splunk Enterprise missing auth
- [CVE-2026-42945](#cve-2026-42945) — NGINX, 0.6.27 → 1.30.0
- [CVE-2026-8053](#cve-2026-8053) — MongoDB RCE
- [CVE-2026-4670](#cve-2026-4670) — MOVEit Automation auth bypass
- [CVE-2026-5174](#cve-2026-5174) — MOVEit Automation privilege escalation
- [CVE-2025-10035](#cve-2025-10035) — GoAnywhere MFT deserialisation
- [CVE-2024-50623](#cve-2024-50623) — Cleo Harmony / VLTrader
- [CVE-2024-55956](#cve-2024-55956) — Cleo arbitrary file write
- [CVE-2023-34362](#cve-2023-34362) — MOVEit Transfer SQL injection
- [CVE-2023-0669](#cve-2023-0669) — GoAnywhere deserialisation
- [CVE-2021-44228](#cve-2021-44228) — Log4Shell
- [CVE-2022-22965](#cve-2022-22965) — Spring4Shell
- [CVE-2021-34473](#cve-2021-34473) — ProxyShell
- [CVE-2021-26855](#cve-2021-26855) — ProxyLogon
- [CVE-2022-26134](#cve-2022-26134) — Confluence OGNL injection
- [CVE-2023-22515](#cve-2023-22515) — Confluence privilege escalation
- [CVE-2025-53770](#cve-2025-53770) — SharePoint ToolShell
- [CVE-2024-6387](#cve-2024-6387) — regreSSHion

</details>

<details>
<summary><b>▸ 11. Air-gapped enclaves &amp; CMMC L3</b> — 12 entries</summary>

- [CVE-2025-4371](#cve-2025-4371) — BadUSB webcam firmware
- [CVE-2024-9680](#cve-2024-9680) — Firefox animation timeline
- [CVE-2023-38831](#cve-2023-38831) — WinRAR archive spoofing
- [CVE-2021-40444](#cve-2021-40444) — MSHTML ActiveX
- [CVE-2022-30190](#cve-2022-30190) — Follina MSDT
- [CVE-2024-21412](#cve-2024-21412) — SmartScreen bypass
- [CVE-2024-47176](#cve-2024-47176) — CUPS cups-browsed
- [CVE-2023-27350](#cve-2023-27350) — PaperCut NG/MF
- [CVE-2024-12356](#cve-2024-12356) — BeyondTrust PRA
- [CVE-2024-37085](#cve-2024-37085) — ESXi AD auth bypass
- [CVE-2025-22224](#cve-2025-22224) — VMware ESXi TOCTOU
- [CVE-2023-23397](#cve-2023-23397) — Outlook NTLM relay

</details>

<details>
<summary><b>▸ 12. Supply chain &amp; build systems</b> — 5 entries</summary>

- [CVE-2024-3094](#cve-2024-3094) — xz-utils backdoor
- [CVE-2025-30066](#cve-2025-30066) — tj-actions/changed-files
- [CVE-2023-38545](#cve-2023-38545) — curl SOCKS5 heap overflow
- [CVE-2024-23897](#cve-2024-23897) — Jenkins CLI file read
- [CVE-2023-42793](#cve-2023-42793) — TeamCity auth bypass

</details>

<details>
<summary><b>▸ 13. Reference</b></summary>

- [Priority ladder](#priority-ladder)
- [Pegasus option index](#pegasus-option-index)
- [Sources](#sources)
- [Credits &amp; disclaimer](#credits)

</details>

---

## ▸ 1. Android platform & media parsers

The parsers that run before any user interaction. All four reach the device without a tap and without a visible file.

<details>
<summary id="cve-2023-21268"><b>▸ CVE-2023-21268 — MediaCodec out-of-bounds read</b> &nbsp;<code>MAPPED</code> <code>GAP</code></summary>

| | |
|---|---|
| **Severity** | High — 7.8 |
| **Affected** | Android 11–14, `stsc` sample-to-chunk table |
| **Impact** | Corrupts the `stsc` box index; decoder reads past the table, crash or controlled read |
| **In tool** | Option 123 — malformed MP4 generator, corruption at offset `0x2C` |

A valid sample count followed by an invalid index is enough. Delivered as an attachment or a gallery file; the decoder does the rest.

</details>

<details>
<summary id="cve-2023-21282"><b>▸ CVE-2023-21282 — MediaCodec heap overflow</b> &nbsp;<code>GAP</code></summary>

| | |
|---|---|
| **Severity** | Critical — 9.8 |
| **Affected** | Android 10–14 media extractor |
| **Impact** | Heap overflow during container parse, potential RCE in `mediaextractor` |
| **In tool** | Reference only — generator covers the sibling `stsc` path |

Stagefright lineage. Same delivery profile as above, worse outcome.

</details>

<details>
<summary id="cve-2023-45866"><b>▸ CVE-2023-45866 — Bluetooth HID injection</b> &nbsp;<code>GAP</code> <code>AIRGAP</code></summary>

| | |
|---|---|
| **Severity** | High — 8.8 |
| **Affected** | Android 11–14, unpatched Bluetooth Classic stack |
| **Impact** | Unauthenticated HID keystroke injection over the air, no pairing |
| **In tool** | Reference only |

Proximity attack. In an enclave with Bluetooth peripherals, this is a keyboard that was never paired.

</details>

<details>
<summary id="cve-2020-0022"><b>▸ CVE-2020-0022 — BlueFrag</b> &nbsp;<code>MAPPED</code></summary>

| | |
|---|---|
| **Severity** | Critical — 8.8 |
| **Affected** | Android 8.0–9.0 |
| **Impact** | L2CAP ACL fragmentation overflow, RCE in the Bluetooth daemon, no user interaction |
| **In tool** | Option 123 — payload class mapped |

Older range, still live on legacy fleet hardware.

</details>

---

## ▸ 2. Android kernel local privilege escalation

The console correlates `uname -r` against these ranges at option 111 and builds a PoC on-device at option 116. Version gating is the real detector; the C source is a convenience.

<details>
<summary id="cve-2022-0847"><b>▸ CVE-2022-0847 — DirtyPipe</b> &nbsp;<code>MAPPED</code></summary>

| | |
|---|---|
| **Severity** | High — 7.8 |
| **Affected** | Linux 5.8 – 5.16.11, 5.15.25, 5.10.102 (Android 12–13 kernels) |
| **Impact** | Arbitrary file write by splicing into a pipe with stale `PIPE_BUF_FLAG_CAN_MERGE`, overwrite read-only pages → root |
| **In tool** | Option 114 — range gate, C PoC compiled on device, usage `./poc <file> <offset> <data>` |

No root needed to start. The classic target is a read-only `su` binary or `/system/etc/hosts`.

</details>

<details>
<summary id="cve-2023-0386"><b>▸ CVE-2023-0386 — overlayfs copy-up</b> &nbsp;<code>MAPPED</code></summary>

| | |
|---|---|
| **Severity** | High — 7.8 |
| **Affected** | Linux 5.11 – 6.2 |
| **Impact** | Ownership confusion on copy-up lets an unprivileged user mount a setuid binary owned by root |
| **In tool** | Option 115 — needs `unshare`/`mount` |

Requires user namespaces. Reliable where they are enabled; dead where they are not.

</details>

<details>
<summary id="cve-2024-1086"><b>▸ CVE-2024-1086 — nf_tables double free</b> &nbsp;<code>MAPPED</code></summary>

| | |
|---|---|
| **Severity** | High — 7.8 |
| **Affected** | Linux 5.14 – 6.7 |
| **Impact** | Double free in the nf_tables verdict path, page-level UAF → LPE |
| **In tool** | Option 116 — requires `CAP_NET_ADMIN` |

Excellent reliability on desktop Linux, narrower on Android where the netfilter surface is trimmed.

</details>

<details>
<summary id="cve-2020-0423"><b>▸ CVE-2020-0423 — binder transaction UAF</b> &nbsp;<code>MAPPED</code></summary>

| | |
|---|---|
| **Severity** | High — 7.8 |
| **Affected** | Android 10–13, kernels 4.14 – 5.9 |
| **Impact** | Race in binder transaction completion frees an in-flight buffer → UAF |
| **In tool** | Option 115 — C skeleton, race-dependent |

Weeks of uptime improve the odds. Patch level matters more than kernel string.

</details>

<details>
<summary id="cve-2019-2215"><b>
