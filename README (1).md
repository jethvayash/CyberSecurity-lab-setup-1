<div align="center">

# 🔐 Cybersecurity Lab Environment Setup

**Building an isolated virtual lab for penetration testing, red teaming, and ethical hacking practice**

</div>

<p align="center">
  <img src="https://img.shields.io/badge/Skill-Cybersecurity-404040?style=flat-square&labelColor=C00000" />
  <img src="https://img.shields.io/badge/Ver-Virtualbox%20v7.2-0070C0?style=flat-square&labelColor=000000" />
  <img src="https://img.shields.io/badge/Kali%20Linux-v2026.2-E87500?style=flat-square&labelColor=000000&logo=kalilinux&logoColor=white" />
  <img src="https://img.shields.io/badge/Skill-Linux-404040?style=flat-square&labelColor=C00000" />
  <img src="https://img.shields.io/badge/Network-10.0.0.0%2F24-238F89?style=flat-square&labelColor=000000" />
  <img src="https://img.shields.io/badge/Penetration%20Testing-C00000?style=flat-square&labelColor=000000&logo=kalilinux&logoColor=white" />
  <img src="https://img.shields.io/badge/Skill-Virtualization-404040?style=flat-square&labelColor=C00000" />
  <img src="https://img.shields.io/badge/GitHub-404040?style=flat-square&labelColor=0070C0&logo=github&logoColor=white" />
  <img src="https://img.shields.io/badge/Red%20Team-404040?style=flat-square&labelColor=C00000&logo=kalilinux&logoColor=white" />
  <img src="https://img.shields.io/badge/Ethical%20Hacking-E87500?style=flat-square&labelColor=000000&logo=kalilinux&logoColor=white" />
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Status-Active-brightgreen?style=flat-square" />
  <img src="https://img.shields.io/badge/License-Educational%20Use-blue?style=flat-square" />
  <img src="https://img.shields.io/badge/Maintained-Yes-success?style=flat-square" />
</p>

---

## 📖 Table of Contents

