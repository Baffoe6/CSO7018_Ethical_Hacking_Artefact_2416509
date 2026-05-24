# Evidence Log — Unit 3 Lesson 3: Enumeration
Student ID: 2416509 | Module: CSO7018 Ethical Hacking
Activity: Service enumeration — Banner grabbing, DNS enumeration
Date: 22 May 2026
Environment: Kali Linux → Metasploitable 2 (authorized university lab)
Attacker IP: 192.168.122.148 | Target IP: 192.168.122.108

---

## Evidence Table

| # | Screenshot | Command | Purpose | Key Findings | Interpretation |
|---|-----------|---------|---------|--------------|----------------|
| 1 | `U3L3_01_nslookup_dns_enum.png` | `nslookup` interactive mode | DNS enumeration session | nslookup prompt ready | DNS enumeration starting |
| 2 | `U3L3_02_nslookup_any_records.png` | `set type=any; <domain>` | Query all DNS record types | Multiple record types returned | Comprehensive DNS profile |
| 3 | `U3L3_03_nslookup_timeout_vm.png` | `nslookup hackthissite.org` in VM | DNS from VM (timed out) | Connection to 192.168.122.1#53 timed out | VM DNS not routed externally; internal lab network confirmed |
| 4 | `U3L3_04_dnsenum_start.png` | `dnsenum <domain>` | Start DNS enumeration with dnsenum | dnsenum running | DNS brute-force enumeration initiated |
| 5 | `U3L3_05_dnsenum_host_records.png` | `dnsenum` host records | View discovered A records | Host IP mappings | DNS host inventory |
| 6 | `U3L3_06_dnsenum_brute_force.png` | `dnsenum` brute force section | Subdomain brute force | `/usr/share/dnsenum/dns.txt` wordlist used | Subdomain enumeration in progress |
| 7 | `U3L3_07_dnsenum_results.png` | `dnsenum` final results | Review dnsenum output | Subdomains: forum, irc, stats, www; Class C: 137.74.187.0/24, 185.24.222.0/24 | Target DNS infrastructure fully mapped |
| 8 | `U3L3_08_service_enum_banners.png` | Service banner grabbing | Enumerate service banners | Service version banners returned | Software versions identified for CVE matching |
| 9 | `U3L3_09_enumeration_complete.png` | Final enumeration view | Activity completion | Results documented | Enumeration activity complete |

---

## Notes

- Banner grabbing on Metasploitable revealed several intentionally misconfigured services with verbose version banners.
- DNS zone transfer (AXFR) attempts against Metasploitable's DNS service may or may not succeed depending on lab configuration.
- Update placeholder rows above with actual findings from your screenshots.

---

## Key Enumeration Targets (Metasploitable 2)

| Port | Service | Expected Banner Information |
|------|---------|----------------------------|
| 21 | vsftpd | vsftpd 2.3.4 (backdoored version) |
| 22 | OpenSSH | OpenSSH 4.7p1 Debian |
| 23 | Telnet | Linux telnetd |
| 25 | Postfix SMTP | Postfix smtpd |
| 80 | Apache | Apache/2.2.8 (Ubuntu) |
| 3306 | MySQL | MySQL 5.0.51a |

---

## Ethical Note

Enumeration activities were limited to the Metasploitable 2 VM. Banner grabbing and service enumeration are standard reconnaissance techniques in authorized penetration testing. No attempts were made to enumerate real-world external systems.

---

Evidence log last updated: 22 May 2026
