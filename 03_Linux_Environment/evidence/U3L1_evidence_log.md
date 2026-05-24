# Evidence Log — Unit 3 Lesson 1: Linux Environment & Networking
Student ID: 2416509 | Module: CSO7018 Ethical Hacking
Activity: Linux networking fundamentals — interface configuration, connectivity verification
Date: 22 May 2026
Environment: Kali Linux VM ↔ Metasploitable 2 VM (authorized university lab)
Kali IP: 192.168.122.148 | Metasploitable IP: 192.168.122.108 | Ubuntu IP: 192.168.122.71

---

## Evidence Table

| # | Screenshot | Command | Purpose | Key Findings | Interpretation |
|---|-----------|---------|---------|--------------|----------------|
| 1 | `U3L1_01_vm_boot_login.png` | VM boot sequence | Start up lab environment | VMs booting up | Lab environment initialising |
| 2 | `U3L1_02_metasploitable_login.png` | Login to Metasploitable | Authenticate to target VM | Login prompt / successful login | Access to target VM confirmed |
| 3 | `U3L1_03_kali_desktop.png` | Kali Linux desktop | Verify attacker VM running | Kali desktop visible | Attacker platform ready |
| 4 | `U3L1_04_metasploitable_hostname_uname.png` | `hostname; uname -a; cat /etc/os-release` | Identify system and OS info | Hostname: metasploitable; kernel 2.6.24-16; Ubuntu | Target system: Metasploitable 2 (Ubuntu, kernel 2.6.24, i686) |
| 5 | `U3L1_05_linux_file_system.png` | `ls /; ls /home` | Explore file system structure | Root directory and home directories listed | Standard Linux file hierarchy confirmed |
| 6 | `U3L1_06_linux_network_ifconfig.png` | `ifconfig` or `ip addr` | View network interface configuration | IP address, subnet mask, MAC address | Network configuration documented; IP identified for lab use |
| 7 | `U3L1_07_linux_users_etc_passwd.png` | `cat /etc/passwd` | List system users | User accounts visible | Multiple service accounts present; attack surface noted |
| 8 | `U3L1_08_linux_processes_ps.png` | `ps aux` | List running processes | Active processes shown | Service processes identified |
| 9 | `U3L1_09_linux_services_running.png` | `service --status-all` or `netstat` | Check running services | Active services listed | Service inventory compiled |
| 10 | `U3L1_10_linux_netstat_ports.png` | `netstat -tuln` | List open ports and listening services | Open TCP/UDP ports | Port inventory for target VM |
| 11 | `U3L1_11_linux_file_permissions.png` | `ls -la` | Inspect file permissions | Permission bits visible | Potential misconfiguration identified |
| 12 | `U3L1_12_linux_package_info.png` | `dpkg -l` or `apt list` | List installed packages | Package list shown | Installed software inventory |
| 13 | `U3L1_13_linux_logs_var_log.png` | `ls /var/log; cat /var/log/auth.log` | Examine system logs | Log files visible | Log analysis capability demonstrated |
| 14 | `U3L1_14_linux_cronjobs.png` | `crontab -l; cat /etc/cron*` | Check scheduled tasks | Cron entries visible | Scheduled task persistence mechanism |
| 15 | `U3L1_15_linux_environment_complete.png` | Final environment check | Document completed setup | Environment overview | Lab environment fully configured |

---

## Notes

- Connectivity between the Kali and Metasploitable VMs was verified before proceeding with scanning exercises.
- The host-only or NAT network adapter configuration was used per lab instructions.

---

## Ethical Note

This activity involved only the internal lab VM network. No external network traffic was generated. The Metasploitable 2 VM is an intentionally vulnerable target designed for educational use and is not connected to any production or external network.

---

Evidence log last updated: 22 May 2026
