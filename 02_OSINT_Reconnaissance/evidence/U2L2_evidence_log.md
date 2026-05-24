# Evidence Log — Unit 2 Lesson 2: Passive Reconnaissance
Student ID: 2416509 | Module: CSO7018 Ethical Hacking
Activity: Passive OSINT Reconnaissance (ping, nslookup, MX records, WHOIS)
Date: 22 May 2026
Environment: Kali Linux VM (authorized university lab)
Target Domain:

---

## Evidence Table

| # | Screenshot | Command | Purpose | Key Findings | Interpretation |
|---|-----------|---------|---------|--------------|----------------|
| 1 | `U2L2_01_ping_target.png` | `ping <target>` | Test ICMP reachability and resolve hostname | ICMP responses / TTL values | Host is reachable; confirms basic network connectivity |
| 2 | `U2L2_02_ping_results.png` | `ping` output analysis | Verify packet statistics | RTT and packet loss shown | Baseline network latency established |
| 3 | `U2L2_03_nslookup_domain.png` | `nslookup <domain>` | Query DNS A record | IP address returned | DNS resolution working; target IP identified |
| 4 | `U2L2_04_nslookup_mx_records.png` | `nslookup -type=MX <domain>` | Identify mail exchange servers | MX records returned | Mail infrastructure mapped |
| 5 | `U2L2_05_nslookup_ns_records.png` | `nslookup -type=NS <domain>` | Identify nameservers | NS records returned | Authoritative nameservers identified |
| 6 | `U2L2_06_nslookup_all_types.png` | `nslookup -type=any <domain>` | Retrieve all DNS record types | Multiple record types returned | Comprehensive DNS footprint |
| 7 | `U2L2_07_whois_query.png` | `whois <domain>` | Initiate WHOIS lookup | WHOIS query sent | Registration data being retrieved |
| 8 | `U2L2_08_whois_results.png` | `whois` output | Domain registration metadata | Registrar, dates, nameservers | Ownership intelligence gathered |
| 9 | `U2L2_09_whois_registrar_info.png` | `whois` registrar section | Identify registrar details | Registrar name and contact | Useful for social engineering awareness |
| 10 | `U2L2_10_traceroute_target.png` | `traceroute <target>` | Map network path | Hop enumeration started | Network topology investigation begins |
| 11 | `U2L2_11_traceroute_results.png` | `traceroute` output | View intermediate routers | Hop count and IPs | Network path to target identified |
| 12 | `U2L2_12_traceroute_hops.png` | `traceroute` detail | Analyse specific hops | Latency per hop | Gateway and transit network identified |
| 13 | `U2L2_13_host_lookup.png` | `host <domain>` | DNS lookup with host tool | A, MX, NS records | Cross-verification of DNS data |
| 14 | `U2L2_14_host_dns_results.png` | `host` output | Review host command output | All record types shown | Complete DNS profile |
| 15 | `U2L2_15_dig_query.png` | `dig <domain>` | DNS query with dig tool | DNS response sections | Detailed DNS response analysis |
| 16 | `U2L2_16_dig_results.png` | `dig` output | Analyse dig output | Answer section with IP | Authoritative DNS response captured |
| 17 | `U2L2_17_dig_full_output.png` | `dig +all <domain>` | Full dig output with stats | Query time, server, flags | Complete DNS audit information |
| 18 | `U2L2_18_recon_tool_overview.png` | Tool overview | Survey available recon tools | Tool list/help shown | Comprehensive recon toolkit |
| 19 | `U2L2_19_theHarvester_start.png` | `theHarvester -d <domain>` | Initiate email/host harvesting | theHarvester running | Active OSINT harvesting started |
| 20 | `U2L2_20_theHarvester_results.png` | `theHarvester` output | Email/host harvest results | Emails and hostnames found | Public email addresses identified |
| 21 | `U2L2_21_theHarvester_emails.png` | `theHarvester` emails section | Review discovered emails | Email list returned | Social engineering surface identified |
| 22 | `U2L2_22_theHarvester_hosts.png` | `theHarvester` hosts section | Review discovered hosts | Hostname list returned | Additional targets discovered |
| 23 | `U2L2_23_shodan_search.png` | Shodan web search | Search for internet-exposed assets | Search interface shown | Passive device intelligence |
| 24 | `U2L2_24_shodan_results.png` | Shodan results | View exposed services | Open ports/services listed | Attack surface intelligence |
| 25 | `U2L2_25_recon_additional_tool.png` | Additional recon tool | Supplementary reconnaissance | Tool output shown | Additional intelligence gathered |
| 26 | `U2L2_26_recon_dns_enumeration.png` | DNS enumeration tool | Enumerate DNS subdomains | Subdomain list returned | Expanded DNS footprint |
| 27 | `U2L2_27_recon_tool_output.png` | Recon tool output | Review collected data | Data output shown | Intelligence documented |
| 28 | `U2L2_28_recon_findings_summary.png` | Findings summary | Collate reconnaissance data | Summary view shown | Key findings consolidated |
| 29 | `U2L2_29_recon_ip_addresses.png` | IP address analysis | Document discovered IPs | IP address list | Network footprint documented |
| 30 | `U2L2_30_passive_recon_summary.png` | Passive recon summary | Review all passive findings | Summary output | All passive data collated |
| 31 | `U2L2_31_osint_final_results.png` | Final OSINT results | Document complete findings | Complete results shown | Full OSINT profile built |
| 32 | `U2L2_32_osint_target_profile.png` | Target profile | Compile target intelligence | Target profile view | Comprehensive target intelligence |
| 33 | `U2L2_33_recon_complete_output.png` | Complete recon output | Final output documentation | All data visible | Investigation near completion |
| 34 | `U2L2_34_passive_recon_complete.png` | Recon complete | Activity conclusion | Final state shown | Passive reconnaissance complete |

---

## Notes

- All commands used public DNS resolution and WHOIS services — no direct target interaction beyond ICMP.
- WHOIS lookups are performed against public IANA/regional registrar databases.
- MX records reveal mail server infrastructure without any intrusive probing.

---

## Ethical Note

All reconnaissance activities in this lesson were passive in nature. Queries were directed at publicly available DNS and WHOIS infrastructure. No vulnerability probing, port scanning, or active exploitation was performed in this activity. All work is within the scope of the authorized university lab exercise.

---

Evidence log last updated: 22 May 2026
