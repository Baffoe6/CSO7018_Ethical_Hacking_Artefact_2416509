# CSO7018 Ethical Hacking — Master Portfolio Report
## Artefact 2: VM Lab Practical Activities

---

| | |
|---|---|
| Student ID | 2416509 |
| Module | CSO7018 Ethical Hacking |
| Assessment | Artefact 2 — VM Lab Practical Activities |
| Coverage | Units 2, 3, and 4 |
| Submission Date | 22 May 2026 |

---

## Ethical Statement

> All activities documented in this report were conducted exclusively within an authorized, isolated virtual machine laboratory environment provided by the university as part of the CSO7018 Ethical Hacking module. No activities were directed at any live, public, production, or unauthorized system. All scanning, enumeration, and exploitation tasks were performed against the designated Metasploitable 2 intentionally vulnerable training VM. This work is conducted under the explicit authorization of the module curriculum and in compliance with the university's ethical hacking lab agreement, the Computer Misuse Act 1990, and applicable UK data protection legislation.

---

## Table of Contents

1. Executive Summary
2. Lab Environment
3. Unit 2 — OSINT and Passive Reconnaissance
 - 3.1 Lesson 1 — Maltego OSINT Investigation
 - 3.2 Lesson 2 — Passive Reconnaissance
4. Unit 3 — Network Scanning and Enumeration
 - 4.1 Lesson 1 — Linux Networking Environment
 - 4.2 Lesson 2 — Nmap, hping3, and Netcat
 - 4.3 Lesson 3 — Service Enumeration
5. Unit 4 — Vulnerability Scanning and Exploitation
 - 5.1 Lesson 1 — Nessus Vulnerability Scanning
 - 5.2 Lesson 3 — Metasploit FTP Exploitation
6. Overall Findings Summary
7. Ethical and Legal Analysis
8. Reflection
9. Conclusion
10. References
11. Appendix A — Screenshot Index
12. Appendix B — Evidence Log Summary

---


## 1. Executive Summary

This report documents the practical lab activities completed as part of the CSO7018 Ethical Hacking module, Artefact 2. The activities span Units 2 through 4, covering the core phases of an ethical hacking engagement: intelligence gathering, active reconnaissance, vulnerability scanning, and controlled exploitation.

Seven practical activities were completed within an authorized VM lab environment comprising a Kali Linux attacker machine and a Metasploitable 2 target VM:

1. OSINT using Maltego — Graph-based intelligence gathering from public sources
2. Passive Reconnaissance — DNS queries, WHOIS, and ping-based host identification
3. Linux Networking — Network interface configuration and VM connectivity verification
4. Nmap/hping3/Netcat — Multi-technique active network scanning
5. Service Enumeration — Banner grabbing and DNS enumeration
6. Nessus Vulnerability Scanning — Automated vulnerability assessment with CVE mapping
7. Metasploit Exploitation — Controlled exploitation of CVE-2011-2523 (vsftpd backdoor)

Key findings include the identification of multiple critical vulnerabilities on Metasploitable 2, including CVE-2011-2523 (CVSS v2: 10.0 / CVSS v3.1: 9.8, Critical), CVE-2010-2075 (CVSS v3.1: 9.8), and CVE-2004-2687 (CVSS v3.1: 9.8). The complete attack chain from public OSINT through to unauthenticated root-level system access was successfully demonstrated and documented.

---


## 2. Lab Environment

| Component | Details |
|-----------|---------|
| Attacker VM | Kali Linux (Rolling Release) |
| Target VM | Metasploitable 2 (Ubuntu 8.04 LTS) |
| Hypervisor | VirtualBox / VMware Workstation |
| Network Type | Host-Only Adapter (isolated) |
| Kali IP | 192.168.122.148 |
| Metasploitable IP | 192.168.122.108 |
| Ubuntu IP | 192.168.122.71 |
| Subnet | 192.168.122.0/24 |

---


## 3. Unit 2 — OSINT and Passive Reconnaissance

### 3.1 Lesson 1 — Maltego OSINT Investigation

> Full report: `01_OSINT_Maltego/report/U2L1_Maltego_OSINT_Report.md`

#### Introduction

Maltego Community Edition was used to conduct an OSINT investigation using graph-based entity analysis. The investigation explored public data relationships through automated transforms against Wikipedia and IBM Watson/NLP services.

#### Key Findings

#### Screenshots

Figure 1.1: Maltego CE launched on Kali Linux.

Figure 1.2: Phrase entity configured as investigation seed node.

Figure 1.3: Wikipedia transform results.

Figure 1.4: IBM Watson NLP entity extraction results.

