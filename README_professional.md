<div align="center">

# 🔐 Cybersecurity Lab Environment

### A Professional Virtual Lab for Ethical Hacking, Network Scanning & Security Practice

<p>
  <img src="https://img.shields.io/badge/Focus-Cybersecurity-111827?style=for-the-badge&logo=hackthebox&logoColor=white" />
  <img src="https://img.shields.io/badge/Kali%20Linux-Security%20Lab-557C94?style=for-the-badge&logo=kalilinux&logoColor=white" />
  <img src="https://img.shields.io/badge/VirtualBox-Virtualization-183A61?style=for-the-badge&logo=virtualbox&logoColor=white" />
  <img src="https://img.shields.io/badge/Network%20Scanning-Nmap-0F766E?style=for-the-badge" />
</p>

<p>
  <strong>Yash Anilbhai Jethva</strong><br/>
  Cybersecurity &amp; Network Security Learner
</p>

</div>

---

## 📌 Project Overview

This project documents the design and setup of an **isolated virtual cybersecurity laboratory** for learning, experimentation, network reconnaissance, and authorized security testing.

The laboratory is designed to provide a controlled environment where security tools and techniques can be practiced repeatedly without exposing unauthorized systems to testing activity.

The core environment is based on **Kali Linux** running inside **VirtualBox**, with a dedicated virtual network that can later be extended with additional target machines.

> **Lab principle:** Learn, test, document, reset, and repeat — always within systems you own or have explicit authorization to assess.

---

## 🎯 Objectives

The main objectives of this project are to:

- Build an isolated and reusable cybersecurity practice environment.
- Configure Kali Linux as the primary security-testing workstation.
- Learn virtual networking and VM-to-VM communication.
- Practice network discovery and port scanning in an authorized environment.
- Verify IP addressing, gateway connectivity, and DNS resolution.
- Maintain a clean VM snapshot for safe recovery.
- Document the configuration and troubleshooting process professionally.
- Create a foundation for future penetration-testing and security projects.

---

## 🛡️ Security Scope

This lab may be used for controlled activities such as:

| Activity | Purpose |
|---|---|
| 🔎 Network Reconnaissance | Discover hosts and understand network structure |
| 📡 Port Scanning | Identify exposed services on authorized targets |
| 🧩 Service Enumeration | Understand technologies and network services |
| 🛠️ Vulnerability Assessment | Identify security weaknesses in lab systems |
| 🌐 Web Security Testing | Practice defensive and authorized web testing |
| 📦 Packet Analysis | Study network traffic and protocols |
| 🧪 Security Tool Practice | Learn professional security tooling |
| ♻️ Snapshot Recovery | Restore the lab to a known-good state |

> ⚠️ **Ethical Use:** Only scan, test, or attack machines when you own them or have explicit permission to perform security testing. Never use this laboratory as a basis for unauthorized activity.

---

## 🏗️ Lab Architecture

```text
                       ┌─────────────────────────┐
                       │      Host Computer       │
                       │     Windows / Linux      │
                       └────────────┬────────────┘
                                    │
                              VirtualBox
                                    │
                       ┌────────────▼────────────┐
                       │     Private Lab LAN      │
                       │      10.0.0.0/24*        │
                       └───────┬─────────┬───────┘
                               │         │
                    ┌──────────▼───┐ ┌──▼───────────┐
                    │  Kali Linux  │ │ Target VM(s) │
                    │ Security VM  │ │ Future Labs  │
                    └──────────────┘ └──────────────┘

* Example private range — replace with your actual lab network.
```

The design separates the cybersecurity practice environment from normal everyday systems and makes it possible to add intentionally vulnerable or test machines later.

---

## ⚙️ Lab Configuration

> The values below are a professional configuration template. Replace the placeholder values with the exact specifications of your own machine before publishing the repository.

