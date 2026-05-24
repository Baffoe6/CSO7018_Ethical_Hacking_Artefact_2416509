# CSO7018 Ethical Hacking — Lab Report
## Unit 2 Lesson 2: Passive OSINT Reconnaissance

---

| | |
|---|---|
| Student ID | 2416509 |
| Module | CSO7018 Ethical Hacking |
| Assessment | Artefact 2 — VM Lab Practical Activities |
| Activity | Unit 2, Lesson 2 — Passive Reconnaissance (ping, nslookup, MX, WHOIS) |
| Date Performed | 22 May 2026 |
| Environment | Kali Linux VM — Authorized University Lab |

---

## Table of Contents

1. Introduction
2. Objectives
3. Methodology
4. Commands Used
5. Findings
 - 5.1 ping Results
 - 5.2 nslookup Results
 - 5.3 MX Record Enumeration
 - 5.4 WHOIS Lookup
6. Ethical Considerations
7. Reflection
8. Conclusion
9. References

---

## 1. Introduction

Passive reconnaissance is the first phase of any structured penetration test or ethical hacking engagement. It involves gathering intelligence about a target organization or host using only publicly available information, without sending any probes directly to the target's infrastructure. This approach minimizes the risk of detection while maximizing the intelligence collected prior to active engagement.

This activity explores the core passive reconnaissance toolkit, including DNS query utilities (`ping`, `nslookup`, `dig`), mail record enumeration, and WHOIS domain registration lookups. These techniques represent the foundational layer of the OSINT/reconnaissance phase in the PTES (Penetration Testing Execution Standard) and EC-Council CEH methodology.

---

## 2. Objectives

- Use `ping` to resolve a target hostname to an IP address and verify ICMP reachability.
- Use `nslookup` to query DNS A records and extract DNS server information.
- Enumerate MX (Mail Exchange) records to identify mail server infrastructure.
- Use `whois` to retrieve domain registration metadata, including registrar, nameservers, and contact information.
- Interpret each output in the context of an attacker's pre-engagement reconnaissance phase.

---

## 3. Methodology

1. ping — ICMP echo request to target domain to confirm DNS resolution and host reachability.
2. nslookup — Interactive DNS query for A records; query against both default and authoritative nameservers.
3. nslookup -type=MX — Specific query for mail exchange records to identify email infrastructure.
4. whois — Domain registration query against public WHOIS database.
5. traceroute (if performed) — Path discovery to map network routing between source and target.

---

## 4. Commands Used

```bash
# Test DNS resolution and ICMP reachability
ping <target_domain>

# Query DNS A record
nslookup <target_domain>

# Query MX records
nslookup -type=MX <target_domain>

# Query nameservers
nslookup -type=NS <target_domain>

# WHOIS domain lookup
whois <target_domain>

# Network path mapping
traceroute <target_domain>
```

---

## 5. Findings

### 5.1 ping Results

Figure 1: `ping` command output showing DNS resolution and ICMP responses.

Analysis: The `ping` command resolved the target domain to IP address ``. ICMP echo replies were received, confirming the host is ICMP-reachable. The TTL value of `` provides an indication of the operating system (Linux/Unix TTL ≈ 64; Windows TTL ≈ 128; Cisco TTL ≈ 255).

---

### 5.2 nslookup Results

Figure 2: `nslookup` DNS query results.

Analysis: `nslookup` confirmed the authoritative DNS response for the target domain, returning IP address(es) ``. The responding server `` indicates [authoritative / recursive] DNS resolution. Multiple A records may indicate load balancing or CDN infrastructure.

---

### 5.3 MX Record Enumeration

Figure 3: MX record query results showing mail exchange server details.

Analysis: MX record enumeration revealed the following mail server(s): ``. The MX priority values indicate the preferred mail routing order. Mail server hostnames can reveal third-party email providers (e.g., Google Workspace, Microsoft 365) or self-hosted infrastructure, both of which are relevant to social engineering and phishing surface assessment.

---

### 5.4 WHOIS Lookup

Figure 4: WHOIS query results displaying domain registration metadata.

Analysis: The WHOIS query returned the following key intelligence:

