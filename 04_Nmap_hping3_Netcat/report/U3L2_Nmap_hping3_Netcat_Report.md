# CSO7018 Ethical Hacking — Lab Report
## Unit 3 Lesson 2: Network Scanning — Nmap, hping3, and Netcat

---

| | |
|---|---|
| Student ID | 2416509 |
| Module | CSO7018 Ethical Hacking |
| Assessment | Artefact 2 — VM Lab Practical Activities |
| Activity | Unit 3, Lesson 2 — Network Scanning Techniques |
| Date Performed | 22 May 2026 |
| Environment | Kali Linux → Metasploitable 2 (authorized university lab) |
| Attacker IP | 192.168.122.148 |
| Target IP | 192.168.122.108 |

---

## Table of Contents

1. Introduction
2. Objectives
3. Technical Background
4. Commands Used
5. Findings
 - 5.1 Nmap List Scan
 - 5.2 Live Host Discovery (Ping Sweep)
 - 5.3 NULL Scan
 - 5.4 XMAS Scan
 - 5.5 hping3 ICMP Scan
 - 5.6 Netcat Port Scan
6. Scan Comparison
7. Ethical Considerations
8. Reflection
9. Conclusion
10. References

---

## 1. Introduction

Network scanning is the active phase of reconnaissance that follows initial OSINT and passive information gathering. It involves sending crafted packets to a target system and analysing the responses to determine the state of ports, identify live hosts, detect running services, and infer the target operating system. This phase transitions the attacker from passive intelligence gathering to active network interaction.

Three tools are explored in this activity:

- Nmap — The industry-standard network scanner, capable of host discovery, port scanning, OS detection, and service version identification.
- hping3 — A packet crafting tool that provides granular control over TCP, UDP, and ICMP packet construction, useful for firewall testing and custom scanning.
- Netcat (nc) — The "Swiss Army knife" of networking, capable of banner grabbing, port scanning, file transfer, and reverse shells.

---

## 2. Objectives

- Perform host discovery across the lab subnet using Nmap list scan and ping sweep.
- Execute stealth scanning techniques (NULL scan, XMAS scan) and interpret the results.
- Use hping3 to send custom ICMP probes to the target.
- Use Netcat to perform lightweight port scanning.
- Compare and critically evaluate the effectiveness of each scanning technique.

---

## 3. Technical Background

### TCP Flag-Based Scan Types

| Scan Type | Flags Set | Closed Port Response | Open Port Response | Stealth Level |
|-----------|----------|---------------------|-------------------|---------------|
| SYN Scan (-sS) | SYN | RST | SYN/ACK | High |
| NULL Scan (-sN) | None | RST | No response | Very High |
| XMAS Scan (-sX) | FIN+PSH+URG | RST | No response | Very High |
| FIN Scan (-sF) | FIN | RST | No response | Very High |
| Connect Scan (-sT) | SYN+ACK+RST | RST | Full 3-way handshake | Low |

NULL, FIN, and XMAS scans exploit an ambiguity in the TCP RFC: compliant implementations should not respond to unexpected flag combinations on open ports, but must respond with RST on closed ports. This allows open/closed port inference without completing a full TCP handshake.

---

## 4. Commands Used

```bash
# List scan — enumerate subnet without sending packets
nmap -n -sL 192.168.122.0/24

# Ping sweep — discover live hosts
nmap -sn 192.168.122.0/24

# NULL scan — no TCP flags
sudo nmap -sN 192.168.122.108

# XMAS scan — FIN, PSH, URG flags
sudo nmap -sX 192.168.122.108

# Service version detection
nmap -sV 192.168.122.108

# OS fingerprinting
sudo nmap -O 192.168.122.108

# hping3 ICMP scan
sudo hping3 -1 192.168.122.108

# Netcat port scan (TCP)
nc -zv 192.168.122.108 1-1024
```

---

## 5. Findings

### 5.1 Nmap List Scan

Figure 1: `nmap -n -sL 192.168.122.0/24` — subnet address enumeration.

Analysis: The list scan (`-sL`) enumerates all possible host addresses within the `192.168.122.0/24` subnet (256 addresses) without transmitting any packets. This is a purely passive operation used to understand the address space before initiating active probes. No host is contacted; no alerts are generated.

---

### 5.2 Live Host Discovery (Ping Sweep)

Figure 2: `nmap -sn` ping sweep showing live hosts on the subnet.

Analysis: The ping sweep identified 3 live host(s) on the subnet, including `192.168.122.71`, `192.168.122.108`, and `192.168.122.148`. The Kali machine itself (`192.168.122.148`) and the Metasploitable VM (`192.168.122.108`) are visible as active hosts, along with the Ubuntu VM (`192.168.122.71`).

