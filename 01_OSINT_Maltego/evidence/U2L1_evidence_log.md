# Evidence Log — Unit 2 Lesson 1: OSINT Using Maltego
Student ID: 2416509 | Module: CSO7018 Ethical Hacking
Activity: Maltego OSINT Investigation
Date: 22 May 2026
Environment: Kali Linux VM (authorized university lab)

---

## Evidence Table

| # | Screenshot | Command / Action | Purpose | Key Findings | Interpretation |
|---|-----------|-----------------|---------|--------------|----------------|
| 1 | `U2L1_01_maltego_kali_desktop.png` | Launch Kali Linux desktop | Verify VM environment is running | Kali Linux desktop loaded | Attack platform ready for OSINT tools |
| 2 | `U2L1_02_maltego_download_page.png` | Navigate to Maltego download page | Obtain Maltego CE installer | Download page accessible | Confirms tool availability |
| 3 | `U2L1_03_maltego_install_setup.png` | Launch Maltego installer | Begin installation process | Setup wizard started | Installation sequence initiated |
| 4 | `U2L1_04_maltego_install_progress.png` | Installation in progress | Monitor install completion | Files being extracted/installed | Tool being deployed to system |
| 5 | `U2L1_05_maltego_launch.png` | Launch Maltego CE application | Verify successful installation | Maltego GUI opened | Tool installed and operational |
| 6 | `U2L1_06_maltego_new_graph.png` | Create new graph | Start OSINT investigation | Blank graph canvas created | Investigation workspace ready |
| 7 | `U2L1_07_maltego_entity_domain.png` | Add Domain entity to graph | Create seed entity for investigation | Domain entity placed in graph | Starting point for transforms |
| 8 | `U2L1_08_maltego_run_transform.png` | Run transform on entity | Execute OSINT data gathering | Transform running against target | Active intelligence collection |
| 9 | `U2L1_09_maltego_dns_results.png` | DNS transform results | Enumerate DNS records | DNS entries returned | DNS infrastructure mapped |
| 10 | `U2L1_10_maltego_ip_entities.png` | IP address entities added | Map IP address space | IP addresses linked to domain | Network footprint identified |
| 11 | `U2L1_11_maltego_website_entities.png` | Website entities added | Identify web presence | Website nodes returned | Web infrastructure documented |
| 12 | `U2L1_12_maltego_expanded_graph.png` | Expanded OSINT graph | Visualise relationships | Multiple nodes with relationships | Entity connections established |
| 13 | `U2L1_13_maltego_person_entities.png` | Person/contact entities | Identify associated individuals | Named entities returned | Social footprint identified |
| 14 | `U2L1_14_maltego_whois_results.png` | WHOIS transform results | Gather registration information | Registrar, creation date, contacts | Domain ownership intelligence |
| 15 | `U2L1_15_maltego_mx_records.png` | MX record transform | Identify mail servers | Mail exchange servers listed | Email infrastructure mapped |
| 16 | `U2L1_16_maltego_full_graph.png` | Full OSINT graph view | Complete entity relationship map | All nodes and edges visible | Comprehensive OSINT picture |
| 17 | `U2L1_17_maltego_entity_detail.png` | Entity detail panel | Inspect individual entity data | Detailed properties shown | Deep intelligence on target entity |
| 18 | `U2L1_18_maltego_final_graph_export.png` | Final graph / export | Document investigation results | Complete graph saved | Evidence preserved for analysis |

---

## Notes

- All transforms used Community Edition free-tier transforms only.
- No authenticated API keys to commercial intelligence services were used.
- Data sourced exclusively from public, open-source repositories (Wikipedia, public DNS, etc.).
- No personal data of real individuals was intentionally targeted.

---

## Ethical Note

This Maltego investigation was conducted using publicly available open-source data within the authorized university lab exercise. No private, confidential, or protected information was accessed. The purpose is purely educational, demonstrating OSINT methodology as taught in CSO7018.

---

Evidence log last updated: 22 May 2026