1. [Project Overview](#-project-overview)
2. [Objectives](#-objectives)
3. [Purpose of the Lab](#️-purpose-of-the-lab)
4. [Lab Architecture](#️-lab-architecture)
5. [Lab Configuration](#️-lab-configuration)
6. [Setup Procedure](#-lab-setup-procedure)
7. [Lab Verification](#-lab-verification)
8. [Problems Encountered & Solutions](#-problems-encountered--solutions)
9. [What I Learned](#-what-i-learned)
10. [Security & Ethical Use](#-security--ethical-use)
11. [Tools & Resources](#-tools--resources)
12. [Author](#-author)

---

## 📌 Project Overview

This project documents the setup of a **fully isolated virtual cybersecurity and penetration-testing laboratory** using VirtualBox and Kali Linux.

The lab provides a controlled, repeatable environment for practicing network scanning, reconnaissance, vulnerability assessment, and other offensive-security techniques — without touching production systems or the public internet.

It is built on a private virtual network so that additional vulnerable/target machines can be added later for structured, authorized security testing exercises.

> 💡 **Why this matters:** A dedicated lab is the foundation of practical cybersecurity skill-building — it's where OSCP-track techniques, OWASP concepts, and red-team methodology move from theory into hands-on practice.

---

## 🎯 Objectives

- ✅ Install and configure VirtualBox as the hypervisor
- ✅ Install / import Kali Linux as a virtual machine
- ✅ Create a private **NAT Network** dedicated to the lab
- ✅ Configure network connectivity for Kali Linux
- ✅ Assign a consistent, documented IP address to the Kali VM
- ✅ Verify network connectivity and DNS resolution
- ✅ Capture a clean VM snapshot as a recovery baseline
- ✅ Fully document the setup process, issues, and fixes
- ✅ Prepare the environment for future offensive-security projects

---

## 🛡️ Purpose of the Lab

The lab creates an isolated, controlled environment for cybersecurity learning and **authorized** security testing. It is intended to support activities such as:

| Category | Example Activities |
|---|---|
| 🌐 Network Reconnaissance | Host discovery, service enumeration, topology mapping |
| 🔎 Port Scanning | Nmap scans, service/version fingerprinting |
| 🧪 Vulnerability Assessment | CVE identification, misconfiguration analysis |
| 📡 Packet Analysis | Wireshark captures, traffic inspection |
| 🕸️ Web Security Testing | OWASP Top 10 practice, Burp Suite testing |
| 💥 Exploitation Practice | Controlled exploitation of intentionally vulnerable VMs |
| 🧰 Security Tool Experimentation | Testing and benchmarking new tools safely |

> ⚠️ **Important:** This laboratory is to be used exclusively on systems that are owned by the operator or for which explicit written authorization has been granted. It must never be used against unauthorized systems, networks, or third parties.

---

## 🏗️ Lab Architecture

```
                    ┌─────────────────────────────┐
                    │        Host Machine         │
                    │   (Windows / Linux / macOS)  │
                    └──────────────┬───────────────┘
                                   │
                          VirtualBox Hypervisor
                                   │
                    ┌──────────────┴───────────────┐
                    │   NAT Network: NatNetwork     │
                    │   Subnet: 10.0.0.0/24         │
                    │   Gateway: 10.0.0.1            │
                    └──────────────┬───────────────┘
                                   │
              ┌────────────────────┼────────────────────┐
              │                    │                     │
   ┌──────────▼─────────┐  ┌───────▼────────┐  ┌────────▼─────────┐
   │   Kali Linux (Attacker) │  Future Target 1 │  │  Future Target 2  │
   │   10.0.0.2/24        │  │  10.0.0.3/24    │  │  10.0.0.4/24      │
   └──────────────────────┘  └─────────────────┘  └───────────────────┘
```

*(Replace this diagram with your own screenshot — e.g. `1-screenshot-title-image.png` — once your lab is running.)*

Additional target machines (DVWA, Metasploitable, vulnerable web apps, etc.) can be added to the same virtual network in future projects for structured attack-practice exercises.

---

## ⚙️ Lab Configuration

| 🧩 Component        | ⚙️ Configuration        |
| -------------------- | ------------------------ |
| 🖥️ Host OS           | *(e.g. Windows 11 / Ubuntu 24.04)* |
| 🧠 Host RAM           | *(e.g. 8–16 GB)*         |
| ⚡ Processor          | *(e.g. Intel Core i5/i7)*|
| 🧰 Hypervisor         | VirtualBox 7.2           |
| 🐉 Security OS        | Kali Linux 2026.2        |
| 🧠 Kali RAM            | 2048 MB                  |
| 💾 Kali Disk           | *(e.g. 40 GB dynamic)*   |
| 🌐 Virtual Network    | NAT Network               |
| 📡 Network Address    | 10.0.0.0/24               |
| 🐧 Kali IP Address    | 10.0.0.2/24                |
| 🚪 Default Gateway    | 10.0.0.1                   |
| 🌍 DNS Server          | 8.8.8.8                    |
| 🔮 Future VM Range    | 10.0.0.3 – 10.0.0.99       |

---

# 🪜 Lab Setup Procedure

### Step 1 — Install 7-Zip

7-Zip is used to extract the Kali Linux VM package, which is often distributed as a `.7z` archive.

**Tool:** [7-Zip](https://7-zip.org/download.html)

---

### Step 2 — Install VirtualBox

Install VirtualBox as the hypervisor that will host and manage all lab virtual machines.

**Tool:** [VirtualBox](https://virtualbox.org/wiki/Downloads)

---

### Step 3 — Create the NAT Network

A dedicated NAT Network was created in VirtualBox to isolate the lab from the host's regular network while still allowing internet access for updates.

```text
Network Name : NatNetwork
IPv4 Prefix  : 10.0.0.0/24
DHCP         : Enabled
IPv6         : Disabled
```

*(Insert screenshot: `2-screenshot-network-settings.png`)*

> A **NAT Network** was chosen (rather than a standard NAT adapter) because multiple VMs attached to the same NAT Network can communicate with **each other** while still retaining outbound internet connectivity. This is essential for future attacker ↔ target communication.

---

### Step 4 — Import Kali Linux

The Kali Linux VM was downloaded from the [official Kali Linux site](https://kali.org/get-kali) and imported into VirtualBox.

**Network adapter configuration:**

```text
Adapter 1
Attached to  : NAT Network
Network      : NatNetwork
Adapter Type : Intel PRO/1000 MT Desktop
```

**Allocated resources:**

```text
RAM : 2048 MB
```

*(Insert screenshot: `3-screenshot-kali-linux.png`)*

A shared folder was also configured to transfer files easily between the host OS and the Kali VM.

---

### Step 5 — Configure the Kali Linux Network

The Kali network configuration was set to a consistent, documented IPv4 address for reliability across future exercises.

```text
IP Address  : 10.0.0.2
Subnet Mask : 255.255.255.0
Gateway     : 10.0.0.1
DNS         : 8.8.8.8
```

*(Insert screenshot: `4-screenshot-kali-network-settings.png`)*

---

### Step 6 — Create a Clean VM Snapshot

Once configuration was complete, a VirtualBox snapshot was taken to establish a known-good baseline.

```text
Snapshot Name : Clean Kali - Network Setup
```

This snapshot allows the VM to be restored instantly if a future exercise breaks or damages the configuration.

---

# 🔎 Lab Verification

| ✅ Test | 🧾 Command | 🎯 Expected Result |
|---|---|---|
| 🌐 Check IP address | `ip a` | Correct Kali IP displayed |
| 📡 Test gateway | `ping 10.0.0.1` | Successful replies |
| 🌍 Test internet connectivity | `ping 8.8.8.8` | Successful replies |
| 🔎 Test DNS resolution | `nslookup kali.org` | Domain resolves correctly |
| 🧰 Verify Nmap | `nmap --version` | Nmap version displayed |
| 🔄 Verify snapshot | Restore snapshot → run `ip a` | Baseline configuration restored |

**Example results:**

```text
IP Address : 10.0.0.2/24
Gateway    : 10.0.0.1
DNS        : 8.8.8.8
Status     : ✅ All checks passed
```

---

# 🐞 Problems Encountered & Solutions

Documenting issues is a core part of professional lab work — it builds a troubleshooting reference for future projects.

### Problem 1 — Internet Connectivity Lost After Static IP Configuration

**Symptom:** After manually setting the static IPv4 address, internet connectivity failed intermittently.

**Fix:**

```bash
sudo nmcli connection modify "Wired connection 1" ipv4.dad-timeout 0
```

The connection was then restarted and connectivity re-tested successfully.

> **Note:** Interface and connection names vary between systems. Run `nmcli connection show` first to confirm the exact connection name before applying this fix.

---

### Problem 2 — VirtualBox VT-x / Virtualization Error

**Symptom:** The VM failed to start with a hardware virtualization error.

**Root cause:** Intel VT-x was disabled in the system BIOS/UEFI.

**Fix:**

1. Restart the computer and enter BIOS/UEFI setup.
2. Locate and enable **Intel VT-x** (or AMD-V on AMD systems).
3. Save the configuration and exit.
4. Restart the computer.
5. Start the Kali VM again.

✅ The VM started successfully after enabling virtualization support.

---

# 💡 What I Learned

### 1. NAT vs. NAT Network
A standard NAT adapter isolates each VM individually, while a **NAT Network** allows multiple VMs to communicate with each other while still sharing outbound internet access — critical for building a multi-machine lab.

### 2. Virtual Machine Networking
How VirtualBox's virtual adapters connect VMs to different network types, and how that configuration governs inter-VM communication.

### 3. Static IP Configuration
How to configure and verify IPv4 addressing, subnet masks, gateways, and DNS on Kali Linux via both GUI and `nmcli`.

### 4. VM Snapshots
The importance of capturing a **clean snapshot before** risky or experimental activity, giving a reliable rollback point.

### 5. Structured Documentation
How to document commands, configurations, screenshots, problems, and solutions in a way that's clear, reproducible, and professional.

---

# 🔐 Security & Ethical Use

This lab is built and maintained **strictly for educational purposes** and authorized security research.

- 🚫 Never test systems you do not own or lack explicit written permission to test.
- 🔒 Keep the lab network isolated from production/host networks where possible.
- 📜 Follow responsible disclosure practices for any real-world findings.
- 🧠 Use this environment to build skills aligned with certifications such as **OSCP**, **CEH**, and coursework like **RCET / MSc Cybersecurity & Digital Forensics**.

---

# 🔗 Tools & Resources

- **7-Zip:** [https://7-zip.org/download.html](https://7-zip.org/download.html)
- **VirtualBox:** [https://virtualbox.org/wiki/Downloads](https://virtualbox.org/wiki/Downloads)
- **Kali Linux:** [https://kali.org/get-kali](https://kali.org/get-kali)
- **OWASP Top 10:** [https://owasp.org/www-project-top-ten/](https://owasp.org/www-project-top-ten/)
- **Metasploitable (target practice VM):** [https://sourceforge.net/projects/metasploitable/](https://sourceforge.net/projects/metasploitable/)

---

# 👤 Author

**[Your Name]**
BSc IT Student | Cybersecurity & Red Team Enthusiast

📎 GitHub: `github.com/yourusername`
📎 LinkedIn: `linkedin.com/in/yourusername`

---

## 📌 Project Information

**Project:** Cybersecurity & Pentesting Lab Setup &nbsp;|&nbsp; **Week:** 01 &nbsp;|&nbsp; **Repository:** GitHub

