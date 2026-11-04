# Critical Vulnerability & Threat-Surface Matrices (2021–2026)

<div align="center">

**Trey A. Smith · Authenticated, Inc. · [@ProjectZeroDays](https://github.com/ProjectZeroDays)**

**A cross-domain research collection spanning operating systems, connected devices, industrial control, transportation, aerospace, defense, and emerging technologies.**

[![Scope](https://img.shields.io/badge/scope-defensive%20security%20research-00c8ff?style=for-the-badge&labelColor=0b0f0c)](.)
[![Window](https://img.shields.io/badge/window-2021%E2%80%932026-ffd166?style=for-the-badge&labelColor=0b0f0c)](.)
[![Matrices](https://img.shields.io/badge/matrices-18-ff4d6d?style=for-the-badge&labelColor=0b0f0c)](.)
[![Coverage](https://img.shields.io/badge/coverage-IT%20%7C%20OT%20%7C%20cyber--physical-8a7dff?style=for-the-badge&labelColor=0b0f0c)](.)
[![Format](https://img.shields.io/badge/format-research%20reference-9aa0a6?style=for-the-badge&labelColor=0b0f0c)](.)

</div>

---

## ▸ Introduction

This repository is a collection of 18 Markdown vulnerability and threat-surface matrices. It is **not limited to Android or mobile devices**: the documents cover consumer and enterprise software, embedded and connected products, industrial environments, vehicles, aircraft, drones, satellites, military systems, and emerging cyber-physical technologies.

Each matrix organizes risks for a technology area, typically describing vulnerability classes or threat scenarios, affected components and systems, attack context, severity where provided, and CVE or standards references where available. Coverage includes both conventional software vulnerabilities and broader operational or physical threat surfaces, such as wireless protocols, firmware, supply chains, sensors, and control systems.

The collection is a research reference—not an executable tool, scanner, verified vulnerability database, or archive of proof-of-concept code. Some entries map to published CVEs; others are generalized, emerging, or illustrative scenarios without a public CVE. A CVE or severity label appearing here is not, by itself, independent confirmation of affected products, exploitability, or real-world use. Verify details against authoritative vendor advisories, CVE records, and applicable safety guidance before relying on them.

Use these documents for defensive orientation, asset inventory, and research planning. Apply findings only to systems you own or are explicitly authorized to assess, and account for operational safety requirements—especially in industrial, transportation, aerospace, medical, and other cyber-physical environments.

---

## ▸ How to use this repository

- Expand the table of contents and choose a system or domain.
- Open its matrix to review the overview table and key takeaways. Document formats vary, but entries commonly identify components, attack context, severity, and CVE or standards references.
- Treat product and platform names as scope indicators, not proof that every version or deployment is vulnerable.
- Confirm affected versions, scores, mitigations, and references using primary sources. Prioritize environment-specific risk and safety assessment.

### Evidence and terminology

The matrices vary in specificity and evidence depth. Terms such as “zero-day,” “zero-click,” and severity ratings reflect the language used in an individual document and should not be read as independent validation. Some entries are threat models rather than claims about a specific, assigned CVE. Not every scenario has a CVE or CVSS score.

---

## ▸ Table of contents

<details>
<summary><b>▸ 1. End-user operating systems</b> — 5 matrices</summary>

- [Android](#1-android)
- [iOS](#2-ios)
- [macOS](#3-macos)
- [Windows](#4-windows)
- [Linux](#5-linux)

</details>

<details>
<summary><b>▸ 2. Connected and embedded devices</b> — 5 matrices</summary>

- [Internet of Things and smart home](#6-internet-of-things-and-smart-home)
- [Smart cameras and monitors](#7-smart-cameras-and-monitors)
- [Smart TVs](#8-smart-tvs)
- [Automotive and connected vehicles](#9-automotive-and-connected-vehicles)
- [Commercial and military drones](#10-commercial-and-military-drones)

</details>

<details>
<summary><b>▸ 3. Industrial, aerospace, and defense systems</b> — 6 matrices</summary>

- [SCADA, PLC, and industrial control](#11-scada-plc-and-industrial-control)
- [Commercial and military avionics](#12-commercial-and-military-avionics)
- [Military drones and tactical UAS](#13-military-drones-and-tactical-uas)
- [Military vehicles and armored platforms](#14-military-vehicles-and-armored-platforms)
- [Military AI systems](#15-military-ai-systems)
- [Commercial and military satellites](#16-commercial-and-military-satellites)

</details>

<details>
<summary><b>▸ 4. Emerging and specialized technologies</b> — 2 matrices</summary>

- [Nanotechnology and bio-cyber interfaces](#17-nanotechnology-and-bio-cyber-interfaces)
- [Military nanotechnology and weaponized nanosystems](#18-military-nanotechnology-and-weaponized-nanosystems)

</details>

<details>
<summary><b>▸ 5. Reference</b></summary>

- [Coverage at a glance](#coverage-at-a-glance)
- [Research and verification notes](#research-and-verification-notes)
- [Disclaimer](#disclaimer)

</details>

---

## ▸ 1. End-user operating systems

### <a id="1-android"></a>1. Android

[Open the Android vulnerability matrix](Android%20Critical%20Zero-Days%20(2021-2026).md)

**Systems and components covered:** Android Framework and system services; Linux kernel and USB/audio drivers; MediaCodec and media/image parsing (`libwebp`); Bluetooth stack and HID; Arm Mali GPU drivers; ActivityManager and intent handling.

### <a id="2-ios"></a>2. iOS

[Open the iOS vulnerability matrix](iOS%20Critical%20Zero-Days%20(2021-2026)%20(2).md)

**Systems and components covered:** iOS kernel and RTKit coprocessor; iMessage, BlastDoor, PassKit, and Mail; ImageIO, CoreGraphics, PDF and font parsing; WebKit; IOSurfaceAccelerator and IOHIDKit; Apple Wireless Direct Link (AWDL).

### <a id="3-macos"></a>3. macOS

[Open the macOS vulnerability matrix](macOS%20Critical%20Zero-Days%20(2021-2026).md)

**Systems and components covered:** WindowServer and IPC; Gatekeeper, Finder, LaunchServices, and Archive Utility; Transparency, Consent, and Control (TCC); IOHIDFamily and Apple GPU drivers; ImageIO, CoreGraphics, and WebKit; AirDrop/AWDL; Screen Sharing/Apple Remote Desktop; Apple Silicon boot and Secure Enclave.

### <a id="4-windows"></a>4. Windows

[Open the Windows vulnerability matrix](Windows%20Critical%20Zero-Days%20(2021-2026).md)

**Systems and components covered:** Windows client and server; PGM/`pgm.sys` and MSMQ; Outlook/MAPI; Remote Desktop Gateway; HTTP.sys; Print Spooler; Active Directory and Kerberos KDC; CLFS; MSDT; Hyper-V; SmartScreen and Mark-of-the-Web.

### <a id="5-linux"></a>5. Linux

[Open the Linux vulnerability matrix](Linux%20Critical%20Zero-Days%20(2021-2026).md)

**Systems and components covered:** Linux kernel, netfilter, eBPF, OverlayFS, and page cache; CUPS (`cups-browsed`, `cups-filters`); polkit/`pkexec`; `runc` and container isolation; OpenSSH/`sshd`; BlueZ and wireless drivers; xz-utils/`liblzma` supply chain.

---

## ▸ 2. Connected and embedded devices

### <a id="6-internet-of-things-and-smart-home"></a>6. Internet of Things and smart home

[Open the IoT and smart-home matrix](IoT%20Critical%20Zero-Days%20(2021-2026)%20(1).md)

**Systems and devices covered:** SmartThings, Home Assistant, and Hubitat hubs; Zigbee, Z-Wave, Matter, and Thread; OpenThread border routers; AWS IoT Greengrass and Azure IoT Edge; smart meters using ANSI C12.22 or DLMS/COSEM; embedded web servers and UPnP; smart speakers and assistants; HVAC, locks, and firmware/SDK supply chains.

### <a id="7-smart-cameras-and-monitors"></a>7. Smart cameras and monitors

[Open the smart-camera matrix](Smart%20Camera%20Critical%20Zero-Days%20(2021-2026).md)

**Systems and devices covered:** Flock/LPR gateways; Ring and cloud cameras; Dahua and Hikvision ONVIF cameras; Axis, Hanwha, and Sunell PTZ cameras; Owlet, Nanit, and VTech baby monitors; RTSP/SIP media services; Wi-Fi Direct and cloud relays; Realtek/MediaTek firmware; Reolink, Lorex, and Amcrest NVRs; UART, JTAG, and SPI flash interfaces.

### <a id="8-smart-tvs"></a>8. Smart TVs

[Open the smart-TV matrix](Smart%20TV%20Critical%20Zero-Days%20(2021-2026).md)

**Systems and devices covered:** Samsung Tizen, LG webOS, Android TV/Google TV, and Fire OS; browser and rendering engines; system/account services; Wi-Fi and Bluetooth firmware; voice/audio subsystems; UPnP/DLNA media servers; Miracast, AirPlay, and Chromecast receivers; ADB/SystemUI; HDMI-CEC; Widevine/PlayReady and trusted execution environments.

### <a id="9-automotive-and-connected-vehicles"></a>9. Automotive and connected vehicles

[Open the automotive matrix](Automotive%20Critical%20Zero-Days%20(2021-2026).md)

**Systems and devices covered:** Telematics control units and cellular basebands; OEM cloud APIs and companion-app backends; central gateway ECUs and CAN; Android Automotive/QNX infotainment; passive keyless entry, UWB, and BLE; EV charging and ISO 15118/CCS; OTA update clients and signing hardware; DSRC/C-V2X; OBD-II/UDS diagnostics; hardware security modules.

### <a id="10-commercial-and-military-drones"></a>10. Commercial and military drones

[Open the commercial, enterprise, and military drone matrix](Drone%20Critical%20Zero-Days%20%26%20Exploit%20Matrix%20(2021-2026).md)

**Systems and devices covered:** UAV command-and-control links and MAVLink; QGroundControl and Mission Planner; GNSS, optical-flow, and lidar sensors; Remote ID over Wi-Fi/Bluetooth; PX4 and ArduPilot flight controllers; FPV/HD video links; OEM cloud and OTA services; ROS/ROS 2 and Jetson companion computers; battery-management systems; CAN buses and electronic speed controllers.

---

## ▸ 3. Industrial, aerospace, and defense systems

### <a id="11-scada-plc-and-industrial-control"></a>11. SCADA, PLC, and industrial control

[Open the SCADA/PLC/ICS matrix](SCADA,%20PLC%20%26%20Industrial%20Control%20Critical%20Zero-Days%20(2021-2026).md)

**Systems and devices covered:** CODESYS and MicroLogix PLC runtimes; engineering workstations and ladder logic; Modbus TCP, S7Comm, and DNP3; safety instrumented systems (SIS); HMI and SCADA consoles; RTUs and smart-grid equipment; IEC 61850 GOOSE; turbine controls and DCS; Profibus/CANopen serial bridges.

### <a id="12-commercial-and-military-avionics"></a>12. Commercial and military avionics

[Open the avionics and aeronautics matrix](Commercial%20%26%20Military%20Avionics%20Critical%20Vulnerabilities%20(2021-2026).md)

**Systems and devices covered:** Flight management systems and ARINC 424 navigation data; in-flight entertainment and airborne network gateways; ACARS and VDL; ADS-B; radio altimeters; electronic flight bags; ARINC 429 buses; gatelink and wireless quick-access recorders; maintenance data links.

### <a id="13-military-drones-and-tactical-uas"></a>13. Military drones and tactical UAS

[Open the military-drone and tactical-UAS matrix](Military%20Drone%20Critical%20Zero-Days%20%26%20Exploit%20Matrix%20(2021-2026).md)

**Systems and devices covered:** Tactical UAS command/data links, CDL, and Link 16; STANAG 4586 ground-control stations; avionics cryptography and secure boot; M-code GNSS and inertial navigation; swarm communication; ARINC 653 RTOS; targeting and EO/IR sensors; electronic-warfare/radar transceivers.

### <a id="14-military-vehicles-and-armored-platforms"></a>14. Military vehicles and armored platforms

[Open the military-vehicle matrix](Military%20Vehicle%20Critical%20Zero-Days%20%26%20Exploit%20Matrix%20(2021-2026).md)

**Systems and devices covered:** Vetronics, MIL-STD-1553B, and CAN; active protection systems and radar; battle-management systems; tactical software-defined radios; fire-control computers and sighting systems; unmanned ground vehicles; hybrid-electric drive and power distribution; HUMS and maintenance diagnostics.

### <a id="15-military-ai-systems"></a>15. Military AI systems

[Open the military-AI matrix](Military%20AI%20Systems%20Critical%20Vulnerabilities%20(2021-2026).md)

**Systems and devices covered:** Autonomous targeting and computer vision; tactical edge AI accelerators; model-training and data pipelines; tactical language models and command interfaces; autonomous swarms and sensor fusion; PyTorch, TensorRT, and ONNX model ingestion/runtime.

### <a id="16-commercial-and-military-satellites"></a>16. Commercial and military satellites

[Open the satellite and space-threat matrix](Satellite%20Critical%20Zero-Days%20%26%20Space%20Threat%20Matrix%20(2021-2026).md)

**Systems and devices covered:** Viasat/KA-SAT terminals and management; TT&C links; ground-control and satellite-management software; GPS/Galileo GNSS; inter-satellite laser/RF links; software-defined satellite payloads and onboard virtualization; MILSATCOM; radiation-hardened microcontrollers and FPGAs.

---

## ▸ 4. Emerging and specialized technologies

### <a id="17-nanotechnology-and-bio-cyber-interfaces"></a>17. Nanotechnology and bio-cyber interfaces

[Open the nanotechnology and bio-cyber matrix](Nanotechnology%20Critical%20Vulnerability%20Matrix%20(2021-2026)%20(1).md)

**Systems and devices covered:** Internet of Nano-Things and molecular signaling; targeted nanocarriers and drug-delivery systems; DNA synthesis and cyber-biosecurity pipelines; NEMS/MEMS actuators and resonators; optogenetics and quantum-dot sensors; nanofabrication/EUV and GDSII supply chains; lab-on-a-chip microfluidics; bio-implants and body-area nanosensor nodes.

### <a id="18-military-nanotechnology-and-weaponized-nanosystems"></a>18. Military nanotechnology and weaponized nanosystems

[Open the military-nanotechnology matrix](Military%20%26%20Weapons%20Nanotech%20Critical%20Vulnerability%20Matrix%20(2021-2026).md)

**Systems and devices covered:** Nano-energetics and explosives; active camouflage and metamaterials; smart-dust/MEMS/NEMS sensor swarms; bio-nano precision delivery; molecular fabrication and atomic-layer deposition; carbon-nanotube materials and exoskeletons.

---

## ▸ Coverage at a glance

| Collection area | Matrices | Examples of covered systems |
|---|---:|---|
| End-user operating systems | 5 | Android, iOS, macOS, Windows, Linux |
| Connected and embedded devices | 5 | IoT, cameras, TVs, vehicles, drones |
| Industrial, aerospace, and defense | 6 | ICS/SCADA, avionics, tactical UAS, military vehicles, AI, satellites |
| Emerging and specialized technologies | 2 | Nanotechnology, bio-cyber interfaces, weaponized nanosystems |
| **Total** | **18** | **Software, hardware, protocols, supply chains, and cyber-physical systems** |

---

## ▸ Research and verification notes

- The 2021–2026 range is the collection's stated scope, not a guarantee that every listed issue was disclosed or assigned during that period.
- Some documents include published CVEs; others present generalized risk scenarios or illustrative threat models. Check each entry and its sources.
- CVSS values and severity labels may vary by source, version, or configuration. Confirm ratings and applicability in authoritative advisories.
- Product names identify examples in the matrices; they do not establish that a vendor or product is vulnerable.
- These documents are not substitutes for asset-specific vulnerability management, vendor guidance, safety engineering, or incident-response procedures.

## ▸ Disclaimer

This repository is provided for educational and defensive security research. It contains summaries and threat scenarios, not operational instructions or exploit code. Assess systems only with explicit authorization and within applicable laws, safety requirements, and rules of engagement. The authors make no guarantee that the matrices are complete, current, or independently validated; readers are responsible for verifying claims before relying on them.
