# CSO7018 Ethical Hacking — Artefact 2: VM Lab Practical Activities

| | |
|---|---|
| Student ID | 2416509 |
| Module | CSO7018 Ethical Hacking |
| Assessment | Artefact 2 — VM Lab Practical Activities |
| Coverage | Units 2, 3, and 4 |
| Submission Date | 22 May 2026 |
| Environment | Apporto University VM Lab — Authorised Use Only |

---

## Ethical Statement

> All activities documented in this portfolio were conducted exclusively within the authorised, isolated virtual machine laboratory environment provided by the university via the Apporto platform as part of the CSO7018 Ethical Hacking module. No activities were directed at any live, public, production, or unauthorised system. All scanning, enumeration, and exploitation tasks were performed against a designated Metasploitable 2 training VM on a host-only, air-gapped network. This work is conducted under the explicit authorisation of the module curriculum and in compliance with the Computer Misuse Act 1990 and the Data Protection Act 2018.

---

## Repository Structure

```
CSO7018_Ethical_Hacking_Artefact_2416509/
│
├── 01_OSINT_Maltego/               # Unit 2, Lesson 1 — OSINT Using Maltego
│   ├── evidence/                   # Evidence logs
│   ├── notes/                      # Working notes
│   ├── report/                     # Lab report (U2L1_Maltego_OSINT_Report.md)
│   └── screenshots/                # Supporting screenshots
│
├── 02_OSINT_Reconnaissance/        # Unit 2, Lesson 2 — Passive Reconnaissance
│   ├── evidence/
│   ├── notes/
│   ├── report/                     # U2L2_Reconnaissance_Report.md
│   └── screenshots/
│
├── 03_Linux_Environment/           # Unit 3, Lesson 1 — Linux Networking Environment
│   ├── evidence/
│   ├── notes/
│   ├── report/                     # U3L1_Linux_Environment_Report.md
│   └── screenshots/
│
├── 04_Nmap_hping3_Netcat/          # Unit 3, Lesson 2 — Network Scanning
│   ├── evidence/
│   ├── notes/
│   ├── report/                     # U3L2_Nmap_hping3_Netcat_Report.md
│   └── screenshots/
│
├── 05_Enumeration/                 # Unit 3, Lesson 3 — Service Enumeration
│   ├── evidence/
│   ├── notes/
│   ├── report/                     # U3L3_Enumeration_Report.md
│   └── screenshots/
│
├── 06_Nessus_Vulnerability_Scanning/ # Unit 4, Lesson 1 — Vulnerability Scanning
│   ├── evidence/
│   ├── notes/
│   ├── report/                     # U4L1_Nessus_Scanning_Report.md
│   └── screenshots/
│
├── 07_Metasploit_Access/           # Unit 4, Lesson 3 — Exploitation with Metasploit
│   ├── evidence/
│   ├── notes/
│   ├── report/                     # U4L3_Metasploit_FTP_Report.md
│   └── screenshots/
│
├── CSO7018_Lab_Questions_and_Answers_2416509.pdf  # Lab questions and answers (PDF)
│
└── final_report/                   # Consolidated portfolio reports
    ├── FINAL_LAB_PORTFOLIO.md      # Full integrated lab portfolio
    ├── MASTER_REPORT.md            # Master summary report
    └── summarised_report_VM_lab_practical_activities_2416509.pdf  # Summarised report (PDF)
```

---

## Lab Activities Summary

| # | Folder | Unit | Activity |
|---|--------|------|----------|
| 1 | `01_OSINT_Maltego` | Unit 2 | OSINT investigation using Maltego |
| 2 | `02_OSINT_Reconnaissance` | Unit 2 | Passive reconnaissance techniques |
| 3 | `03_Linux_Environment` | Unit 3 | Linux networking environment setup |
| 4 | `04_Nmap_hping3_Netcat` | Unit 3 | Network scanning with Nmap, hping3, Netcat |
| 5 | `05_Enumeration` | Unit 3 | Service and OS enumeration |
| 6 | `06_Nessus_Vulnerability_Scanning` | Unit 4 | Vulnerability scanning with Nessus |
| 7 | `07_Metasploit_Access` | Unit 4 | Exploitation via Metasploit (FTP) |

---

## Target Environment

- Target VM: Metasploitable 2 (intentionally vulnerable training system)
- Network: Host-only, air-gapped — no external connectivity
- Platform: Apporto University Virtual Lab
- Attacker VM: Kali Linux

---

## Legal & Ethical Compliance

- Computer Misuse Act 1990
- Data Protection Act 2018
- University Ethical Hacking Lab Agreement
- All activities performed within the authorised lab scope only