| Component | Configuration |
|---|---|
| 🖥️ Host OS | `<Your Host OS>` |
| 🧠 Host RAM | `<Your RAM>` |
| ⚡ Processor | `<Your CPU>` |
| 🧰 Hypervisor | VirtualBox |
| 🐉 Security OS | Kali Linux |
| 🧠 Kali RAM | `<Allocated RAM>` |
| 🌐 Virtual Network | NAT Network / Host-Only Network |
| 📡 Network Address | `<Lab Network>/24` |
| 🐧 Kali IP | `<Kali IP>/24` |
| 🚪 Default Gateway | `<Gateway>` |
| 🌍 DNS | `<DNS Server>` |
| 🎯 Future Target Range | `<Target IP Range>` |

---

# 🪜 Lab Setup Procedure

## 1. Install Required Tools

Install the virtualization and archive-management software required for the lab.

### Recommended Tools

- **VirtualBox** — virtual machine platform
- **7-Zip** — archive extraction utility
- **Kali Linux** — security-testing operating system
- **Git** — repository and documentation management

---

## 2. Prepare VirtualBox

Install the latest compatible version of VirtualBox and verify that hardware virtualization is enabled in the system firmware/BIOS when required.

### Checklist

```text
[ ] VirtualBox installed
[ ] Hardware virtualization enabled
[ ] Sufficient RAM available
[ ] Sufficient storage available
[ ] Kali Linux image downloaded
```

---

## 3. Create the Lab Network

Create a dedicated virtual network for the cybersecurity environment.

### Example NAT Network

```text
Network Name : CyberLab
IPv4 Prefix  : 10.0.0.0/24
DHCP         : Enabled or manually managed
IPv6         : Disabled (optional)
```

A dedicated lab network allows multiple virtual machines to communicate with each other while keeping the environment organized and easier to reset.

---

## 4. Install / Import Kali Linux

Import or install Kali Linux into VirtualBox and configure its network adapter to use the dedicated laboratory network.

### Example Adapter Configuration

```text
Adapter 1
Attached to : NAT Network
Network     : CyberLab
```

Allocate enough memory and processor resources for the tools you plan to use, while leaving adequate resources for the host system.

---

## 5. Configure Kali Linux Networking

Verify the assigned interface and network configuration from Kali Linux.

### Useful Commands

```bash
ip a
ip route
cat /etc/resolv.conf
```

Example static configuration format:

```text
IP Address   : 10.0.0.2
Subnet Mask  : 255.255.255.0
Gateway      : 10.0.0.1
DNS          : 8.8.8.8
```

Use the actual values assigned to your laboratory network rather than copying these examples blindly.

---

## 6. Create a Clean Snapshot

Once the operating system, networking, and core tools are working correctly, create a baseline snapshot.

Recommended snapshot name:

```text
CyberLab - Clean Baseline
```

The clean snapshot provides a safe recovery point before performing more experimental activities.

---

# 🔎 Lab Verification

Run basic verification tests before starting security exercises.

| ✅ Test | 🧾 Command | 🎯 Expected Result |
|---|---|---|
| Network interface | `ip a` | Correct IP/interface shown |
| Routing table | `ip route` | Expected gateway present |
| Gateway connectivity | `ping <gateway>` | Replies received |
| Internet connectivity | `ping 8.8.8.8` | Replies received when Internet access is enabled |
| DNS resolution | `nslookup example.com` | Domain resolves successfully |
| Nmap installation | `nmap --version` | Version displayed |
| Snapshot recovery | Restore baseline | Lab returns to known-good state |

### Example Verification Record

```text
Kali IP      : <YOUR_IP>/24
Gateway      : <YOUR_GATEWAY>
DNS          : <YOUR_DNS>
Nmap Version : <VERSION>
Status       : PASS
```

---

# 🔍 Network Scanning Practice

Once the lab is verified, network discovery can be practiced against **authorized laboratory systems only**.

### Basic Host Discovery

```bash
nmap -sn <LAB_NETWORK>/24
```

### Service Discovery

```bash
nmap -sV <AUTHORIZED_TARGET_IP>
```

### Save Scan Results

```bash
nmap -sV <AUTHORIZED_TARGET_IP> -oN scan-results.txt
```

These commands should only be used against systems that are explicitly within the scope of your lab or for which you have authorization.

---

# 🐞 Troubleshooting & Lessons from Common Issues

## Problem 1 — Network Connectivity After IP Changes

