# MITRE ATT&CK Technique Mapping

Mapping of observed adversary behaviors during the Tor Browser threat hunt to the [MITRE ATT&CK Framework](https://attack.mitre.org/).

---

## Techniques Observed

| Tactic | Technique ID | Technique Name | Observed Behavior |
|--------|-------------|----------------|-------------------|
| **Resource Development** | T1588.002 | Obtain Capabilities: Tool | User downloaded Tor Browser portable installer from the internet |
| **Defense Evasion** | T1090.003 | Proxy: Multi-hop Proxy | Tor Browser used to route traffic through multiple anonymizing relay nodes |
| **Defense Evasion** | T1070.004 | Indicator Removal: File Deletion | Tor installer deleted from Downloads immediately after extraction |
| **Defense Evasion** | T1036 | Masquerading | `firefox.exe` used as the Tor Browser process, blending with legitimate browser traffic |
| **Command & Control** | T1090.003 | Proxy: Multi-hop Proxy | Outbound connections routed through Tor relay nodes (port 9001) |
| **Command & Control** | T1571 | Non-Standard Port | Use of port 9001 for Tor OR relay connections |
| **Exfiltration** | T1048 | Exfiltration Over Alternative Protocol | Potential data exfiltration via anonymized Tor channels |
| **Collection** | T1005 | Data from Local System | Creation of `Tor-shopping-list.txt` suggests local data collection/planning |

---

## Tactic Summary

```
Initial Access
└── (Internal threat — existing user account)

Resource Development
└── T1588.002 — Downloaded Tor Browser portable installer

Execution
└── User manually launched installer and browser (interactive)

Defense Evasion
├── T1090.003 — Multi-hop proxy via Tor network
├── T1070.004 — Installer deleted post-extraction
└── T1036    — firefox.exe masking Tor Browser process

Command & Control
├── T1090.003 — Tor relay nodes used for anonymous C2-style routing
└── T1571    — Non-standard port 9001 for relay connections

Collection
└── T1005 — Tor-shopping-list.txt created (planning/staging artifact)

Exfiltration (Potential)
└── T1048 — Anonymous browsing channel established and actively used
```

---

## Notes

- This was an **insider threat** scenario, not an external intrusion. Standard initial access techniques do not apply.
- The use of a **portable installer** (no system-wide install required, no admin rights needed) is a deliberate evasion choice that bypasses software installation controls.
- The **deletion of the installer** immediately after extraction (T1070.004) is a clear indicator of intent to conceal.
