# Evidence Log — Unit 3 Lesson 2: Nmap / hping3 / Netcat
Student ID: 2416509 | Module: CSO7018 Ethical Hacking
Activity: Network scanning — Nmap, hping3, Netcat techniques
Date: 22 May 2026
Environment: Kali Linux → Metasploitable 2 (authorized university lab)
Attacker IP: 192.168.122.148 | Target IP: 192.168.122.108 | Ubuntu IP: 192.168.122.71 | Subnet: 192.168.122.0/24

---

## Evidence Table

| # | Screenshot | Command | Purpose | Key Findings | Interpretation |
|---|-----------|---------|---------|--------------|----------------|
| 1 | `U3L2_01_nmap_basic_scan.png` | `nmap <target>` | Basic Nmap default scan | Open ports listed | Initial port discovery |
| 2 | `U3L2_02_nmap_scan_results.png` | `nmap` results | Review port scan output | Port list with states | Port inventory established |
| 3 | `U3L2_03_nmap_service_version.png` | `nmap -sV <target>` | Service and version detection | Service names and versions | Vulnerability surface identified |
| 4 | `U3L2_04_nmap_os_detection.png` | `nmap -O <target>` | OS fingerprinting | OS guess with confidence | Target OS identified |
| 5 | `U3L2_05_nmap_null_scan.png` | `nmap -sN <target>` | NULL scan (no TCP flags) | Open/filtered ports | Firewall evasion scan completed |
| 6 | `U3L2_06_nmap_xmas_scan.png` | `nmap -sX <target>` | XMAS scan (FIN+PSH+URG) | Port state responses | Stealth scan technique demonstrated |
| 7 | `U3L2_07_nmap_fin_scan.png` | `nmap -sF <target>` | FIN scan | Port state responses | Alternative stealth scan |
| 8 | `U3L2_08_nmap_syn_scan.png` | `nmap -sS <target>` | SYN (half-open) scan | Open ports via SYN-ACK | Fast stealthy scan |
| 9 | `U3L2_09_nmap_udp_scan.png` | `nmap -sU <target>` | UDP port scan | UDP open/filtered ports | UDP service discovery |
| 10 | `U3L2_10_hping3_icmp.png` | `hping3 -1 <target>` | ICMP ping with hping3 | ICMP replies / RTT | Custom packet crafting demonstrated |
| 11 | `U3L2_11_hping3_syn_flood.png` | `hping3 -S <target>` | TCP SYN probe with hping3 | SYN responses | TCP handshake analysis |
| 12 | `U3L2_12_hping3_tcp_flags.png` | `hping3 --tcp-timestamp` | Custom TCP flag manipulation | Packet responses | Advanced packet crafting |
| 13 | `U3L2_13_hping3_results.png` | hping3 output | Review hping3 results | Statistics output | hping3 activity documented |
| 14 | `U3L2_14_netcat_listen.png` | `nc -lvp <port>` | Netcat listener mode | Listening on port | NC listener established |
| 15 | `U3L2_15_netcat_connect.png` | `nc <target> <port>` | Netcat connection | Connection established | NC client connected |
| 16 | `U3L2_16_netcat_banner_grab.png` | `nc <target> 21/22/80` | Banner grab via Netcat | Service banner returned | Service version confirmed passively |
| 17 | `U3L2_17_netcat_shell.png` | Netcat shell interaction | Demonstrate shell transfer | Shell session visible | Remote shell capability demonstrated |
| 18 | `U3L2_18_nmap_hping3_netcat_complete.png` | Final scan summary | Document activity completion | Results overview | All scanning techniques demonstrated |

---

## Scan Technique Comparison

| Technique | Tool | TCP Flags Sent | Purpose | Stealth Level |
|-----------|------|---------------|---------|---------------|
| List Scan | Nmap | None | Enumerate address space | Highest (no packets) |
| Ping Sweep | Nmap | ICMP/ARP | Discover live hosts | Medium |
| NULL Scan | Nmap | None | Port state detection | High |
| XMAS Scan | Nmap | FIN+PSH+URG | Port state detection | High |
| ICMP Probe | hping3 | ICMP | Connectivity / rate test | Medium |
| Port Scan | Netcat | SYN/ACK | Open port identification | Low |

---

## Ethical Note

All scanning activities were directed exclusively at the Metasploitable 2 VM within the isolated university lab network. No scans were directed at external hosts, the internet, or unauthorized systems. Root/sudo access was required for raw socket scans (NULL, XMAS).

---

Evidence log last updated: 22 May 2026
