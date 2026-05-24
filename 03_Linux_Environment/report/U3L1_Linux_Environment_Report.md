# CSO7018 Ethical Hacking — Lab Report
## Unit 3 Lesson 1: Linux Networking Environment

---

| | |
|---|---|
| Student ID | 2416509 |
| Module | CSO7018 Ethical Hacking |
| Assessment | Artefact 2 — VM Lab Practical Activities |
| Activity | Unit 3, Lesson 1 — Linux Networking Fundamentals |
| Date Performed | 22 May 2026 |
| Environment | Kali Linux VM ↔ Metasploitable 2 VM — Authorized University Lab |

---

## Table of Contents

1. Introduction
2. Objectives
3. Lab Environment Configuration
4. Commands Used
5. Findings
 - 5.1 Kali Linux Network Interface
 - 5.2 ICMP Connectivity to Metasploitable 2
 - 5.3 Linux CLI Navigation
 - 5.4 Routing Table
6. Ethical Considerations
7. Reflection
8. Conclusion
9. References

---

## 1. Introduction

A proficient ethical hacker requires fluency with Linux command-line networking utilities. The Kali Linux distribution is the de facto standard platform for penetration testing and ethical hacking, providing a curated collection of security tools alongside the full power of the Linux operating system. Developed and maintained by Offensive Security, Kali Linux is purpose-built for security professionals and ships with hundreds of pre-installed tools spanning network scanning, enumeration, exploitation, password analysis, and digital forensics.

The target for this and all subsequent Unit 3 and Unit 4 activities is Metasploitable 2 — a deliberately vulnerable Ubuntu-based virtual machine developed by Rapid7 for training and Capture the Flag (CTF) purposes. It intentionally contains misconfigured services, outdated software versions, and known exploitable vulnerabilities. Metasploitable 2 must only ever be deployed on an isolated, air-gapped network and must never be exposed to the internet or any production environment.

This activity establishes the foundational networking competencies required for subsequent scanning, enumeration, and exploitation exercises. It covers network interface inspection, connectivity verification between the attacker (Kali) and target (Metasploitable 2) virtual machines, and Linux filesystem navigation.

---

## 2. Objectives

- Identify and document the Kali Linux network interface configuration, including IP address, subnet mask, and MAC address.
- Verify ICMP connectivity between the Kali attacker VM and the Metasploitable 2 target VM.
- Demonstrate proficiency with core Linux CLI navigation commands.
- Confirm the lab networking environment is correctly configured for subsequent practical activities.

---

## 3. Lab Environment Configuration

| Host | Role | OS | IP Address | Adapter |
|------|------|----|------------|---------|
| Kali Linux | Attacker | Kali Linux (Rolling) | 192.168.122.148 | Host-Only / NAT |
| Metasploitable 2 | Target | Ubuntu 8.04 LTS | 192.168.122.108 | Host-Only |

---

## 4. Commands Used

```bash
# Display network interface configuration
ip addr
# or legacy:
ifconfig

# Display routing table
ip route
# or:
netstat -rn

# Test ICMP connectivity to Metasploitable
ping -c 4 <Metasploitable_IP>

# Linux filesystem navigation
pwd           # print working directory
ls -la        # list directory contents
cd /etc       # change directory
cat /etc/hosts  # display file contents
whoami        # display current user
uname -a      # display kernel/OS information
```

---

## 5. Findings

### 5.1 Kali Linux Network Interface

Figure 1: `ip addr` output showing Kali Linux network interface configuration.

Analysis: The Kali Linux VM is configured with IP address `192.168.122.148` on the `192.168.122.0/24` subnet. The interface is in the UP state, confirming active network connectivity on the isolated lab network shared with Metasploitable (`192.168.122.108`) and Ubuntu (`192.168.122.71`).

---

### 5.2 ICMP Connectivity to Metasploitable 2

Figure 2: `ping` command confirming ICMP reachability between Kali and Metasploitable 2.

Analysis: ICMP echo replies were received from Metasploitable 2 at `192.168.122.108`, confirming Layer 3 (network layer) connectivity between the two VMs. The consistent round-trip time indicates a stable, low-latency local virtual network connection. This is a prerequisite verification step before executing any scanning or exploitation activities.

---

### 5.3 Linux CLI Navigation