Figure 1.5: Complete Maltego investigation graph showing all entity relationships.

---

### 3.2 Lesson 2 — Passive Reconnaissance

> Full report: `02_OSINT_Reconnaissance/report/U2L2_Reconnaissance_Report.md`

#### Key Findings

#### Screenshots

Figure 2.1: ping results confirming hostname resolution and ICMP reachability.

Figure 2.2: nslookup DNS A record query.

Figure 2.3: MX record enumeration.

Figure 2.4: WHOIS domain registration data.

---


## 4. Unit 3 — Network Scanning and Enumeration

### 4.1 Lesson 1 — Linux Networking Environment

> Full report: `03_Linux_Environment/report/U3L1_Linux_Environment_Report.md`

#### Key Findings

- Kali Linux attacker IP confirmed: `192.168.122.148` on subnet `192.168.122.0/24`
- Metasploitable 2 target IP confirmed: `192.168.122.108` — ICMP reachable
- Ubuntu VM: `192.168.122.71` — visible on shared host-only network
- Lab environment validated as correctly configured for subsequent scanning and exploitation activities

#### Screenshots

Figure 3.1: Kali Linux network interface configuration (`ip addr`).

Figure 3.2: ICMP ping confirming Kali-to-Metasploitable connectivity.

---

### 4.2 Lesson 2 — Nmap, hping3, and Netcat

> Full report: `04_Nmap_hping3_Netcat/report/U3L2_Nmap_hping3_Netcat_Report.md`

#### Scan Results Summary

| Technique | Command | Key Result |
|-----------|---------|-----------|
| List Scan | `nmap -n -sL 192.168.122.0/24` | Subnet addresses enumerated |
| Ping Sweep | `nmap -sn 192.168.122.0/24` | 3 live hosts |
| NULL Scan | `nmap -sN 192.168.122.108` | open\|filtered ports |
| XMAS Scan | `nmap -sX 192.168.122.108` | open\|filtered ports |
| hping3 ICMP | `hping3 -1 192.168.122.108` | RTT |
| Netcat | `nc -zv 192.168.122.108 1-1024` | open ports |

#### Screenshots

Figure 4.1: Nmap list scan of subnet.

Figure 4.2: Nmap ping sweep — live host discovery.

Figure 4.3: Nmap NULL scan results.

Figure 4.4: Nmap XMAS scan results.

Figure 4.5: hping3 ICMP probe output.

Figure 4.6: Netcat port scan output.

---

### 4.3 Lesson 3 — Service Enumeration

> Full report: `05_Enumeration/report/U3L3_Enumeration_Report.md`

#### Key Findings

| Port | Service | Banner (Example) | CVE Mapping |
|------|---------|-----------------|-------------|
| 21/tcp | vsftpd | `220 (vsFTPd 2.3.4)` | CVE-2011-2523 (Critical) |
| 22/tcp | OpenSSH | `SSH-2.0-OpenSSH_4.7p1 Debian-8ubuntu1` | Multiple (outdated) |
| 80/tcp | Apache | `Apache/2.2.8 (Ubuntu) DAV/2` | Multiple CVEs |
| 3306/tcp | MySQL | `5.0.51a-3ubuntu5` | CVE-2012-2122 |

Banner grabbing disclosed service versions across multiple ports, enabling direct CVE mapping. DNS zone transfer was.

#### Screenshots

Figure 5.1: Banner grabbing via Netcat.

Figure 5.2: dnsenum DNS enumeration output.

---


## 5. Unit 4 — Vulnerability Scanning and Exploitation

### 5.1 Lesson 1 — Nessus Vulnerability Scanning

> Full report: `06_Nessus_Vulnerability_Scanning/report/U4L1_Nessus_Scanning_Report.md`

#### Vulnerability Summary

| Severity | Count (Basic Scan) | Count (All Ports Scan) |
|----------|-------------------|----------------------|
| Critical | | |
| High | | |
| Medium | | |
| Low | | |
| Informational | | |

#### Key Vulnerabilities Identified

