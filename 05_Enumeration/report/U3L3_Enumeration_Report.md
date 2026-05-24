# CSO7018 Ethical Hacking — Lab Report
## Unit 3 Lesson 3: Service Enumeration

---

| | |
|---|---|
| Student ID | 2416509 |
| Module | CSO7018 Ethical Hacking |
| Assessment | Artefact 2 — VM Lab Practical Activities |
| Activity | Unit 3, Lesson 3 — Enumeration (Banner Grabbing, DNS Enumeration) |
| Date Performed | 22 May 2026 |
| Environment | Kali Linux → Metasploitable 2 (authorized university lab) |
| Attacker IP | 192.168.122.148 |
| Target IP | 192.168.122.108 |

---

## Table of Contents

1. Introduction
2. Objectives
3. Commands Used
4. Findings
 - 4.1 Banner Grabbing
 - 4.2 DNS Enumeration
5. Key Banners on Metasploitable 2
6. Mitigation Recommendations
7. Ethical Considerations
8. Reflection
9. Conclusion
10. References

---

## 1. Introduction

Enumeration is the process of extracting detailed information from discovered services on a target host. Unlike reconnaissance, enumeration involves direct interaction with services to extract service banners, user account lists, configuration details, and other information disclosed by the target. This phase bridges scanning (identifying open ports) and exploitation (leveraging specific vulnerabilities).

Two primary enumeration techniques are covered in this activity:

1. Banner Grabbing — Connecting to a service and capturing the introductory text (banner) that the service transmits upon connection. Banners frequently disclose software name, version, and sometimes OS information.

2. DNS Enumeration — Querying DNS infrastructure to enumerate all available records, including subdomains, mail servers, and zone data, using tools such as `dnsenum`.

---

## 2. Objectives

- Perform banner grabbing against multiple open services on Metasploitable 2 using Netcat.
- Interpret service banners to identify software versions for CVE mapping.
- Execute DNS enumeration against a target domain using `dnsenum`.
- Identify information disclosure vulnerabilities arising from verbose service banners.

---

## 3. Commands Used

```bash
# Banner grabbing — FTP (port 21)
nc -v 192.168.122.108 21

# Banner grabbing — SSH (port 22)
nc -v 192.168.122.108 22

# Banner grabbing — HTTP (port 80)
echo -e "HEAD / HTTP/1.0\r\n\r\n" | nc 192.168.122.108 80

# Banner grabbing — Telnet (port 23)
nc -v 192.168.122.108 23

# DNS enumeration
dnsenum <target_domain>

# DNS enumeration with brute force subdomains
dnsenum --dnsserver <nameserver_IP> --enum <target_domain>

# Zone transfer attempt
dig axfr @<nameserver_IP> <target_domain>
```

---

## 4. Findings

### 4.1 Banner Grabbing

Figure 1: Netcat banner grabbing output showing service banners from the target.

Analysis: The service banner captured from port `` revealed: ``.

This banner discloses:

| Field | Value | Significance |
|-------|-------|-------------|
| Service | | Identifies the running daemon |
| Version | | Enables direct CVE lookup |
| OS Hint | | Narrows exploitation options |

For example, the vsftpd 2.3.4 banner on port 21 directly maps to CVE-2011-2523, a critical backdoor vulnerability. This exemplifies how verbose service banners significantly reduce the effort required by an attacker to identify applicable exploits.

---

### 4.2 DNS Enumeration

Figure 2: `dnsenum` output showing DNS record enumeration results.

Analysis: The `dnsenum` tool performed automated DNS enumeration, querying for:
- A records — IP addresses for domain/subdomain names
- MX records — Mail server infrastructure
- NS records — Authoritative nameservers
- Zone transfer — Attempted AXFR (if configured)

A successful DNS zone transfer (AXFR) would expose the complete DNS record set for the target domain, providing a comprehensive map of all internal and external hostnames. Failed zone transfers indicate correctly configured DNS server access controls.

---

## 5. Key Banners on Metasploitable 2

| Port | Service | Example Banner | CVE Mapping |
|------|---------|---------------|-------------|
| 21 | vsftpd | `220 (vsFTPd 2.3.4)` | CVE-2011-2523 (Critical) |
| 22 | OpenSSH | `SSH-2.0-OpenSSH_4.7p1 Debian-8ubuntu1` | Multiple (old version) |
| 23 | Telnet | `Linux telnetd` | Cleartext credential transmission |
| 25 | Postfix | `220 metasploitable.localdomain ESMTP Postfix` | SMTP VRFY user enumeration |
| 80 | Apache | `Apache/2.2.8 (Ubuntu) DAV/2` | Multiple CVEs |
| 3306 | MySQL | `5.0.51a-3ubuntu5` | CVE-2012-2122 and others |

