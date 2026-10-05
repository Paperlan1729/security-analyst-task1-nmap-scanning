# Security Analyst Task 1: Basic Network Scanning with Nmap

**Author:** Dhrumit Asari  
**GitHub:** [Paperlan1729](https://github.com/Paperlan1729)  
**Track:** Security Analyst (Practical Task)

---

## What is Nmap?

Nmap (Network Mapper) is a free, open-source tool used for network discovery and security auditing. It can determine which hosts are available on a network, what services those hosts are offering, what operating systems they are running, and many other characteristics. Nmap is widely used by security professionals, system administrators, and network engineers.

## Why Network Scanning Matters

Network scanning provides visibility into the actual state of a network. It helps identify:
- Unexpected open ports and services
- Unauthorized or rogue devices
- Outdated or vulnerable service versions
- Attack surface that needs to be reduced

Without regular scanning, organizations operate with incomplete knowledge of their own infrastructure.

## Ethical Use Guidelines

**Only scan systems you own or have explicit written permission to scan.**  
Unauthorized scanning can be illegal and is considered hostile activity. For this task, all scanning was performed exclusively on a local virtual machine under my control. Never scan external, production, or third-party systems without authorization.

---

## Installation Steps (Documented)

### On Kali Linux (recommended for this task)
Nmap comes pre-installed. Verify with:
```bash
nmap --version
```

### On Ubuntu / Debian
```bash
sudo apt update
sudo apt install nmap -y
nmap --version
```

### On Windows
Download the official installer from https://nmap.org/download.html and follow the setup wizard. Nmap can also be used via Windows Subsystem for Linux (WSL).

---

## Scans Performed

Target: Local Kali Linux / Ubuntu VM (example IP: 192.168.56.101 — VirtualBox Host-Only network)

### 1. Basic Scan
```bash
nmap 192.168.56.101
```

### 2. Service Version Detection
```bash
nmap -sV 192.168.56.101
```

### 3. OS Detection
```bash
sudo nmap -O 192.168.56.101
```

Detailed results are recorded in [nmap_scan_results.txt](nmap_scan_results.txt).

---

## Open Ports & Security Analysis

| Port | Service          | Purpose                              | Security Risk Assessment                                                                 |
|------|------------------|--------------------------------------|------------------------------------------------------------------------------------------|
| 22   | SSH              | Secure remote administration         | Medium – Ensure key-based auth only, disable root login, use fail2ban or equivalent      |
| 80   | HTTP             | Web server                           | High if unpatched or misconfigured – Prefer HTTPS, keep software updated                 |
| 443  | HTTPS            | Encrypted web traffic                | Lower risk when properly configured with strong TLS; still monitor for vulnerabilities   |
| 3306 | MySQL            | Database                             | High if exposed – Should not be publicly reachable; bind to localhost or use firewall    |
| 8080 | HTTP-Proxy/Alt   | Alternative web service              | Medium–High – Often used by development tools; restrict access                           |

**Key Observation:** Any service that is not strictly required should be disabled or firewalled. Database ports in particular should never be exposed beyond the application tier.

---

## Files in this Repository

- `nmap_scan_results.txt` — Structured scan output and analysis
- `screenshots/` — Placeholder for terminal screenshots (add your own images here)
- `README.md` — This file

## How to Reproduce

1. Install a local VM (Kali Linux recommended — download from kali.org).
2. Note the VM’s IP address on the host-only or NAT network.
3. Run the Nmap commands shown above.
4. Document results and take screenshots of the terminal.

---

*Completed by Dhrumit Asari as part of the Security Analyst track. All scanning performed on owned local virtual machines only.*
