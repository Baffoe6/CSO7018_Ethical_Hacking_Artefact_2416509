# Evidence Log — Unit 4 Lesson 3: Metasploit FTP Exploitation
Student ID: 2416509 | Module: CSO7018 Ethical Hacking
Activity: Controlled exploitation of vsftpd 2.3.4 backdoor via Metasploit Framework
Date: 22 May 2026
Environment: Kali Linux → Metasploitable 2 (authorized university lab)
Exploit Module: `exploit/unix/ftp/vsftpd_234_backdoor`
Attacker IP: 192.168.122.148 | Target IP: 192.168.122.108 | Target Port: 21 (FTP)
CVE: CVE-2011-2523

---

## Evidence Table

| # | Screenshot | Command | Purpose | Key Findings | Interpretation |
|---|-----------|---------|---------|--------------|----------------|
| 1 | `U4L3_01_nmap_recon_metasploitable.png` | `nmap <target>` | Initial recon scan of target | Open ports including port 21 (FTP) | Target fingerprinted; attack surface identified |
| 2 | `U4L3_02_nmap_ftp_port_open.png` | `nmap -sV -p 21 <target>` | Confirm FTP service version | vsftpd 2.3.4 on port 21 | Vulnerable version confirmed; CVE-2011-2523 applicable |
| 3 | `U4L3_03_msfconsole_launch.png` | `msfconsole` | Launch Metasploit Framework | MSF banner and prompt `msf6 >` | Metasploit ready for exploitation |
| 4 | `U4L3_04_msf_search_vsftpd.png` | `search vsftpd` | Find vsftpd exploit module | `exploit/unix/ftp/vsftpd_234_backdoor` listed | CVE-2011-2523 exploit module identified |
| 5 | `U4L3_05_msf_use_exploit.png` | `use exploit/unix/ftp/vsftpd_234_backdoor; set RHOSTS <IP>` | Load exploit and set target | Module loaded; RHOSTS configured | Exploit armed and targeted at Metasploitable |
| 6 | `U4L3_06_msf_set_options_run.png` | `show options; run` | Confirm settings and execute exploit | Options confirmed; exploit running | Backdoor trigger sent to vsftpd on port 21 |
| 7 | `U4L3_07_msf_shell_etc_shadow.png` | `cat /etc/shadow` | Demonstrate root access via shell | /etc/shadow contents visible including root hash | Root-level command execution confirmed; password hashes exposed |
| 8 | `U4L3_08_msf_root_access_confirmed.png` | `cat /etc/shadow` (continued) | Full shadow file review | All user accounts: msfadmin, postgres, user, service, etc. | Complete credential exposure; full system compromise demonstrated |

---

## Exploit Technical Detail

| Attribute | Value |
|-----------|-------|
| CVE | CVE-2011-2523 |
| CVSS v2 Score | 10.0 (Critical) |
| Vulnerability Type | Backdoor command execution |
| Affected Software | vsftpd 2.3.4 |
| Exploitation Mechanism | Sending `:)` in the FTP username triggers backdoor shell on port 6200 |
| Payload | Unix command shell (bind/reverse) |
| Access Level Obtained | Root (uid=0) |

---

## Attack Chain Summary

```
1. Nmap service discovery → vsftpd 2.3.4 identified on port 21
2. CVE-2011-2523 matched to service version
3. Metasploit module: exploit/unix/ftp/vsftpd_234_backdoor selected
4. RHOSTS configured to Metasploitable 2 IP
5. exploit command executed
6. Backdoor triggered → root shell opened
7. whoami / id confirmed root access
```

---

## Ethical Note

This exploitation activity was performed exclusively against the Metasploitable 2 virtual machine, an intentionally vulnerable training platform specifically designed for this type of authorized educational exercise. The vsftpd 2.3.4 backdoor (CVE-2011-2523) is a known, documented vulnerability included in Metasploitable 2 for teaching purposes. This exercise was conducted under the direct authorization of the CSO7018 module curriculum and did not involve any real-world, production, or external system.

---

Evidence log last updated: 22 May 2026