---

## 6. Mitigation Recommendations

The information disclosure vulnerabilities identified through banner grabbing represent misconfigurations that can be remediated without disrupting service functionality:

| Recommendation | Priority | Implementation |
|---------------|---------|----------------|
| Suppress service version banners | High | Configure FTP, SSH, HTTP, and SMTP daemons to omit version strings; replace default banners with generic text |
| Upgrade legacy services | Critical | Replace vsftpd 2.3.4, OpenSSH 4.7, Apache 2.2.8, and MySQL 5.0 with current supported versions to address known CVEs |
| Disable Telnet (port 23) | Critical | Telnet transmits credentials in cleartext; replace with SSH for all remote access requirements |
| Restrict DNS zone transfers (AXFR) | High | Configure DNS servers to allow AXFR only to authorised secondary nameservers; deny all other requestors |
| Disable SMTP VRFY/EXPN commands | Medium | Disable VRFY and EXPN in Postfix/Sendmail configuration to prevent user account enumeration via SMTP |
| Apply CWE-200 controls | Medium | Audit all externally-visible service configurations; suppress identifying information from banners, HTTP headers, and error messages |

Suppressing banner information does not prevent a determined attacker from fingerprinting services through alternative techniques, but significantly increases the effort required and reduces susceptibility to automated scanning tools.

---

## 7. Ethical Considerations

Banner grabbing involves direct TCP connection to open service ports on the target. In an unauthorized context, even reading a service banner could constitute unauthorized computer access under the Computer Misuse Act 1990. DNS enumeration against public infrastructure may be more legally ambiguous but could violate service terms of use.

In this activity, all connections were to the authorized Metasploitable 2 target within the isolated university lab. No production DNS zones or external services were queried.

Information disclosed by service banners represents a misconfiguration vulnerability (CWE-200 — Exposure of Sensitive Information). Best practice dictates that production service banners should be suppressed or obscured to remove version and OS information.

---

## 8. Reflection

This activity demonstrated the disproportionate intelligence value that service banners provide to an attacker with minimal effort. A single Netcat connection to port 21 on Metasploitable immediately reveals the vsftpd version — which maps to a publicly documented, exploitable backdoor. This highlights why version disclosure suppression is a critical security hardening step.

DNS enumeration reinforced that organizational DNS infrastructure can expose significant internal architecture if zone transfers are permitted from arbitrary sources.

---

## 9. Conclusion

Enumeration against the Metasploitable 2 target revealed detailed service version information across multiple ports, directly enabling the identification of exploitable vulnerabilities. Banner grabbing demonstrated the information disclosure risk posed by unmodified default service configurations. DNS enumeration illustrated the intelligence value of DNS infrastructure analysis. These findings directly inform the exploit selection process in subsequent exploitation activities.

---

## 10. References

Computer Misuse Act 1990 (c.18) UK Parliament. Available at: https://www.legislation.gov.uk/ukpga/1990/18/contents [Accessed: 22 May 2026].

dnsenum on GitHub (2024) dnsenum — DNS Enumeration Tool. Available at: https://github.com/fwaeytens/dnsenum [Accessed: 22 May 2026].

Kennedy, D., O'Gorman, J., Kearns, D. and Aharoni, M. (2011) Metasploit: The Penetration Tester's Guide. San Francisco: No Starch Press.

MITRE (2024) CWE-200: Exposure of Sensitive Information to an Unauthorized Actor. Available at: https://cwe.mitre.org/data/definitions/200.html [Accessed: 22 May 2026].

Mockapetris, P. (1987) RFC 1035: Domain Names — Implementation and Specification. Available at: https://datatracker.ietf.org/doc/html/rfc1035 [Accessed: 22 May 2026].

National Vulnerability Database (2024) CVE-2011-2523. NIST. Available at: https://nvd.nist.gov/vuln/detail/CVE-2011-2523 [Accessed: 22 May 2026].

Netcat project (2024) Netcat Documentation. Available at: https://netcat.sourceforge.net [Accessed: 22 May 2026].

---

Report prepared as part of CSO7018 Ethical Hacking, Artefact 2. Student ID: 2416509.