---

### 5.3 NULL Scan

Figure 3: `nmap -sN` NULL scan results against Metasploitable 2.

Analysis: The NULL scan sent TCP segments with no flags set. Ports that returned no response are reported as `open|filtered`; ports responding with RST are `closed`. This scan type can evade some stateless packet filtering firewalls that only block SYN packets.

---

### 5.4 XMAS Scan

Figure 4: `nmap -sX` XMAS scan results against Metasploitable 2.

Analysis: The XMAS scan set the FIN, PSH, and URG flags simultaneously — named for its resemblance to a "lit-up Christmas tree." Responses mirrored those of the NULL scan: open ports returned no response (`open|filtered`); closed ports returned RST.

---

### 5.5 hping3 ICMP Scan

Figure 5: `hping3 -1` ICMP probe output.

Analysis: hping3 was used to send ICMP echo requests (`-1` flag) to the target. ICMP replies confirmed reachability with RTT values of ``. Unlike standard `ping`, hping3 provides detailed packet statistics and allows modification of packet fields, making it a flexible tool for firewall rule enumeration and network mapping.

---

### 5.6 Netcat Port Scan

Figure 6: Netcat TCP port scan of the target.

Analysis: `nc -zv` attempted TCP connections to ports 1–1024 without sending data (`-z` zero I/O mode). Open ports returned `open` or connection success messages. While less sophisticated than Nmap, Netcat's port scanning capability is useful in constrained environments where Nmap is unavailable.

---

## 6. Scan Comparison

| Technique | Open Ports Found | Stealth | Speed | Firewall Evasion | Root Required |
|-----------|-----------------|---------|-------|-----------------|---------------|
| Nmap Ping Sweep | N/A | Medium | Fast | No | No |
| NULL Scan | | High | Medium | Yes (stateless) | Yes |
| XMAS Scan | | High | Medium | Yes (stateless) | Yes |
| hping3 ICMP | N/A | Medium | Slow | Partial | Yes |
| Netcat Scan | | Low | Slow | No | No |

---

## 7. Ethical Considerations

All scanning activities were performed against the Metasploitable 2 VM within the isolated university lab network. Scanning unauthorized systems constitutes an offence under the Computer Misuse Act 1990, Section 1 (unauthorized access) and Section 3 (unauthorized modification, where scan traffic could be argued to impair system function). In professional penetration testing, all scanning must be within the explicitly defined scope of a signed Rules of Engagement document.

NULL and XMAS scans require root/sudo privileges to create raw sockets and are detected by modern IDS/IPS systems despite their theoretical stealth — modern network security monitoring (NSM) platforms flag these non-standard scan patterns.

---

## 8. Reflection

This activity reinforced that no single scan type is universally optimal. The choice of scanning technique must balance thoroughness, stealth requirements, and the target environment's security controls. Nmap's versatility was particularly evident — the transition from a non-intrusive list scan to progressively more active techniques illustrates a methodical reconnaissance approach.

The theoretical basis for NULL and XMAS scans — exploiting ambiguity in RFC 793's TCP specification — demonstrates how protocol design decisions made decades ago continue to have security implications. Modern Linux kernels respond to these scans differently from Windows systems, making them useful for OS discrimination alongside `-O` fingerprinting.

---

## 9. Conclusion

This activity demonstrated a comprehensive range of network scanning techniques against an authorized target. Beginning with passive host enumeration and progressing through stealth scans, custom packet crafting with hping3, and lightweight Netcat scanning, each tool's strengths and limitations were evaluated. The results collectively characterise the target's network exposure and establish the open port inventory required for subsequent enumeration and exploitation phases.

---

## 10. References

Computer Misuse Act 1990 (c.18) UK Parliament. Available at: https://www.legislation.gov.uk/ukpga/1990/18/contents [Accessed: 22 May 2026].

GNU Netcat (2024) Netcat Documentation. Available at: https://netcat.sourceforge.net [Accessed: 22 May 2026].

hping.org (2024) hping3 Man Page. Available at: http://www.hping.org/manpage.html [Accessed: 22 May 2026].

Lyon, G.F. (2009) Nmap Network Scanning. Nmap Project.

Nmap.org (2024) Nmap Reference Guide — Scan Types. Available at: https://nmap.org/book/man-port-scanning-techniques.html [Accessed: 22 May 2026].

Postel, J. (1981) RFC 793: Transmission Control Protocol. Available at: https://datatracker.ietf.org/doc/html/rfc793 [Accessed: 22 May 2026].

---

Report prepared as part of CSO7018 Ethical Hacking, Artefact 2. Student ID: 2416509.