Manual network configuration can sometimes cause connectivity problems depending on the active NetworkManager profile.

Useful diagnostic commands:

```bash
nmcli connection show
ip a
ip route
resolvectl status
```

Always identify the actual connection name on your system before modifying a NetworkManager profile.

---

## Problem 2 — Hardware Virtualization Error

A virtual machine may fail to start if hardware virtualization is unavailable or disabled.

### Typical Resolution

1. Restart the computer.
2. Open BIOS/UEFI settings.
3. Enable the CPU virtualization feature.
4. Save the configuration.
5. Restart the system.
6. Launch the VM again.

The exact BIOS/UEFI option name varies by motherboard and processor manufacturer.

---

# 💡 What I Learned

This project helped me build practical foundations in:

### 1. Virtualization

Understanding how VirtualBox creates isolated virtual machines and how VM resources can be allocated safely.

### 2. Network Configuration

Learning the relationship between IP addresses, subnet masks, gateways, DNS, routes, and virtual network adapters.

### 3. Kali Linux

Working with a security-focused Linux environment and becoming familiar with command-line security tools.

### 4. Network Scanning

Developing practical understanding of host discovery, open ports, services, and basic network reconnaissance in an authorized environment.

### 5. Recovery & Documentation

Learning why clean snapshots, structured notes, screenshots, commands, and troubleshooting records are essential in a professional security workflow.

---

# 📚 Skills Demonstrated

<p>
  <img src="https://img.shields.io/badge/Kali%20Linux-Security%20Lab-557C94?style=flat-square&logo=kalilinux&logoColor=white" />
  <img src="https://img.shields.io/badge/Network%20Scanning-Skill-0F766E?style=flat-square" />
  <img src="https://img.shields.io/badge/Linux-Skill-111827?style=flat-square&logo=linux&logoColor=white" />
  <img src="https://img.shields.io/badge/Virtualization-VirtualBox-183A61?style=flat-square&logo=virtualbox&logoColor=white" />
  <img src="https://img.shields.io/badge/Cybersecurity-Learning-7C3AED?style=flat-square" />
</p>

---

# 🏆 Certifications & Learning

### Workshop Certification

**TTU Security Pvt. Ltd.**  
Cybersecurity / Security Workshop

### EC-Council Certification

**Introduction to Dark Web Anonymity and Cryptocurrency**  
EC-Council

> Add certificate IDs, dates, or verification links here when you publish the repository.

---

# 🔐 Security & Ethical Use

This repository is intended for **education, authorized security testing, and professional skill development**.

Do not use the tools, techniques, commands, or knowledge documented here against systems without authorization.

The safest cybersecurity workflow is:

```text
Define Scope
     ↓
Build Lab
     ↓
Verify Targets
     ↓
Test Responsibly
     ↓
Document Findings
     ↓
Restore Snapshot
     ↓
Improve
```

---

# 🔗 Useful Resources

- [Kali Linux](https://www.kali.org/)
- [VirtualBox](https://www.virtualbox.org/)
- [Nmap](https://nmap.org/)
- [EC-Council](https://www.eccouncil.org/)
- [7-Zip](https://www.7-zip.org/)

---

# 👤 Author

<div align="center">

## Yash Anilbhai Jethva

**Cybersecurity | Network Security | Ethical Hacking Enthusiast**

🎓 **GTU Graduate — 8.20 CGPA**  
💻 **Core Skills:** Kali Linux · Network Scanning · Linux · Cybersecurity Fundamentals

</div>

---

# 📌 Project Information

| Field | Details |
|---|---|
| 👤 Author | Yash Anilbhai Jethva |
| 🎓 Education | GTU Graduate |
| ⭐ CGPA | 8.20 |
| 🔐 Domain | Cybersecurity & Network Security |
| 🧰 Primary Platform | Kali Linux + VirtualBox |
| 🧪 Project Type | Practical Cybersecurity Lab |
| 📖 Documentation | GitHub README |

---

<div align="center">

### ⭐ Built for Learning. Secured by Practice. Documented Professionally.

**© Yash Anilbhai Jethva**

</div>