| Field | Value |
|-------|-------|
| Registrar | |
| Registration Date | |
| Expiry Date | |
| Nameservers | |
| Registrant Organization | |

The registrar and nameserver information confirms. Domain age (registration date) is relevant as recently registered domains may indicate malicious infrastructure or new organizational entities.

---

## 6. Ethical Considerations

Passive reconnaissance is the least invasive phase of a penetration test. All commands used in this activity query publicly accessible databases:

- ping / nslookup — Use public DNS infrastructure; no private systems accessed.
- WHOIS — Queries public IANA/regional registrar databases; data is publicly disclosed by domain registrants.
- MX records — Public DNS data; no access to mail systems.

In a real-world engagement, written authorization from the target organization is required before any reconnaissance, even passive. Under UK law, unauthorized computer access, even passive querying of in-scope infrastructure, may constitute an offence under the Computer Misuse Act 1990.

Where WHOIS queries return personal data — such as registrant names, addresses, or email addresses — collection and processing of that data is governed by the UK General Data Protection Regulation (UK GDPR) and the Data Protection Act 2018. Security practitioners must ensure that data is collected only for the stated engagement purpose, retained no longer than necessary, and handled in accordance with applicable data protection obligations.

In this activity, all queries were directed exclusively at the designated lab domain within the explicit authorization of the CSO7018 module curriculum.

---

## 7. Reflection

This activity demonstrated that significant intelligence about a target can be gathered without any direct interaction with their systems. The combination of DNS queries and WHOIS lookups reveals IP ranges, mail infrastructure, hosting providers, domain age, and administrative contacts — all from public sources.

A key observation is that organizations can reduce their passive reconnaissance exposure through privacy-protected WHOIS registrations, split-horizon DNS configuration, and minimizing publicly disclosed infrastructure details. This understanding is directly applicable to defensive security consulting roles.

---

## 8. Conclusion

This activity successfully demonstrated passive OSINT reconnaissance techniques using standard Kali Linux networking utilities. The tools examined — `ping`, `nslookup`, and `whois` — collectively revealed DNS resolution, mail infrastructure, and domain registration metadata without any active interaction with the target. These findings form the foundation of the reconnaissance phase in a structured penetration test.

The exercise illustrated how a security assessor can construct a detailed intelligence picture of target infrastructure from entirely public sources, prior to any active engagement. The combined intelligence — resolved IP addresses, mail exchange servers, domain registrar details, and authoritative nameservers — directly informs subsequent active scanning, social engineering planning, and phishing surface assessment. Organisations that neglect their OSINT footprint risk exposing significant infrastructure detail to adversaries at zero cost and without detection.

---

## 9. References

Computer Misuse Act 1990 (c.18) UK Parliament. Available at: https://www.legislation.gov.uk/ukpga/1990/18/contents [Accessed: 22 May 2026].

Daigle, L. (2004) RFC 3912: WHOIS Protocol Specification. Available at: https://datatracker.ietf.org/doc/html/rfc3912 [Accessed: 22 May 2026].

Engebretson, P. (2013) The Basics of Hacking and Penetration Testing. 2nd edn. Syngress.

ICANN (2024) WHOIS Lookup and Domain Registration Data. Available at: https://lookup.icann.org/ [Accessed: 22 May 2026].

Mockapetris, P. (1987a) RFC 1034: Domain Names — Concepts and Facilities. Available at: https://datatracker.ietf.org/doc/html/rfc1034 [Accessed: 22 May 2026].

Mockapetris, P. (1987b) RFC 1035: Domain Names — Implementation and Specification. Available at: https://datatracker.ietf.org/doc/html/rfc1035 [Accessed: 22 May 2026].

Nmap.org (2024) Nmap Host Discovery Reference. Available at: https://nmap.org/book/man-host-discovery.html [Accessed: 22 May 2026].

UK Government (2018) Data Protection Act 2018. Available at: https://www.legislation.gov.uk/ukpga/2018/12/contents/enacted [Accessed: 22 May 2026].

---

Report prepared as part of CSO7018 Ethical Hacking, Artefact 2. Student ID: 2416509.
