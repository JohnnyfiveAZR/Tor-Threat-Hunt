# 🔍 Threat Hunt — Unauthorized Tor Browser Usage

![Platform](https://img.shields.io/badge/Platform-Microsoft%20Defender%20XDR-blue)
![Language](https://img.shields.io/badge/Query%20Language-KQL-orange)
![Status](https://img.shields.io/badge/Status-Completed-green)
![Classification](https://img.shields.io/badge/Classification-Confirmed%20Threat-red)

## Overview

This repository documents a completed threat hunt investigating unauthorized Tor Browser usage on a corporate Windows endpoint (`threat-hunt-lab`). The hunt was conducted using **Microsoft Defender XDR / Microsoft Sentinel** with **KQL (Kusto Query Language)** queries across multiple device telemetry tables.

The investigation confirmed deliberate Tor Browser download, installation, and active use across **three separate sessions** by two user accounts, along with the creation of a file named `Tor-shopping-list.txt` — a strong indicator of intended dark web activity.

---

## 🗂️ Repository Structure

```
tor-threat-hunt/
├── README.md                   # This file
├── queries/                    # All KQL queries used during the hunt
│   ├── 01_file_events.kql      # Detect Tor-related file creation/deletion
│   ├── 02_installer_execution.kql  # Detect installer launch
│   ├── 03_process_execution.kql    # Detect Tor/Firefox process execution
│   └── 04_network_connections.kql  # Detect outbound Tor network connections
├── evidence/                   # Raw log exports from Defender XDR
│   ├── Tor-Download.csv        # File creation/deletion events
│   ├── Tor-install.csv         # Installer process creation events
│   ├── Tor-process-creation.csv # Tor & Firefox process events
│   └── Tor-usage.csv           # Network connection events
├── docs/
│   ├── iocs.md                 # Indicators of Compromise
│   └── mitre-mapping.md        # MITRE ATT&CK technique mapping
└── reports/
    └── Tor-ThreatHunt-Report.docx  # Full formal investigation report
```

---

## 🎯 Hunt Hypothesis

> **"An employee on the corporate endpoint `threat-hunt-lab` may be using the Tor Browser to anonymize network traffic and access dark web resources in violation of acceptable use policy."**

---

## 📅 Timeline Summary

| Timestamp | Event | Account |
|-----------|-------|---------|
| Apr 14, 2026 — 8:44 AM | First Tor Browser session detected (pre-existing install) | `employee` |
| Apr 14, 2026 — 8:45 AM | Outbound Tor relay connections confirmed (port 9001) | `employee` |
| Apr 29, 2026 — 2:12 PM | Tor Browser installer downloaded | `johnnynet1` |
| Apr 29, 2026 — 3:57 PM | Installer executed, Tor extracted to Desktop; installer deleted | `johnnynet1` |
| Apr 29, 2026 — 3:57 PM | Second Tor session launched; relay connections to 3 nodes | `johnnynet1` |
| Apr 29, 2026 — 4:07 PM | **`Tor-shopping-list.txt` created on Desktop** | `johnnynet1` |
| May 4, 2026 — 10:46 AM | Third Tor session launched | `employee` |
| May 4, 2026 — 10:47 AM | Outbound relay connections confirmed; 20+ tabs opened | `employee` |

---

## 🔎 Hunt Methodology

Queries were executed across the following Microsoft Defender XDR tables:

| Table | Purpose |
|-------|---------|
| `DeviceFileEvents` | Detect Tor-related file creation, extraction, and deletion |
| `DeviceProcessEvents` | Detect execution of `tor.exe`, `firefox.exe`, installer launch |
| `DeviceNetworkEvents` | Detect outbound connections on known Tor ports |

---

## ✅ Outcome

- **Verdict:** Threat Confirmed
- **Action Taken:** Device isolated from the network; user's direct manager notified
- **Key Evidence:** Installer download + deletion, three active Tor sessions, outbound connections to 6 Tor relay nodes, and creation of `Tor-shopping-list.txt`

---

## 📋 Requirements

- Microsoft Defender XDR or Microsoft Sentinel workspace
- Access to `DeviceFileEvents`, `DeviceProcessEvents`, `DeviceNetworkEvents` tables
- KQL query editor (Defender XDR Advanced Hunting or Log Analytics)

---

## 📄 License

This project is for educational and professional portfolio purposes. All hostnames, usernames, and IP addresses are from a controlled lab environment.