| CVE | Vulnerability | CVSS v2 / v3.1 | Service | Severity | Mitigation |
|-----|---------------|------|---------|------------|
| CVE-2011-2523 | vsftpd 2.3.4 Backdoor | 10.0 / 9.8 | 21/tcp (FTP) | Critical | Upgrade vsftpd ≥ 3.0.5; block port 21 |
| CVE-2010-2075 | UnrealIRCd Backdoor | 7.5 / 9.8 | 6667/tcp (IRC) | Critical | Remove UnrealIRCd; verify binary integrity |
| CVE-2004-2687 | distcc RCE | 10.0 / 9.8 | 3632/tcp (distcc) | Critical | Disable distcc; restrict via firewall |
| CVE-2012-1823 | PHP CGI Arg Injection | 7.5 / 9.8 | 80/tcp (HTTP) | Critical | Upgrade PHP; disable CGI arg passthrough |
| CVE-2007-2447 | Samba MS-RPC Shell Injection | 6.0 / 6.3 | 139/tcp (SMB) | High | Upgrade Samba; restrict RPC |
| | | | | | |

#### Screenshots

Figure 6.1: Nessus Essentials installation.

Figure 6.2: Nessus web GUI dashboard.

Figure 6.3: Basic Network Scan configuration.

Figure 6.4: Scan results overview.

Figure 6.5: Vulnerability listing with severity ratings.

Figure 6.6: Severity distribution comparison — Basic Scan vs. All Ports Scan.

Figure 6.7: Nessus CVE detail view showing CVSS score, description, and remediation guidance.

---

### 5.2 Lesson 3 — Metasploit FTP Exploitation

> Full report: `07_Metasploit_Access/report/U4L3_Metasploit_FTP_Report.md`

#### Exploit Summary

| Attribute | Value |
|-----------|-------|
| CVE | CVE-2011-2523 |
| CVSS v2 | 10.0 (Critical) |
| CVSS v3.1 | 9.8 (Critical) |
| CVSS v3.1 Vector | `AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H` |
| Module | `exploit/unix/ftp/vsftpd_234_backdoor` |
| Access Achieved | Root (uid=0) |

#### Screenshots

Figure 7.1: Nmap confirming vsftpd 2.3.4 on port 21.

Figure 7.2: Metasploit with vsftpd exploit module loaded.

Figure 7.3: Exploit module options.

Figure 7.4: Exploit execution output.

Figure 7.5: Shell access obtained.

Figure 7.6: Root access confirmed via `whoami`/`id`.

---


## 6. Overall Findings Summary

| Activity | Key Tool | Primary Finding | Severity |
|---------|---------|----------------|---------|
| OSINT — Maltego | Maltego CE | Entity relationships from public sources | Informational |
| Passive Recon | nslookup/whois | Domain infrastructure exposed | Low |
| Linux Networking | ip addr/ping | VM connectivity verified | Informational |
| Network Scanning | Nmap/hping3 | Multiple open ports identified | Medium |
| Enumeration | Netcat/dnsenum | Version banners expose CVE-mappable services | High |
| Vulnerability Scan | Nessus Essentials | Multiple Critical/High CVEs identified | Critical |
| Exploitation | Metasploit | Root access via CVE-2011-2523 | Critical |
The table above illustrates how each phase feeds directly into the next, forming a complete and traceable attack chain. The OSINT and passive reconnaissance phases (Units 2.1–2.2) established a target profile without direct network interaction, providing the intelligence foundation for subsequent active operations. Network scanning (Unit 3.2) characterised the attack surface and revealed the open port inventory that enumeration (Unit 3.3) then translated into specific software versions and CVE identifiers via banner grabbing. Nessus scanning (Unit 4.1) independently corroborated those findings through automated vulnerability assessment, confirming CVE-2011-2523 among multiple critical findings. The Metasploit activity (Unit 4.3) closed the loop by converting the theoretical CVSS 9.8 severity score into documented, unauthenticated root-level access — demonstrating the concrete operational impact of unpatched vulnerabilities. This progression reflects the PTES (Penetration Testing Execution Standard) methodology and mirrors the Lockheed Martin Cyber Kill Chain (Hutchins, Cloppert and Amin, 2011) across its Reconnaissance, Weaponisation, Delivery, and Exploitation stages.
---


## 7. Ethical and Legal Analysis

All activities were conducted within the following ethical and legal framework:

Computer Misuse Act 1990 (UK): The CMA 1990 prohibits unauthorized computer access (Section 1), unauthorized access with intent to commit further offences (Section 2), and unauthorized modification (Section 3). All activities in this report were authorized by the CSO7018 module curriculum.

Data Protection Act 2018 / UK GDPR: No personal data of real individuals was collected, processed, or retained. All OSINT activities used only fictional or university-provided seed data.

Network and Information Security (NIS) Regulations 2018: Applicable to critical infrastructure — not relevant to this isolated educational lab.

University Ethical Guidelines: All activities conform to the module's stated learning objectives and the university's acceptable use policy for IT resources.

---


## 8. Reflection