Figure 3: Linux filesystem navigation commands executed on Kali Linux.

Analysis: Core Linux CLI commands were demonstrated, including directory navigation, file listing, and content viewing. The working directory, file permissions, and directory structure are visible. Proficiency with these commands is essential for post-exploitation activities, such as navigating a compromised system's filesystem.

---

### 5.4 Routing Table

Figure 4: Routing table output from Kali Linux.

Analysis: The routing table confirms the directly connected subnet `192.168.122.0/24`, enabling communication between the Kali VM (`192.168.122.148`), Metasploitable (`192.168.122.108`), and Ubuntu (`192.168.122.71`) on the isolated lab network.

---

## 6. Ethical Considerations

This activity was restricted to the internal VM lab network. All traffic was contained within the isolated virtual network between the Kali and Metasploitable VMs. No external network traffic was generated. The Metasploitable 2 VM is an intentionally vulnerable platform designed exclusively for educational use and is not connected to any production network or the internet.

Even in this controlled educational setting, the core principles of ethical hacking practice were observed throughout:

- Authorization — All activities were explicitly authorized under the CSO7018 module curriculum. No actions were taken outside the defined learning objectives.
- Scope — All network commands were directed exclusively at the designated lab IP addresses (`192.168.122.148` and `192.168.122.108`).
- Non-interference — No system configuration was modified, and no attempt was made to disrupt or alter the target VM beyond the defined exercise tasks.
- Documentation — All activities were recorded with screenshots as evidence of methodology and findings.

These principles reflect the obligations of a professional penetration tester operating under a formal Rules of Engagement agreement in a real-world security assessment context.

---

## 7. Reflection

Establishing the lab environment and verifying connectivity is an often-overlooked but critical step in practical ethical hacking exercises. Incorrect network configuration — such as both VMs being on different subnets, or one VM having a NAT adapter rather than host-only — would cause all subsequent scanning and exploitation attempts to fail.

Understanding the distinction between different virtual adapter types (NAT, host-only, bridged) is directly relevant to understanding how target networks are segmented in real-world environments.

---

## 8. Conclusion

This activity successfully verified the Kali Linux networking environment and confirmed ICMP connectivity to the Metasploitable 2 target VM. The correct network configuration was documented through IP address inspection and ping testing, establishing a validated foundation for all subsequent Unit 3 activities.

The importance of this validation step should not be underestimated: an incorrectly configured virtual network — such as mismatched subnets, bridged rather than host-only adapters, or DHCP assignment to an unexpected address range — would cause all subsequent scanning, enumeration, and exploitation exercises to fail without an obvious explanation. Verifying Layer 3 connectivity and interface assignment prior to active engagement mirrors the environment verification phase required at the commencement of any professional penetration testing engagement.

The Linux CLI commands demonstrated — `ip addr`, `ifconfig`, `ping`, `ip route`, and basic filesystem navigation — are directly applicable in post-exploitation scenarios, where an attacker must navigate and assess a compromised target system from the command line.

---

## 9. References

Barrett, D. and Silverman, R. (2005) Linux Security Cookbook. Sebastopol: O'Reilly Media.

Computer Misuse Act 1990 (c.18) UK Parliament. Available at: https://www.legislation.gov.uk/ukpga/1990/18/contents [Accessed: 22 May 2026].

Kali Linux (2024) Kali Linux Documentation. Available at: https://www.kali.org/docs/ [Accessed: 22 May 2026].

Linux man-pages project (2024) ip(8), ifconfig(8), ping(8) Manual Pages. Available at: https://man7.org/linux/man-pages/ [Accessed: 22 May 2026].

Offensive Security (2024) Kali Linux Revealed: Mastering the Penetration Testing Distribution. Available at: https://kali.training/ [Accessed: 22 May 2026].

Rapid7 (2024a) Metasploitable 2 Exploitability Guide. Available at: https://docs.rapid7.com/metasploit/metasploitable-2-exploitability-guide/ [Accessed: 22 May 2026].

Rapid7 (2024b) Metasploitable 2 Setup Guide. Available at: https://docs.rapid7.com/metasploit/metasploitable-2/ [Accessed: 22 May 2026].

---

Report prepared as part of CSO7018 Ethical Hacking, Artefact 2. Student ID: 2416509.
