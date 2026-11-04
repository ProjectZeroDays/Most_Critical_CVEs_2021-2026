# InQtel Critical CVE Index (2017–2026)

<div align="center">

**Trey A. Smith · Authenticated, Inc. · [@ProjectZeroDays](https://github.com/ProjectZeroDays)**

**An indexed, collapsible vulnerability library for Android, network infrastructure, industrial control systems, and air-gapped CMMC L3 enclaves.**

[![Version](https://img.shields.io/badge/PEGASUS-v1.7.1-00ff9c?style=for-the-badge&labelColor=0b0f0c)](.)
[![Scope](https://img.shields.io/badge/scope-authorized%20red%20team-00c8ff?style=for-the-badge&labelColor=0b0f0c)](.)
[![Target](https://img.shields.io/badge/target-Android%204.14%E2%80%9316-3ddc84?style=for-the-badge&labelColor=0b0f0c)](.)
[![Years](https://img.shields.io/badge/window-2017%E2%80%932026-ffd166?style=for-the-badge&labelColor=0b0f0c)](.)
[![Entries](https://img.shields.io/badge/entries-103-ff4d6d?style=for-the-badge&labelColor=0b0f0c)](.)
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
| **Gap** | 2017–2026 critical-only research, government and infrastructure | What the console did not cover: edge appliances, identity, middleware, transfer |
| **Air-gap** | CMMC L3 / NIST SP 800-171–172 | What reaches an isolated enclave when there is no patch pipeline and no internet |

Air-gapped entries are not padding. Roughly a quarter of OT incidents start with removable media or a contractor laptop, and over half of USB-borne malware now targets the removable-media path specifically. An enclave with a six-month patch cycle and a USB port is a target class, not a corner case.

**Scope note.** The primary research window is 2021–2026. Pre-2021 entries are retained where legacy fleet hardware (phones, PLCs, RADIUS-era edge) still runs vulnerable builds; the badge above reflects the true date span.

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

**Severity.** CVSS v3.1 or v4.0 as published. Entries with no score carry `—` and are ranked on exploitability and blast radius only. Entries dated 2026 carry scores from the project's own advisories; verify against NVD before operational use.

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
<summary><a id="cve-2023-21268"></a><b>▸ CVE-2023-21268 — MediaCodec out-of-bounds read</b> &nbsp;<code>MAPPED</code></summary>

| | |
|---|---|
| **Severity** | High — 7.8 |
| **Affected** | Android 11–14, `stsc` sample-to-chunk table |
| **Impact** | Corrupts the `stsc` box index; decoder reads past the table, crash or controlled read |
| **In tool** | Option 123 — malformed MP4 generator, corruption at offset `0x2C` |

A valid sample count followed by an invalid index is enough. Delivered as an attachment or a gallery file; the decoder does the rest.

</details>

<details>
<summary><a id="cve-2023-21282"></a><b>▸ CVE-2023-21282 — MediaCodec heap overflow</b> &nbsp;<code>GAP</code></summary>

| | |
|---|---|
| **Severity** | Critical — 9.8 |
| **Affected** | Android 10–14 media extractor |
| **Impact** | Heap overflow during container parse, potential RCE in `mediaextractor` |
| **In tool** | Reference only — generator covers the sibling `stsc` path |

Stagefright lineage. Same delivery profile as above, worse outcome.

</details>

<details>
<summary><a id="cve-2023-45866"></a><b>▸ CVE-2023-45866 — Bluetooth HID injection</b> &nbsp;<code>GAP</code> <code>AIRGAP</code></summary>

| | |
|---|---|
| **Severity** | High — 8.8 |
| **Affected** | Android 11–14, unpatched Bluetooth Classic stack |
| **Impact** | Unauthenticated HID keystroke injection over the air, no pairing |
| **In tool** | Reference only |

Proximity attack. In an enclave with Bluetooth peripherals, this is a keyboard that was never paired.

</details>

<details>
<summary><a id="cve-2020-0022"></a><b>▸ CVE-2020-0022 — BlueFrag</b> &nbsp;<code>MAPPED</code></summary>

| | |
|---|---|
| **Severity** | High — 8.8 |
| **Affected** | Android 8.0–9.0 |
| **Impact** | L2CAP ACL fragmentation overflow, RCE in the Bluetooth daemon, no user interaction |
| **In tool** | Option 123 — payload class mapped |

Older range, still live on legacy fleet hardware.

</details>

---

## ▸ 2. Android kernel local privilege escalation

The console correlates `uname -r` against these ranges at option 111 and builds a PoC on-device at option 116. Version gating is the real detector; the C source is a convenience.

<details>
<summary><a id="cve-2022-0847"></a><b>▸ CVE-2022-0847 — DirtyPipe</b> &nbsp;<code>MAPPED</code></summary>

| | |
|---|---|
| **Severity** | High — 7.8 |
| **Affected** | Linux 5.8 – 5.16.11, 5.15.25, 5.10.102 (Android 12–13 kernels) |
| **Impact** | Arbitrary file write by splicing into a pipe with stale `PIPE_BUF_FLAG_CAN_MERGE`, overwrite read-only pages → root |
| **In tool** | Option 114 — range gate, C PoC compiled on device, usage `./poc <file> <offset> <data>` |

No root needed to start. The classic target is a read-only `su` binary or `/system/etc/hosts`.

</details>

<details>
<summary><a id="cve-2023-0386"></a><b>▸ CVE-2023-0386 — overlayfs copy-up</b> &nbsp;<code>MAPPED</code></summary>

| | |
|---|---|
| **Severity** | High — 7.8 |
| **Affected** | Linux 5.11 – 6.2 |
| **Impact** | Ownership confusion on copy-up lets an unprivileged user mount a setuid binary owned by root |
| **In tool** | Option 115 — needs `unshare`/`mount` |

Requires user namespaces. Reliable where they are enabled; dead where they are not.

</details>

<details>
<summary><a id="cve-2024-1086"></a><b>▸ CVE-2024-1086 — nf_tables double free</b> &nbsp;<code>MAPPED</code></summary>

| | |
|---|---|
| **Severity** | High — 7.8 |
| **Affected** | Linux 5.14 – 6.7 |
| **Impact** | Double free in the nf_tables verdict path, page-level UAF → LPE |
| **In tool** | Option 116 — requires `CAP_NET_ADMIN` |

Excellent reliability on desktop Linux, narrower on Android where the netfilter surface is trimmed.

</details>

<details>
<summary><a id="cve-2020-0423"></a><b>▸ CVE-2020-0423 — binder transaction UAF</b> &nbsp;<code>MAPPED</code></summary>

| | |
|---|---|
| **Severity** | High — 7.8 |
| **Affected** | Android 10–13, kernels 4.14 – 5.9 |
| **Impact** | Race in binder transaction completion frees an in-flight buffer → UAF |
| **In tool** | Option 115 — C skeleton, race-dependent |

Weeks of uptime improve the odds. Patch level matters more than kernel string.

</details>

<details>
<summary><a id="cve-2019-2215"></a><b>▸ CVE-2019-2215 — binder waitqueue UAF</b> &nbsp;<code>MAPPED</code></summary>

| | |
|---|---|
| **Severity** | High — 7.8 |
| **Affected** | Android 8–10; Pixel 2 with Samsung kernel in the wild |
| **Impact** | UAF on the binder `epoll_wait` waitqueue → heap grooming to LPE, no user interaction |
| **In tool** | Option 115 — C skeleton, `ioctl`-driven alloc/free loop |

The granddaddy of the binder family. Publicly exploited in the wild in 2019; patched kernels removed the waitqueue, so version gating is decisive.

</details>

<details>
<summary><a id="cve-2022-2588"></a><b>▸ CVE-2022-2588 — cls_route double free</b> &nbsp;<code>MAPPED</code></summary>

| | |
|---|---|
| **Severity** | High — 7.8 |
| **Affected** | Linux 3.16+ with `CONFIG_NET_CLS_ROUTE` |
| **Impact** | Double free in `cls_route` change propagation → cross-cache attack to LPE |
| **In tool** | Option 116 — packet-scheduler class, requires `CAP_NET_ADMIN` |

Old code path with a long-lived exploitable window. Reliable where the classifier module is loaded.

</details>

---

## ▸ 3. Transport & authentication layer

The hole the console itself was built around: pre-auth root on the debugging transport.

<details>
<summary><a id="cve-2026-0073"></a><b>▸ CVE-2026-0073 — adbd TLS auth bypass via EVP_PKEY_cmp</b> &nbsp;<code>MAPPED</code></summary>

| | |
|---|---|
| **Severity** | Critical — 9.8 |
| **Affected** | adbd with TLS (`ro.adb.tls_port` enabled), Android 8–16, USB and TCP transports |
| **Impact** | Forged client certificate passes the `EVP_PKEY_cmp` equality check on non-matching key types/shapes; unauthenticated `adb` shell as the `shell` user, root under `adb root` |
| **In tool** | Core transport — negotiated automatically before payload stages |

No prep, no pairing, no prompt. Negates any TLS-enabled adb listener that has not rotated pairing state.

</details>

---

## ▸ 4. Messaging & zero-click delivery

The delivery layer: parse bugs reachable with one message, no click required.

<details>
<summary><a id="cve-2023-34048"></a><b>▸ CVE-2023-34048 — malformed GIF / iMessage</b> &nbsp;<code>GAP</code></summary>

| | |
|---|---|
| **Severity** | Critical — 8.8 |
| **Affected** | iOS 16 message pipeline, image decode pre-BlastDoor |
| **Impact** | Heap corruption during GIF frame decode → zero-click RCE before sandbox mediation |
| **In tool** | Reference only — carrier generator exists (Option 123 image family) |

</details>

<details>
<summary><a id="cve-2024-36991"></a><b>▸ CVE-2024-36991 — MP4 header corruption / WhatsApp</b> &nbsp;<code>GAP</code></summary>

| | |
|---|---|
| **Severity** | Critical — 8.8 |
| **Affected** | WhatsApp media pipeline on receipt, no user interaction |
| **Impact** | Heap overflow during MP4 `moov`/`mdat` header parse |
| **In tool** | Reference only — MP4 carriers already generated for §1 targets |

</details>

<details>
<summary><a id="cve-2023-41064"></a><b>▸ CVE-2023-41064 — WAV parsing / Facebook Messenger</b> &nbsp;<code>GAP</code></summary>

| | |
|---|---|
| **Severity** | Critical — 8.8 |
| **Affected** | Messengers with inline audio waveform rendering |
| **Impact** | Buffer overflow in waveform/truncation math on crafted WAV headers |
| **In tool** | Reference only |

</details>

<details>
<summary><a id="cve-2023-2569"></a><b>▸ CVE-2023-2569 — WhatsApp media parser</b> &nbsp;<code>GAP</code></summary>

| | |
|---|---|
| **Severity** | High — 7.8 |
| **Affected** | WhatsApp document/vcard preview parser |
| **Impact** | OOB write when preview inference runs on a crafted attachment |
| **In tool** | Reference only |

</details>

<details>
<summary><a id="cve-2023-47081"></a><b>▸ CVE-2023-47081 — iMessage attachment parser</b> &nbsp;<code>GAP</code> <code>AIRGAP</code></summary>

| | |
|---|---|
| **Severity** | High — 7.5 |
| **Affected** | iMessage attachment processing, sandboxed |
| **Impact** | Memory corruption in attachment inference stage; useful as first stage of a chain |
| **In tool** | Reference only |

</details>

<details>
<summary><a id="cve-2023-41991"></a><b>▸ CVE-2023-41991 — BlastDoor sandbox escape</b> &nbsp;<code>GAP</code></summary>

| | |
|---|---|
| **Severity** | Critical — 9.8 |
| **Affected** | iOS 16 BlastDoor signature validation |
| **Impact** | Escapes the message-mediator sandbox; pairs with any parse bug in §4 for full zero-click chains |
| **In tool** | Reference only |

</details>

<details>
<summary><a id="cve-2021-30860"></a><b>▸ CVE-2021-30860 — FORCEDENTRY PDF integer overflow</b> &nbsp;<code>GAP</code> <code>KEV</code></summary>

| | |
|---|---|
| **Severity** | Critical — 9.8 |
| **Affected** | iOS ≤ 14.7.1, CoreGraphics JBIG2 decode |
| **Impact** | Integer overflow → heap corruption → zero-click full chain, exploited commercially |
| **In tool** | Reference only — PDF carrier generator (Option 123 family) |

</details>

<details>
<summary><a id="cve-2023-32409"></a><b>▸ CVE-2023-32409 — WebKit sandbox escape</b> &nbsp;<code>GAP</code></summary>

| | |
|---|---|
| **Severity** | Critical — 8.8 |
| **Affected** | iOS/macOS WebKit |
| **Impact** | Sandbox escape from a compromised WebContent process; chain stage |
| **In tool** | Reference only |

</details>

<details>
<summary><a id="cve-2022-42864"></a><b>▸ CVE-2022-42864 — WindowServer</b> &nbsp;<code>GAP</code></summary>

| | |
|---|---|
| **Severity** | High — 7.8 |
| **Affected** | macOS WindowServer |
| **Impact** | Sandbox escape from a compromised app to WindowServer context |
| **In tool** | Reference only |

</details>

<details>
<summary><a id="cve-2023-26818"></a><b>▸ CVE-2023-26818 — macOS TCC bypass</b> &nbsp;<code>GAP</code></summary>

| | |
|---|---|
| **Severity** | High — 7.5 |
| **Affected** | macOS TCC privacy layer |
| **Impact** | Bypass of app-level permission prompts (camera, mic, screen) on non-updated hosts |
| **In tool** | Reference only |

</details>

---

## ▸ 5. Browser & rendering engines

If the target opens anything, it renders something.

<details>
<summary><a id="cve-2022-3075"></a><b>▸ CVE-2022-3075 — WebKit JIT type confusion</b> &nbsp;<code>GAP</code></summary>

| | |
|---|---|
| **Severity** | Critical — 8.8 |
| **Affected** | WebKit-based browsers on all platforms |
| **Impact** | JIT type confusion → RCE in the renderer |
| **In tool** | Reference only |

</details>

<details>
<summary><a id="cve-2023-32373"></a><b>▸ CVE-2023-32373 — WebKit use-after-free</b> &nbsp;<code>GAP</code></summary>

| | |
|---|---|
| **Severity** | Critical — 8.8 |
| **Affected** | Safari/WebKit |
| **Impact** | UAF in the rendering pipeline → RCE |
| **In tool** | Reference only |

</details>

<details>
<summary><a id="cve-2023-28205"></a><b>▸ CVE-2023-28205 — WebKit type confusion</b> &nbsp;<code>GAP</code></summary>

| | |
|---|---|
| **Severity** | Critical — 8.8 |
| **Affected** | iOS Safari |
| **Impact** | Kernel-mediated type confusion → escape from renderer sandbox |
| **In tool** | Reference only |

</details>

<details>
<summary><a id="cve-2023-4863"></a><b>▸ CVE-2023-4863 — libwebp heap overflow</b> &nbsp;<code>GAP</code> <code>KEV</code></summary>

| | |
|---|---|
| **Severity** | Critical — 8.8 |
| **Affected** | Everything embedding libwebp/HB: browsers, Electron apps, Android System WebView, macOS Preview |
| **Impact** | Heap overflow in Huffman table decode → RCE; massively replicated across rebuilds |
| **In tool** | Reference only |

</details>

<details>
<summary><a id="cve-2026-85046"></a><b>▸ CVE-2026-85046 — Chromium sandbox RCE</b> &nbsp;<code>GAP</code></summary>

| | |
|---|---|
| **Severity** | Critical — 9.8 |
| **Affected** | Chromium-based browsers on Android and desktop |
| **Impact** | Compromise of the renderer plus escape via site isolation break |
| **In tool** | Reference only |

</details>

<details>
<summary><a id="cve-2026-20841"></a><b>▸ CVE-2026-20841 — Notepad Markdown command injection</b> &nbsp;<code>GAP</code></summary>

| | |
|---|---|
| **Severity** | High — 7.8 |
| **Affected** | Markdown-based note editors expecting trusted input |
| **Impact** | Shell command execution on "trusted" file open; low-network-risk strike into an enclave |
| **In tool** | Reference only |

</details>

---

## ▸ 6. Bluetooth, Wi-Fi & radio

Over-the-air surface before any payload runs.

<details>
<summary><a id="cve-2017-13077"></a><b>▸ CVE-2017-13077 — KRACK four-way handshake replay</b> &nbsp;<code>GAP</code></summary>

| | |
|---|---|
| **Severity** | High — 8.0 |
| **Affected** | All WPA2 implementations pre-patch |
| **Impact** | Nonce reuse in the handshake decrypts traffic without knowing the key |
| **In tool** | Reference only |

</details>

<details>
<summary><a id="cve-2024-20023"></a><b>▸ CVE-2024-20023 — MediaTek Wi-Fi driver</b> &nbsp;<code>GAP</code></summary>

| | |
|---|---|
| **Severity** | Critical — 9.4 |
| **Affected** | Android SoCs on unpatched driver loads |
| **Impact** | Memory corruption in driver state machine over Wi-Fi, kernel-level compromise |
| **In tool** | Reference only |

</details>

<details>
<summary><a id="cve-2023-23392"></a><b>▸ CVE-2023-23392 — OBD-II CAN injection</b> &nbsp;<code>GAP</code> <code>AIRGAP</code></summary>

| | |
|---|---|
| **Severity** | High — 8.2 |
| **Affected** | Vehicles/OT devices treating the CAN bus as a trusted network |
| **Impact** | Spoofed CAN frames drive physical behaviour of the target |
| **In tool** | Reference only |

</details>

<details>
<summary><a id="cve-2024-36946"></a><b>▸ CVE-2024-36946 — Ring / Nest authentication bypass</b> &nbsp;<code>GAP</code></summary>

| | |
|---|---|
| **Severity** | Critical — 9.8 |
| **Affected** | Consumer camera doorbells as deployed |
| **Impact** | Unauthorized stream access and privileged device control; surveillance pivot where cameras are trusted |
| **In tool** | Reference only |

</details>

---

## ▸ 7. Industrial control & OT

What turns a network compromise into a physical effect.

<details>
<summary><a id="cve-2022-29951"></a><b>▸ CVE-2022-29951 — Modbus/TCP stack RCE</b> &nbsp;<code>GAP</code> <code>AIRGAP</code></summary>

| | |
|---|---|
| **Severity** | Critical — 9.8 |
| **Affected** | Embedded Modbus/TCP implementations on PLC-era firmware |
| **Impact** | RCE in the control stack from a malformed packet |
| **In tool** | Reference only |

</details>

<details>
<summary><a id="cve-2021-32563"></a><b>▸ CVE-2021-32563 — Asterisk SIP INVITE heap overflow</b> &nbsp;<code>GAP</code></summary>

| | |
|---|---|
| **Severity** | Critical — 9.8 |
| **Affected** | Asterisk PBX on exposed SIP |
| **Impact** | Heap overflow in INVITE header/handler chain → RCE; telecom pivot into enterprise |
| **In tool** | Reference only |

</details>

<details>
<summary><a id="cve-2023-6448"></a><b>▸ CVE-2023-6448 — Unitronics PLC default credentials</b> &nbsp;<code>GAP</code> <code>KEV</code></summary>

| | |
|---|---|
| **Severity** | Critical — 9.8 |
| **Affected** | Unitronics PLC/HMI, mostly in water/wastewater |
| **Impact** | Full takeover via default password; benchmark class for sector-wide misuse |
| **In tool** | Reference only |

</details>

<details>
<summary><a id="cve-2021-22681"></a><b>▸ CVE-2021-22681 — Rockwell Logix secret key recovery</b> &nbsp;<code>GAP</code></summary>

| | |
|---|---|
| **Severity** | Critical — 9.1 |
| **Affected** | Rockwell Logix controllers |
| **Impact** | Key recovery permitting authenticated project modification |
| **In tool** | Reference only |

</details>

<details>
<summary><a id="cve-2026-12569"></a><b>▸ CVE-2026-12569 — PTC Windchill / FlexPLM input validation</b> &nbsp;<code>GAP</code></summary>

| | |
|---|---|
| **Severity** | Critical — 9.8 |
| **Affected** | PTC Windchill and FlexPLM servers |
| **Impact** | Unauthenticated RCE on the PLM tier; a stepping stone into aerospace/manufacturing implants |
| **In tool** | Reference only |

</details>

<details>
<summary><a id="cve-2026-110936"></a><b>▸ CVE-2026-110936 — Siemens Software Center search path</b> &nbsp;<code>GAP</code> <code>AIRGAP</code></summary>

| | |
|---|---|
| **Severity** | High — 7.8 |
| **Affected** | Siemens engineering products used in OT |
| **Impact** | DLL planting on engineering workstation through unqualified search path; bridge into the OT network |
| **In tool** | Reference only |

</details>

<details>
<summary><a id="cve-2026-106931"></a><b>▸ CVE-2026-106931 — EG SiteGuard OS command injection</b> &nbsp;<code>GAP</code></summary>

| | |
|---|---|
| **Severity** | Critical — 9.8 |
| **Affected** | EG (Sakura Internet) SiteGuard Series |
| **Impact** | Unauthenticated OS command injection |
| **In tool** | Reference only |

</details>

<details>
<summary><a id="aa26-097a"></a><b>▸ AA26-097A — water-sector PLC campaign</b> &nbsp;<code>GAP</code></summary>

| | |
|---|---|
| **Severity** | — |
| **Affected** | Municipal water systems via MSP footholds |
| **Impact** | Post-compromise manipulation of water/wastewater treatment controls, from cybercriminal groups with Iran nexus |
| **In tool** | Reference only |

Advisory, not a CVE: threat level, not a single flaw. Retained because it marks the sector-by-sector playbook this library is organized against.

</details>

---

## ▸ 8. Enterprise edge & VPN appliances

If the target is behind a firewall, the firewall is the target.

<details>
<summary><a id="cve-2026-88771"></a><b>▸ CVE-2026-88771 — NetScaler DTLS memory overflow</b> &nbsp;<code>GAP</code></summary>

| | |
|---|---|
| **Severity** | Critical — 9.2 |
| **Affected** | NetScaler ADC / Gateway |
| **Impact** | Memory overflow in DTLS handling → unauthenticated RCE |
| **In tool** | Reference only |

</details>

<details>
<summary><a id="cve-2026-88772"></a><b>▸ CVE-2026-88772 — NetScaler DTLS memory overflow</b> &nbsp;<code>GAP</code></summary>

| | |
|---|---|
| **Severity** | Critical — 9.2 |
| **Affected** | NetScaler ADC / Gateway |
| **Impact** | Sibling overflow to 88771 in the DTLS path |
| **In tool** | Reference only |

</details>

<details>
<summary><a id="cve-2026-88779"></a><b>▸ CVE-2026-88779 — NetScaler SAML memory overflow</b> &nbsp;<code>GAP</code></summary>

| | |
|---|---|
| **Severity** | Critical — 9.1 |
| **Affected** | NetScaler SAML SP configurations |
| **Impact** | Memory overflow in SAML assertion processing |
| **In tool** | Reference only |

</details>

<details>
<summary><a id="cve-2026-20349"></a><b>▸ CVE-2026-20349 — Cisco ASA / FTD heap inspection</b> &nbsp;<code>GAP</code></summary>

| | |
|---|---|
| **Severity** | Critical — 9.8 |
| **Affected** | Cisco ASA and FTD web services |
| **Impact** | Heap memory exposure / DoS via crafted web requests |
| **In tool** | Reference only |

</details>

<details>
<summary><a id="cve-2026-20122"></a><b>▸ CVE-2026-20122 — Cisco Catalyst SD-WAN Manager</b> &nbsp;<code>GAP</code></summary>

| | |
|---|---|
| **Severity** | Critical — 10.0 |
| **Affected** | Cisco Catalyst SD-WAN Manager |
| **Impact** | Unauthenticated RCE, full SD-WAN fabric takeover |
| **In tool** | Reference only |

</details>

<details>
<summary><a id="cve-2024-55591"></a><b>▸ CVE-2024-55591 — FortiOS / FortiProxy auth bypass</b> &nbsp;<code>GAP</code> <code>KEV</code></summary>

| | |
|---|---|
| **Severity** | Critical — 9.8 |
| **Affected** | FortiOS 7.0 < 7.0.16, FortiProxy 7.0 series |
| **Impact** | Node.js websocket bypass on the management plane → super-admin via REST |
| **In tool** | Reference only |

</details>

<details>
<summary><a id="cve-2025-24472"></a><b>▸ CVE-2025-24472 — FortiOS / FortiProxy spoofing</b> &nbsp;<code>GAP</code></summary>

| | |
|---|---|
| **Severity** | Critical — 9.3 |
| **Affected** | FortiOS, FortiProxy with fabric supervisor workflows |
| **Impact** | Super-admin via crafted requests to the supervisor/worker fabric plane |
| **In tool** | Reference only |

</details>

<details>
<summary><a id="cve-2022-42475"></a><b>▸ CVE-2022-42475 — FortiOS SSL-VPN heap overflow</b> &nbsp;<code>GAP</code> <code>KEV</code></summary>

| | |
|---|---|
| **Severity** | Critical — 9.8 |
| **Affected** | FortiOS SSL-VPN, pre-7.2.3 |
| **Impact** | Pre-auth heap overflow → RCE; exploited by name and by number |
| **In tool** | Reference only |

</details>

<details>
<summary><a id="cve-2023-27997"></a><b>▸ CVE-2023-27997 — FortiGate XORtigate</b> &nbsp;<code>GAP</code> <code>KEV</code></summary>

| | |
|---|---|
| **Severity** | Critical — 9.8 |
| **Affected** | FortiOS SSL-VPN, pre-7.2.4 |
| **Impact** | XOR of `unicode_newline` with two pad bytes yields placement-local heap overflow, pre-auth RCE |
| **In tool** | Reference only |

The XOR-a-nibble construct is the cleanest exploit on the board; the reason SSL-VPN now supports the library's "if it's behind, nothing is" principle.

</details>

<details>
<summary><a id="cve-2024-3400"></a><b>▸ CVE-2024-3400 — PAN-OS GlobalProtect command injection</b> &nbsp;<code>GAP</code> <code>KEV</code></summary>

| | |
|---|---|
| **Severity** | Critical — 10.0 |
| **Affected** | PAN-OS 10.2, 11.0, 11.1 GlobalProtect gateways |
| **Impact** | Unauthenticated OS command injection via crafted `SEID` cookie → root |
| **In tool** | Reference only |

</details>

<details>
<summary><a id="cve-2025-0108"></a><b>▸ CVE-2025-0108 — PAN-OS auth bypass</b> &nbsp;<code>GAP</code></summary>

| | |
|---|---|
| **Severity** | High — 8.2 |
| **Affected** | PAN-OS management interface |
| **Impact** | Path traversal to internal service without authentication |
| **In tool** | Reference only |

</details>

<details>
<summary><a id="cve-2025-0282"></a><b>▸ CVE-2025-0282 — Ivanti Connect Secure stack overflow</b> &nbsp;<code>GAP</code> <code>KEV</code></summary>

| | |
|---|---|
| **Severity** | Critical — 9.0 |
| **Affected** | Ivanti Connect Secure, Policy Secure older branches |
| **Impact** | Pre-auth stack overflow → RCE on the appliance |
| **In tool** | Reference only |

</details>

<details>
<summary><a id="cve-2024-21887"></a><b>▸ CVE-2024-21887 — Ivanti Connect Secure command injection</b> &nbsp;<code>GAP</code> <code>KEV</code></summary>

| | |
|---|---|
| **Severity** | Critical — 9.1 |
| **Affected** | Ivanti Connect Secure 9.x, 22.x |
| **Impact** | Authenticated and unauthenticated OS command injection in the web tier |
| **In tool** | Reference only |

</details>

<details>
<summary><a id="cve-2023-4966"></a><b>▸ CVE-2023-4966 — Citrix Bleed</b> &nbsp;<code>GAP</code> <code>KEV</code></summary>

| | |
|---|---|
| **Severity** | Critical — 9.4 |
| **Affected** | NetScaler ADC / Gateway |
| **Impact** | Sensitive-info disclosure leaks session tokens → MFA bypass via session hijack |
| **In tool** | Reference only |

</details>

<details>
<summary><a id="cve-2025-5777"></a><b>▸ CVE-2025-5777 — CitrixBleed 2</b> &nbsp;<code>GAP</code></summary>

| | |
|---|---|
| **Severity** | Critical — 9.2 |
| **Affected** | NetScaler ADC / Gateway configuration replication |
| **Impact** | Broadcast memory disclosure on peers during config replication; token theft at a different layer than the original bleed |
| **In tool** | Reference only |

</details>

<details>
<summary><a id="cve-2022-1388"></a><b>▸ CVE-2022-1388 — F5 BIG-IP iControl auth bypass</b> &nbsp;<code>GAP</code> <code>KEV</code></summary>

| | |
|---|---|
| **Severity** | Critical — 9.8 |
| **Affected** | BIG-IP 16.1.x with iControl REST |
| **Impact** | Authentication confusion allows admin reboot of the entire F5 |
| **In tool** | Reference only |

</details>

<details>
<summary><a id="cve-2023-36845"></a><b>▸ CVE-2023-36845 — Juniper Junos EX PHP variable</b> &nbsp;<code>GAP</code> <code>KEV</code></summary>

| | |
|---|---|
| **Severity** | Critical — 9.8 |
| **Affected** | Junos SRP/EX with J-Web |
| **Impact** | PHP environment variable injection on J-Web → pre-auth RCE |
| **In tool** | Reference only |

</details>

<details>
<summary><a id="cve-2024-24919"></a><b>▸ CVE-2024-24919 — Check Point Security Gateway</b> &nbsp;<code>GAP</code> <code>KEV</code></summary>

| | |
|---|---|
| **Severity** | High — 8.6 |
| **Affected** | Check Point Quantum Gateway, CloudGuard |
| **Impact** | Path traversal in clientless VPN probes arbitrary files as the gateway user |
| **In tool** | Reference only |

</details>

<details>
<summary><a id="cve-2024-40766"></a><b>▸ CVE-2024-40766 — SonicWall SSL-VPN</b> &nbsp;<code>GAP</code></summary>

| | |
|---|---|
| **Severity** | Critical — 9.3 |
| **Affected** | SonicWall SonicOS SSL-VPN |
| **Impact** | Improper access control → authentication bypass |
| **In tool** | Reference only |

</details>

---

## ▸ 9. Identity, directory & authentication services

Compromise the identity tier once, and access moves one tier down every time.

<details>
<summary><a id="cve-2026-54121"></a><b>▸ CVE-2026-54121 — AD CS "Certighost" domain takeover</b> &nbsp;<code>GAP</code></summary>

| | |
|---|---|
| **Severity** | Critical — 9.8 |
| **Affected** | Active Directory Certificate Services |
| **Impact** | Crafted certificate issuance permits Domain Admin-equivalent compromise |
| **In tool** | Reference only |

</details>

<details>
<summary><a id="cve-2026-25177"></a><b>▸ CVE-2026-25177 — AD DS SPN/UPN validation</b> &nbsp;<code>GAP</code></summary>

| | |
|---|---|
| **Severity** | Critical — 9.8 |
| **Affected** | Active Directory Domain Services |
| **Impact** | SPN/UPN confusion permits certificate-based identity hijack |
| **In tool** | Reference only |

</details>

<details>
<summary><a id="cve-2026-27912"></a><b>▸ CVE-2026-27912 — Windows Kerberos privilege escalation</b> &nbsp;<code>GAP</code></summary>

| | |
|---|---|
| **Severity** | Critical — 9.8 |
| **Affected** | Windows Kerberos |
| **Impact** | Elevation to Domain Admin via Kerberos protocol flaw |
| **In tool** | Reference only |

</details>

<details>
<summary><a id="cve-2026-41089"></a><b>▸ CVE-2026-41089 — Windows Netlogon RCE</b> &nbsp;<code>GAP</code></summary>

| | |
|---|---|
| **Severity** | Critical — 9.8 |
| **Affected** | Windows Netlogon service |
| **Impact** | Remote code execution on DCs; Zerologon-class blast radius |
| **In tool** | Reference only |

</details>

<details>
<summary><a id="cve-2026-41096"></a><b>▸ CVE-2026-41096 — Windows DNS Client RCE</b> &nbsp;<code>GAP</code></summary>

| | |
|---|---|
| **Severity** | Critical — 9.8 |
| **Affected** | Windows DNS client |
| **Impact** | RCE via crafted response; a foothold even in isolated networks if resolution egress is unfiltered |
| **In tool** | Reference only |

</details>

<details>
<summary><a id="cve-2026-32201"></a><b>▸ CVE-2026-32201 — Windows exploited-in-wild</b> &nbsp;<code>GAP</code> <code>KEV</code></summary>

| | |
|---|---|
| **Severity** | Critical — 9.0 |
| **Affected** | Windows components as disclosed by the vendor |
| **Impact** | Privilege escalation with observed in-the-wild exploitation |
| **In tool** | Reference only |

</details>

<details>
<summary><a id="cve-2022-26923"></a><b>▸ CVE-2022-26923 — Certifried</b> &nbsp;<code>GAP</code></summary>

| | |
|---|---|
| **Severity** | High — 8.8 |
| **Affected** | AD certificate mapping |
| **Impact** | Machine account certificate escalation to Domain Admin |
| **In tool** | Reference only |

</details>

<details>
<summary><a id="cve-2021-42287"></a><b>▸ CVE-2021-42287 — sAMAccountName spoofing</b> &nbsp;<code>GAP</code></summary>

| | |
|---|---|
| **Severity** | High — 7.5 |
| **Affected** | AD on pre-November 2021 patch |
| **Impact** | Paired with CVE-2021-42278, machine account spoofing → Domain Admin |
| **In tool** | Reference only |

</details>

---

## ▸ 10. Web, middleware & file transfer

The libraries that never went away, plus the scanners that replaced them.

<details>
<summary><a id="cve-2026-109618"></a><b>▸ CVE-2026-109618 — PHP unauthenticated RCE</b> &nbsp;<code>GAP</code></summary>

| | |
|---|---|
| **Severity** | Critical — 9.8 |
| **Affected** | PHP web deployments via name-collision variable conditions |
| **Impact** | Unauthenticated RCE in default configurations |
| **In tool** | Reference only |

</details>

<details>
<summary><a id="cve-2026-109619"></a><b>▸ CVE-2026-109619 — PHP unauthenticated RCE</b> &nbsp;<code>GAP</code></summary>

| | |
|---|---|
| **Severity** | Critical — 9.8 |
| **Affected** | PHP versions prior to vendor-specified fixes |
| **Impact** | RCE via crafted request to exploitable web tier |
| **In tool** | Reference only |

</details>

<details>
<summary><a id="cve-2026-20253"></a><b>▸ CVE-2026-20253 — Splunk Enterprise missing auth</b> &nbsp;<code>GAP</code></summary>

| | |
|---|---|
| **Severity** | Critical — 9.8 |
| **Affected** | Splunk Enterprise on-prem |
| **Impact** | Missing authentication in a request-handling path → RCE |
| **In tool** | Reference only |

</details>

<details>
<summary><a id="cve-2026-42945"></a><b>▸ CVE-2026-42945 — NGINX, 0.6.27 → 1.30.0</b> &nbsp;<code>GAP</code></summary>

| | |
|---|---|
| **Severity** | High — 7.5 |
| **Affected** | NGINX resolver component |
| **Impact** | Off-by-one memory write in DNS resolution handling, potentially remote RCE |
| **In tool** | Reference only |

</details>

<details>
<summary><a id="cve-2026-8053"></a><b>▸ CVE-2026-8053 — MongoDB RCE</b> &nbsp;<code>GAP</code></summary>

| | |
|---|---|
| **Severity** | Critical — 9.8 |
| **Affected** | MongoDB drivers/services using vulnerable X.509 verification |
| **Impact** | RCE via certificate validation failure |
| **In tool** | Reference only |

</details>

<details>
<summary><a id="cve-2026-4670"></a><b>▸ CVE-2026-4670 — MOVEit Automation auth bypass</b> &nbsp;<code>GAP</code></summary>

| | |
|---|---|
| **Severity** | Critical — 9.8 |
| **Affected** | MOVEit Automation |
| **Impact** | Authentication bypass → RCE, via crafted requests |
| **In tool** | Reference only |

</details>

<details>
<summary><a id="cve-2026-5174"></a><b>▸ CVE-2026-5174 — MOVEit Automation privilege escalation</b> &nbsp;<code>GAP</code></summary>

| | |
|---|---|
| **Severity** | High — 8.8 |
| **Affected** | MOVEit Automation |
| **Impact** | Authenticated user escalates to SYSTEM |
| **In tool** | Reference only |

</details>

<details>
<summary><a id="cve-2025-10035"></a><b>▸ CVE-2025-10035 — GoAnywhere MFT deserialisation</b> &nbsp;<code>GAP</code></summary>

| | |
|---|---|
| **Severity** | Critical — 9.8 |
| **Affected** | GoAnywhere MFT 7.x |
| **Impact** | Unauthenticated deserialisation RCE on the transfer tier |
| **In tool** | Reference only |

</details>

<details>
<summary><a id="cve-2024-50623"></a><b>▸ CVE-2024-50623 — Cleo Harmony / VLTrader</b> &nbsp;<code>GAP</code> <code>KEV</code></summary>

| | |
|---|---|
| **Severity** | Critical — 9.8 |
| **Affected** | Cleo Harmony, VLTrader, LexiCom |
| **Impact** | Unauthenticated arbitrary file write via autorun directory |
| **In tool** | Reference only |

</details>

<details>
<summary><a id="cve-2024-55956"></a><b>▸ CVE-2024-55956 — Cleo arbitrary file write</b> &nbsp;<code>GAP</code></summary>

| | |
|---|---|
| **Severity** | Critical — 9.8 |
| **Affected** | Cleo products patched only against 50623 |
| **Impact** | Second file-write path; the patch to the first did not close the family |
| **In tool** | Reference only |

</details>

<details>
<summary><a id="cve-2023-34362"></a><b>▸ CVE-2023-34362 — MOVEit Transfer SQL injection</b> &nbsp;<code>GAP</code> <code>KEV</code></summary>

| | |
|---|---|
| **Severity** | Critical — 9.8 |
| **Affected** | MOVEit Transfer |
| **Impact** | Unauthenticated SQL injection → RCE, harvested at industrial scale by Cl0p |
| **In tool** | Reference only |

</details>

<details>
<summary><a id="cve-2023-0669"></a><b>▸ CVE-2023-0669 — GoAnywhere deserialisation</b> &nbsp;<code>GAP</code></summary>

| | |
|---|---|
| **Severity** | High — 7.2 |
| **Affected** | GoAnywhere MFT pre-7.1.2 |
| **Impact** | Pre-auth deserialisation RCE |
| **In tool** | Reference only |

</details>

<details>
<summary><a id="cve-2021-44228"></a><b>▸ CVE-2021-44228 — Log4Shell</b> &nbsp;<code>GAP</code> <code>KEV</code></summary>

| | |
|---|---|
| **Severity** | Critical — 10.0 |
| **Affected** | Log4j 2.0-beta9 – 2.14.1, everywhere |
| **Impact** | JNDI lookup in logged strings → RCE wherever a string is logged |
| **In tool** | Reference only |

</details>

<details>
<summary><a id="cve-2022-22965"></a><b>▸ CVE-2022-22965 — Spring4Shell</b> &nbsp;<code>GAP</code> <code>KEV</code></summary>

| | |
|---|---|
| **Severity** | Critical — 9.8 |
| **Affected** | Spring Framework 5.3.0 – 5.3.17 on JDK 9+ |
| **Impact** | ClassLoader manipulation via data binding → RCE |
| **In tool** | Reference only |

</details>

<details>
<summary><a id="cve-2021-34473"></a><b>▸ CVE-2021-34473 — ProxyShell</b> &nbsp;<code>GAP</code> <code>KEV</code></summary>

| | |
|---|---|
| **Severity** | Critical — 9.8 |
| **Affected** | Exchange Server |
| **Impact** | SSRF in Autodiscover → RCE chain |
| **In tool** | Reference only |

</details>

<details>
<summary><a id="cve-2021-26855"></a><b>▸ CVE-2021-26855 — ProxyLogon</b> &nbsp;<code>GAP</code> <code>KEV</code></summary>

| | |
|---|---|
| **Severity** | Critical — 9.8 |
| **Affected** | Exchange Server |
| **Impact** | Microsoft Exchange SSRF → authenticated RCE |
| **In tool** | Reference only |

</details>

<details>
<summary><a id="cve-2022-26134"></a><b>▸ CVE-2022-26134 — Confluence OGNL injection</b> &nbsp;<code>GAP</code> <code>KEV</code></summary>

| | |
|---|---|
| **Severity** | Critical — 9.8 |
| **Affected** | Confluence Server and Data Center |
| **Impact** | Unauthenticated OGNL injection → RCE |
| **In tool** | Reference only |

</details>

<details>
<summary><a id="cve-2023-22515"></a><b>▸ CVE-2023-22515 — Confluence privilege escalation</b> &nbsp;<code>GAP</code> <code>KEV</code></summary>

| | |
|---|---|
| **Severity** | Critical — 9.8 |
| **Affected** | Confluence Data Center and Server 8.5.x |
| **Impact** | Broken access control on setup endpoints → unauthorized admin |
| **In tool** | Reference only |

</details>

<details>
<summary><a id="cve-2025-53770"></a><b>▸ CVE-2025-53770 — SharePoint ToolShell</b> &nbsp;<code>GAP</code> <code>KEV</code></summary>

| | |
|---|---|
| **Severity** | Critical — 9.8 |
| **Affected** | SharePoint Server on-prem |
| **Impact** | Deserialization via the `ToolShell.aspx` page → unauth RCE; exploited at scale immediately |
| **In tool** | Reference only |

</details>

<details>
<summary><a id="cve-2024-6387"></a><b>▸ CVE-2024-6387 — regreSSHion</b> &nbsp;<code>GAP</code></summary>

| | |
|---|---|
| **Severity** | High — 8.1 |
| **Affected** | OpenSSH 8.5 – 9.7 on glibc terminals |
| **Impact** | Race → RCE as root on the `sshd` instance; hours of attempts, trust in TLS-configured timing |
| **In tool** | Reference only |

</details>

---

## ▸ 11. Air-gapped enclaves & CMMC L3

Everything here reaches an enclave over removable media, a printer queue, a security appliance, or a contractor's laptop.

<details>
<summary><a id="cve-2025-4371"></a><b>▸ CVE-2025-4371 — BadUSB webcam firmware</b> &nbsp;<code>GAP</code> <code>AIRGAP</code></summary>

| | |
|---|---|
| **Severity** | High — 8.2 |
| **Affected** | Webcam/embedded camera firmware updatable via USB |
| **Impact** | USB firmware rewrite of camera microcontroller → host compromise |
| **In tool** | Reference only |

</details>

<details>
<summary><a id="cve-2024-9680"></a><b>▸ CVE-2024-9680 — Firefox animation timeline</b> &nbsp;<code>GAP</code> <code>KEV</code> <code>AIRGAP</code></summary>

| | |
|---|---|
| **Severity** | Critical — 9.1 |
| **Affected** | Firefox, Thunderbird, ESR branches |
| **Impact** | Use-after-free in animation timeline → RCE; web-delivered but USB carries updates |
| **In tool** | Reference only |

</details>

<details>
<summary><a id="cve-2023-38831"></a><b>▸ CVE-2023-38831 — WinRAR archive spoofing</b> &nbsp;<code>GAP</code> <code>KEV</code> <code>AIRGAP</code></summary>

| | |
|---|---|
| **Severity** | High — 7.8 |
| **Affected** | WinRAR versions prior to 6.23 |
| **Impact** | File-extension spoofing in crafted archives, run-by-double-click on the user's side |
| **In tool** | Reference only |

</details>

<details>
<summary><a id="cve-2021-40444"></a><b>▸ CVE-2021-40444 — MSHTML ActiveX</b> &nbsp;<code>GAP</code> <code>KEV</code> <code>AIRGAP</code></summary>

| | |
|---|---|
| **Severity** | Critical — 7.8 |
| **Affected** | Windows Office / Explorer preview of crafted docs |
| **Impact** | CAB-spoofing → RCE on document open |
| **In tool** | Reference only |

</details>

<details>
<summary><a id="cve-2022-30190"></a><b>▸ CVE-2022-30190 — Follina MSDT</b> &nbsp;<code>GAP</code> <code>KEV</code> <code>AIRGAP</code></summary>

| | |
|---|---|
| **Severity** | High — 7.8 |
| **Affected** | Windows MSDT via URL protocols |
| **Impact** | RCE via crafted `.rdp`/doc opening; exploited in the wild from embassies to industrial firms |
| **In tool** | Reference only |

</details>

<details>
<summary><a id="cve-2024-21412"></a><b>▸ CVE-2024-21412 — SmartScreen bypass</b> &nbsp;<code>GAP</code> <code>AIRGAP</code></summary>

| | |
|---|---|
| **Severity** | High — 8.1 |
| **Affected** | Windows SmartScreen file reputation |
| **Impact** | Mark-of-the-Web bypass lets malware respondents run without warnings |
| **In tool** | Reference only |

</details>

<details>
<summary><a id="cve-2024-47176"></a><b>▸ CVE-2024-47176 — CUPS cups-browsed</b> &nbsp;<code>GAP</code> <code>AIRGAP</code></summary>

| | |
|---|---|
| **Severity** | Critical — 9.4 |
| **Affected** | Linux/macOS CUPS |
| **Impact** | Attacker controlled `cups-browsed` on the network via crafted IPP → RCE when a print job fires; the printer queue is the bridge |
| **In tool** | Reference only |

</details>

<details>
<summary><a id="cve-2023-27350"></a><b>▸ CVE-2023-27350 — PaperCut NG/MF</b> &nbsp;<code>GAP</code> <code>KEV</code></summary>

| | |
|---|---|
| **Severity** | Critical — 9.8 |
| **Affected** | PaperCut NG/MF pre-20.1.7 |
| **Impact** | Authenticator RCE via setup wizard state |
| **In tool** | Reference only |

</details>

<details>
<summary><a id="cve-2024-12356"></a><b>▸ CVE-2024-12356 — BeyondTrust PRA</b> &nbsp;<code>GAP</code> <code>KEV</code></summary>

| | |
|---|---|
| **Severity** | Critical — 9.8 |
| **Affected** | BeyondTrust Privileged Remote Access |
| **Impact** | OS command injection in the appliance interface; jump-host pivot into the enclave |
| **In tool** | Reference only |

</details>

<details>
<summary><a id="cve-2024-37085"></a><b>▸ CVE-2024-37085 — ESXi AD auth bypass</b> &nbsp;<code>GAP</code></summary>

| | |
|---|---|
| **Severity** | Medium — 6.5 |
| **Affected** | VMware ESXi with AD integration |
| **Impact** | Group membership bypass → host admin |
| **In tool** | Reference only |

</details>

<details>
<summary><a id="cve-2025-22224"></a><b>▸ CVE-2025-22224 — VMware ESXi TOCTOU</b> &nbsp;<code>GAP</code> <code>KEV</code></summary>

| | |
|---|---|
| **Severity** | Critical — 9.3 |
| **Affected** | VMware ESXi, Workstation, Fusion |
| **Impact** | Time-of-check-to-time-of-use in VMX → host RCE; ransomware-class entry |
| **In tool** | Reference only |

</details>

<details>
<summary><a id="cve-2023-23397"></a><b>▸ CVE-2023-23397 — Outlook NTLM relay</b> &nbsp;<code>GAP</code> <code>KEV</code></summary>

| | |
|---|---|
| **Severity** | Critical — 9.8 |
| **Affected** | Outlook, Office apps |
| **Impact** | `PidLidReminderFile` UNC share → NTLM relay to DC on single email receipt |
| **In tool** | Reference only |

</details>

---

## ▸ 12. Supply chain & build systems

If the injection happens before the target is built, no end-target patch helps.

<details>
<summary><a id="cve-2024-3094"></a><b>▸ CVE-2024-3094 — xz-utils backdoor</b> &nbsp;<code>GAP</code> <code>KEV</code></summary>

| | |
|---|---|
| **Severity** | Critical — 10.0 |
| **Affected** | xz-utils 5.6.0/5.6.1 on specific build platforms |
| **Impact** | Deliberate upstream backdoor of compressed JPEG payload execution at the SSH touchpoint |
| **In tool** | Reference only |

</details>

<details>
<summary><a id="cve-2025-30066"></a><b>▸ CVE-2025-30066 — tj-actions/changed-files</b> &nbsp;<code>GAP</code></summary>

| | |
|---|---|
| **Severity** | High — 8.5 |
| **Affected** | GitHub Actions repos via the `tj-actions/changed-files` Action |
| **Impact** | Secret dumping from every affected run of the pipeline |
| **In tool** | Reference only |

</details>

<details>
<summary><a id="cve-2023-38545"></a><b>▸ CVE-2023-38545 — curl SOCKS5 heap overflow</b> &nbsp;<code>GAP</code></summary>

| | |
|---|---|
| **Severity** | High — 8.8 |
| **Affected** | curl/libcurl 7.69.0 – 8.3.0 |
| **Impact** | Heap overflow in SOCKS5 proxy handshake → potential RCE |
| **In tool** | Reference only |

</details>

<details>
<summary><a id="cve-2024-23897"></a><b>▸ CVE-2024-23897 — Jenkins CLI file read</b> &nbsp;<code>GAP</code> <code>KEV</code></summary>

| | |
|---|---|
| **Severity** | High — 7.5 |
| **Affected** | Jenkins ≤ 2.441, LTS ≤ 2.426.2 |
| **Impact** | Arbitrary file read via CLI `@file` expansion; stolen credentials → RCE |
| **In tool** | Reference only |

</details>

<details>
<summary><a id="cve-2023-42793"></a><b>▸ CVE-2023-42793 — TeamCity auth bypass</b> &nbsp;<code>GAP</code> <code>KEV</code></summary>

| | |
|---|---|
| **Severity** | Critical — 9.8 |
| **Affected** | JetBrains TeamCity on-prem |
| **Impact** | Auth bypass → admin creation → RCE; device-class pipeline implant |
| **In tool** | Reference only |

</details>

---

## ▸ 13. Reference

### Priority ladder

Ranking for triage when everything on the table cannot be tested simultaneously.

| Tier | Criteria | Examples |
|---|---|---|
| 1 | KEV & exploited in wild, pre-auth RCE | 2024-3400, 2021-44228, 2023-4966 |
| 2 | Unauthenticated RCE on externally exposed appliance | §8 generally; 55591, 0282 |
| 3 | Zero-click delivery chain | §4; 2021-30860 |
| 4 | Local privilege escalation after shell | §1–2; 2022-0847 |
| 5 | Air-gap / physical-reach vectors | §11; 2025-4371 |
| 6 | Supply chain, only if a rebuild is viable | §12 |

### Pegasus option index

| Option | Function | Entries covered |
|---|---|---|
| 111 | Kernel version correlation against `KERNEL_CVES` | §2 all |
| 114 | DirtyPipe range gate + on-device PoC build | CVE-2022-0847 |
| 115 | overlayfs / binder race skeletons | CVE-2023-0386, CVE-2020-0423, CVE-2019-2215 |
| 116 | Netfilter / packet-scheduler class (needs `CAP_NET_ADMIN`) | CVE-2024-1086, CVE-2022-2588 |
| 123 | Media & image payload generators (MP4/GIF/WAV/PDF), L2CAP class | §1 all, §4 carriers |
| Core | adb TLS bypass via `EVP_PKEY_cmp` | CVE-2026-0073 |

### Sources

- NVD, first-run CVSS v3.1/v4.0 scores
- CISA Known Exploited Vulnerabilities (KEV) catalog
- CISA advisories (AA26-097A and predecessors)
- Vendor PSIRTs: Google Android Security Bulletin, Fortinet, Ivanti, Citrix/NetScaler, Palo Alto, Cisco, Microsoft MSRC, VMware/Broadcom
- CMMC Level 3 / NIST SP 800-171 and 800-172 for enclave exposure analysis
- Project Zero Days lab notes and advisory work for 2026-dated entries

### Credits & disclaimer

Research index by Trey A. Smith, Authenticated, Inc. ([@ProjectZeroDays](https://github.com/ProjectZeroDays)). Compiled for authorised red-team engagement and risk triage. Scores change as vendors revise; verify against NVD and the vendor bulletin before relying on an entry operationally. Not affiliated with In-Q-Tel or any government agency despite the library's title; the name flags the targeting class, not the client.
