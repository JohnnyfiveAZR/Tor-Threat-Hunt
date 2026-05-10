# Indicators of Compromise (IOCs)

All IOCs identified during the Tor Browser threat hunt on device `threat-hunt-lab`.

---

## File Hashes (SHA256)

| Filename | SHA256 | Notes |
|----------|--------|-------|
| `tor-browser-windows-x86_64-portable-15.0.11.exe` | `3ae94669801d4c1370066c2322eb3bd58a4e3cd063dab6670ea3eecf286145e7` | Tor Browser portable installer |
| `tor.exe` | `176c9cb6131fb49fa5e982e823766947e5ce673177c7fff339f5e7a9d330ebf3` | Tor core binary — Apr 14 session |
| `tor.exe` | `a028d058c4d49cf0df10fe6069e4c8fe177d8996414550c6f10c1a97ee24a620` | Tor core binary — Apr 29 / May 4 sessions |
| `firefox.exe` | `ef09a491d65b51f1f304145f6914a6682acd5c6226d0a241361730881134de35` | Tor Browser engine — Apr 14 session |
| `firefox.exe` | `cc24a3b8e51a8301f65fe06335ec65a95b9076d4784dfbae0a6adac0f025bfaa` | Tor Browser engine — Apr 29 / May 4 sessions |
| `Tor-shopping-list.txt.txt` | `aed3e74a0a0fa51d5a45eb539e0868ff136bbfbacfbef85b84c5a1f4b4523ab2` | Suspicious file created post-browsing |
| `Tor Browser.lnk` (Desktop) | `55df6c674d8f72cfda77db3dad77082ea99c3d1715697df392dd179e7aca478a` | Desktop shortcut |
| `Tor Browser.lnk` (Start Menu) | `2e42228df9c26a6d525f32f8870bd1de5312934bc26d55099b41c1f69dd400c4` | Start Menu shortcut |
| `Tor-shopping-list.txt.lnk` | `96a1e29d880fe7b2fbab545d599011c4e743a9c5d3e1f6bc982e27e1fc27a846` | Recent Items shortcut for the shopping list |

---

## IP Addresses — Tor Relay Nodes

All connections observed on port **9001** (Tor OR relay port).

| IP Address | Port | Date Observed | Session |
|------------|------|---------------|---------|
| `65.21.49.9` | 9001 | Apr 14, 2026 | Session 1 (employee) |
| `45.157.234.132` | 9001 | Apr 14, 2026 | Session 1 (employee) |
| `144.217.90.187` | 9001 | Apr 29, 2026 | Session 2 (johnnynet1) |
| `86.121.35.224` | 9001 | Apr 29, 2026 | Session 2 (johnnynet1) |
| `192.34.87.86` | 9001 | May 4, 2026 | Session 3 (employee) |
| `87.98.237.152` | 9001 | May 4, 2026 | Session 3 (employee) |

---

## Process Indicators

| Process | Path | Notes |
|---------|------|-------|
| `tor.exe` | `C:\Users\[account]\Desktop\Tor Browser\Browser\TorBrowser\Tor\tor.exe` | Non-standard path; confirms portable install off Desktop |
| `firefox.exe` | `C:\Users\[account]\Desktop\Tor Browser\Browser\firefox.exe` | Tor-bundled Firefox; not standard Firefox install |

---

## File Path Indicators

| Path | Significance |
|------|-------------|
| `C:\Users\JohnnyNet1\Downloads\tor-browser-windows-x86_64-portable-15.0.11.exe` | Download location (file later deleted) |
| `C:\Users\[account]\Desktop\Tor Browser\` | Portable install root |
| `C:\Users\JohnnyNet1\Desktop\Tor-shopping-list.txt.txt` | High-interest file — dark web intent indicator |

---

## Ports

| Port | Protocol | Role |
|------|----------|------|
| 9001 | TCP | Tor OR relay (outbound to Tor network) |
| 9150 | TCP | Local Tor SOCKS proxy (firefox.exe → tor.exe) |
| 9151 | TCP | Local Tor control port |