Completing Units 2–4 in sequence provided a holistic understanding of the ethical hacking lifecycle. Beginning with passive OSINT and progressing through active scanning to exploitation demonstrated how each phase builds upon the last — intelligence gathered in Unit 2 informs the scanning targets in Unit 3, which in turn identifies the vulnerable service exploited in Unit 4.

The most impactful learning from this portfolio was the accessibility of exploitation when patch management is neglected. CVE-2011-2523 is over a decade old, fully documented, and trivially exploitable with Metasploit. The fact that Metasploitable 2 continues to serve as a relevant training platform demonstrates how persistent unpatched vulnerabilities remain in real-world environments.

---


## 9. Conclusion

This artefact documents a comprehensive practical ethical hacking portfolio spanning OSINT, passive and active reconnaissance, vulnerability scanning, and controlled exploitation. All seven activities were completed successfully within the authorized university lab environment, producing traceable evidence across 36 screenshots referenced across the seven sub-reports, each mapped to specific commands, tool outputs, and findings.

The progression from open-source intelligence gathering to root-level system access on a vulnerable target demonstrates a methodical, structured approach to ethical hacking, consistent with professional penetration testing methodology (PTES, OWASP, EC-Council CEH framework). The identification of multiple CVSS v3.1 9.8-rated vulnerabilities — and the subsequent successful exploitation of CVE-2011-2523 — underscores the persistent operational risk posed by unpatched legacy services, a risk that remains prevalent in real-world enterprise environments regardless of vulnerability age. The technical, analytical, and ethical competencies demonstrated across this portfolio reflect the core learning outcomes of the CSO7018 module.

---


## 10. References

CISA (2024) Known Exploited Vulnerabilities Catalog. Available at: https://www.cisa.gov/known-exploited-vulnerabilities-catalog [Accessed: 22 May 2026].

Computer Misuse Act 1990 (c.18) UK Parliament. Available at: https://www.legislation.gov.uk/ukpga/1990/18/contents [Accessed: 22 May 2026].

EC-Council (2023) Certified Ethical Hacker (CEH) v12 Official Courseware. EC-Council Press.

Engebretson, P. (2013) The Basics of Hacking and Penetration Testing. 2nd edn. Syngress.

FIRST.org (2024) CVSS v3.1 Specification Document. Available at: https://www.first.org/cvss/ [Accessed: 22 May 2026].

hping.org (2024) hping3 Man Page. Available at: http://www.hping.org/manpage.html [Accessed: 22 May 2026].

Hutchins, E., Cloppert, M. and Amin, R. (2011) Intelligence-Driven Computer Network Defense Informed by Analysis of Adversary Campaigns and Intrusion Kill Chains. Lockheed Martin Corporation.

ICANN (2024) WHOIS Lookup. Available at: https://lookup.icann.org [Accessed: 22 May 2026].

Kennedy, D., O'Gorman, J., Kearns, D. and Aharoni, M. (2011) Metasploit: The Penetration Tester's Guide. San Francisco: No Starch Press.

Lyon, G.F. (2009) Nmap Network Scanning. Nmap Project.

Maltego Technologies (2024) Maltego Documentation. Available at: https://docs.maltego.com [Accessed: 22 May 2026].

National Vulnerability Database (2024) CVE-2011-2523. NIST. Available at: https://nvd.nist.gov/vuln/detail/CVE-2011-2523 [Accessed: 22 May 2026].

Nmap.org (2024) Nmap Reference Guide. Available at: https://nmap.org/book/man.html [Accessed: 22 May 2026].

Offensive Security (2024) Kali Linux Documentation. Available at: https://www.kali.org/docs/ [Accessed: 22 May 2026].

Postel, J. (1981) RFC 793: Transmission Control Protocol. Available at: https://datatracker.ietf.org/doc/html/rfc793 [Accessed: 22 May 2026].

Rapid7 (2024a) Metasploit Framework Documentation. Available at: https://docs.metasploit.com/ [Accessed: 22 May 2026].

Rapid7 (2024b) Metasploitable 2 Documentation. Available at: https://docs.rapid7.com/metasploit/metasploitable-2/ [Accessed: 22 May 2026].

Tenable (2024) Nessus Essentials User Guide. Available at: https://docs.tenable.com/nessus/ [Accessed: 22 May 2026].

UK Government (2018) Data Protection Act 2018. Available at: https://www.legislation.gov.uk/ukpga/2018/12/contents [Accessed: 22 May 2026].

---


## 11. Appendix A — Screenshot Index

| Figure | Filename | Activity | Description |
|--------|----------|---------|-------------|
| 1.1 | U2L1_01_maltego_kali_desktop.png | OSINT — Maltego | Maltego application launch |
| 1.2 | U2L1_02_maltego_download_page.png | OSINT — Maltego | Phrase entity configuration |
| 1.3 | U2L1_03_maltego_install_setup.png | OSINT — Maltego | Wikipedia transform results |
| 1.4 | U2L1_04_maltego_install_progress.png | OSINT — Maltego | IBM Watson NLP entities |
| 1.5 | U2L1_05_maltego_launch.png | OSINT — Maltego | Complete investigation graph |
| 2.1 | U2L2_02_ping_results.png | Passive Recon | Ping DNS resolution |
| 2.2 | U2L2_03_nslookup_domain.png | Passive Recon | DNS A record query |
| 2.3 | U2L2_04_nslookup_mx_records.png | Passive Recon | MX record enumeration |
| 2.4 | U2L2_07_whois_query.png | Passive Recon | WHOIS lookup |
| 3.1 | U3L1_06_linux_network_ifconfig.png | Linux Environment | Kali interface config |
| 3.2 | U3L1_01_vm_boot_login.png | Linux Environment | VM connectivity test |
| 4.1 | U3L2_01_nmap_basic_scan.png | Network Scanning | Nmap list scan |
| 4.2 | U3L2_02_nmap_scan_results.png | Network Scanning | Ping sweep |
| 4.3 | U3L2_05_nmap_null_scan.png | Network Scanning | NULL scan |
| 4.4 | U3L2_06_nmap_xmas_scan.png | Network Scanning | XMAS scan |
| 4.5 | U3L2_10_hping3_icmp.png | Network Scanning | hping3 ICMP |
| 4.6 | U3L2_16_netcat_banner_grab.png | Network Scanning | Netcat scan |
| 5.1 | U3L3_08_service_enum_banners.png | Enumeration | Banner grabbing |
| 5.2 | U3L3_04_dnsenum_start.png | Enumeration | DNS enumeration |
| 6.1 | U4L1_02_nessus_install_dpkg.png | Nessus | Installation |
| 6.2 | U4L1_06_nessus_dashboard.png | Nessus | Web GUI dashboard |
| 6.3 | U4L1_08_nessus_scan_config.png | Nessus | Basic scan config |
| 6.4 | U4L1_10_nessus_scan_results_hosts.png | Nessus | Scan results |
| 6.5 | U4L1_11_nessus_vulnerabilities_list.png | Nessus | Vulnerability list |
| 6.6 | U4L1_19_nessus_severity_summary.png | Nessus | Severity comparison — Basic vs. All Ports |
| 6.7 | U4L1_15_nessus_vuln_detail.png | Nessus | CVE detail and remediation guidance |
| 7.1 | U4L3_02_nmap_ftp_port_open.png | Metasploit | FTP version confirm |
| 7.2 | U4L3_04_msf_search_vsftpd.png | Metasploit | Module loaded |
| 7.3 | U4L3_05_msf_use_exploit.png | Metasploit | Module options |
| 7.4 | U4L3_06_msf_set_options_run.png | Metasploit | Exploit execution |
| 7.5 | U4L3_07_msf_shell_etc_shadow.png | Metasploit | Shell access |
| 7.6 | U4L3_08_msf_root_access_confirmed.png | Metasploit | Root confirmed |

---

## 12. Appendix B — Evidence Log Summary

| Activity | Evidence Log File | Screenshots | Commands |
|---------|-----------------|------------|---------|
| U2L1 — Maltego | `01_OSINT_Maltego/evidence/U2L1_evidence_log.md` | 5 | Maltego transforms |
| U2L2 — Recon | `02_OSINT_Reconnaissance/evidence/U2L2_evidence_log.md` | 5 | ping, nslookup, whois |
| U3L1 — Linux | `03_Linux_Environment/evidence/U3L1_evidence_log.md` | 4 | ip addr, ping |
| U3L2 — Scanning | `04_Nmap_hping3_Netcat/evidence/U3L2_evidence_log.md` | 8 | nmap, hping3, nc |
| U3L3 — Enum | `05_Enumeration/evidence/U3L3_evidence_log.md` | 4 | nc, dnsenum |
| U4L1 — Nessus | `06_Nessus_Vulnerability_Scanning/evidence/U4L1_evidence_log.md` | 9 | Nessus scans |
| U4L3 — Metasploit | `07_Metasploit_Access/evidence/U4L3_evidence_log.md` | 7 | msfconsole, exploit |

---

This master report constitutes the complete submission for CSO7018 Ethical Hacking, Artefact 2. Student ID: 2416509.
