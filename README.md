<div align="center">

# 🔐 Cyber-Range Engineering: Isolated Penetration-Testing Laboratory

### *A Self-Directed Systems Project in Offensive Security Infrastructure*

**Author:** [Your Name] · BSc Information Technology
**Focus Areas:** Ethical Hacking · Red Teaming · Network Security · Digital Forensics

</div>

<p align="center">
  <img src="https://img.shields.io/badge/Discipline-Offensive%20Security-1a1a2e?style=for-the-badge&labelColor=8B0000" />
  <img src="https://img.shields.io/badge/Hypervisor-VirtualBox%207.2-1a1a2e?style=for-the-badge&labelColor=003153" />
  <img src="https://img.shields.io/badge/Platform-Kali%20Linux%202026.2-1a1a2e?style=for-the-badge&labelColor=D2691E&logo=kalilinux&logoColor=white" />
  <img src="https://img.shields.io/badge/Topology-Segmented%20NAT-1a1a2e?style=for-the-badge&labelColor=0F4C3A" />
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Status-Completed-2ecc71?style=flat-square" />
  <img src="https://img.shields.io/badge/Category-Academic%20Portfolio-blue?style=flat-square" />
  <img src="https://img.shields.io/badge/Certification%20Track-OSCP%20%7C%20CEH-9b59b6?style=flat-square" />
  <img src="https://img.shields.io/badge/Institution-BSc%20IT-orange?style=flat-square" />
</p>

<p align="center">
  <sub>📅 Documented as part of ongoing self-study toward a career in cybersecurity and digital forensics</sub>
</p>

---

## 📇 Candidate Snapshot

> A brief orientation for reviewers, mentors, or recruiters assessing this work.

| | |
|---|---|
| 🎓 **Academic Standing** | BSc Information Technology (in progress) |
| 🧭 **Career Trajectory** | Cybersecurity · Ethical Hacking · Red Team Operations |
| 📚 **Next Milestone** | MSc Cybersecurity & Digital Forensics (RCET-track admission) |
| 🛠️ **Core Toolkit** | Kali Linux, VirtualBox, Nmap, Burp Suite, OWASP methodology |
| 🧠 **Learning Philosophy** | Build, break, document, repeat — infrastructure literacy before exploitation literacy |

---

## 📖 Table of Contents

| Section | Description |
|---|---|
| [01 · Project Rationale](#01--project-rationale) | Why this lab exists and what it demonstrates |
| [02 · Learning Objectives](#02--learning-objectives) | Competencies this project was designed to build |
| [03 · Scope & Ethical Boundaries](#03--scope--ethical-boundaries) | Authorized-use framework |
| [04 · System Architecture](#04--system-architecture) | Network topology and design logic |
| [05 · Environment Specification](#05--environment-specification) | Full hardware/software baseline |
| [06 · Build Log](#06--build-log) | Step-by-step provisioning record |
| [07 · Verification Suite](#07--verification-suite) | Proof-of-function testing |
| [08 · Troubleshooting Journal](#08--troubleshooting-journal) | Real issues, real fixes |
| [09 · Key Takeaways](#09--key-takeaways) | Skills demonstrated |
| [10 · Roadmap](#10--roadmap) | What's planned next |
| [11 · References](#11--references) | Tools and resources |
| [12 · Contact](#12--contact) | Author details |

---

## 01 · Project Rationale

Every offensive-security skill — reconnaissance, enumeration, exploitation, reporting — depends on having somewhere safe to practice it. Before touching a single security tool, this project prioritized getting the **foundation** right: an isolated, reproducible, well-documented lab environment that can scale as skills grow.

This is intentionally treated as an **infrastructure project first, a hacking project second**. The reasoning: recruiters and certification bodies alike can tell the difference between someone who ran a few commands from a tutorial and someone who understands *why* the network is shaped the way it is. This README reflects the latter approach.

> 🎯 **Guiding principle:** *Document like the next person who reads this has to rebuild it from scratch — because eventually, that person is future-me.*

---

## 02 · Learning Objectives

| # | Objective | Skill Demonstrated |
|---|---|---|
| 1 | Provision a type-2 hypervisor for multi-guest workloads | Virtualization fundamentals |
| 2 | Deploy and configure Kali Linux as an offensive workstation | OS-level security tooling |
| 3 | Design an isolated NAT Network segment | Network architecture & segmentation |
| 4 | Assign and verify deterministic IP addressing | TCP/IP fundamentals |
| 5 | Validate connectivity, routing, and DNS resolution | Diagnostic methodology |
| 6 | Establish snapshot-based recovery points | Operational resilience |
| 7 | Reserve address space for future target machines | Forward-compatible design |
| 8 | Produce replication-grade technical documentation | Professional communication |

---

## 03 · Scope & Ethical Boundaries

| ✅ Permitted | 🚫 Prohibited |
|---|---|
| Testing self-owned virtual machines | Testing any system without explicit authorization |
| Practicing on intentionally vulnerable targets (Metasploitable, DVWA) | Scanning or attacking production/public infrastructure |
| Tool experimentation within the isolated segment | Using lab tooling outside the sandboxed network |
| Academic and portfolio documentation | Sharing exploitation output that identifies real third parties |

> ⚠️ This laboratory operates strictly within an educational and authorized-testing scope. All activity is confined to the isolated `10.0.0.0/24` segment, with no bridging to production networks.

---

## 04 · System Architecture

```
                         ┌────────────────────────────────┐
                         │           Host Machine            │
                         │    (Physical / Bare-Metal Layer)   │
                         └─────────────────┬────────────────┘
                                           │
                               VirtualBox Hypervisor
                                           │
                         ┌─────────────────┴────────────────┐
                         │      Segment: NatNetwork            │
                         │      CIDR: 10.0.0.0/24              │
                         │      Gateway: 10.0.0.1               │
                         │      DHCP: Enabled | IPv6: Disabled   │
                         └─────────────────┬────────────────┘
                                           │
              ┌─────────────────────────────┼─────────────────────────────┐
              │                             │                             │
   ┌──────────▼──────────┐    ┌─────────────▼─────────────┐    ┌──────────▼──────────┐
   │  Kali Linux (Operator) │    Reserved: Target Host α      │    Reserved: Target Host β │
   │  10.0.0.2/24             │    10.0.0.3/24                  │    10.0.0.4/24               │
   └──────────────────────────┘    └────────────────────────┘    └───────────────────────────┘
```

*(Replace with an annotated screenshot — `topology-overview.png` — once captured from the live environment.)*

**Design logic:** A NAT Network (rather than a simple NAT adapter) was chosen specifically so that additional victim machines can be added later and communicate with the Kali host directly — this single decision is what makes the lab *extensible* rather than a dead-end single-VM setup.

---

## 05 · Environment Specification

| 🧩 Component | ⚙️ Configuration |
|---|---|
| 🖥️ Host OS |  Windows 11 Pro |
| 🧠 Host RAM |  16 GB |
| ⚡ Host CPU |  Intel Core i7, 8 cores)* |
| 🧰 Hypervisor | VirtualBox 7.2 |
| 🐉 Guest OS | Kali Linux 2026.2 |
| 🧠 Guest RAM | 11100 MB |
| 💾 Guest Storage |  80 GB dynamic |
| 🌐 Network Type | NAT Network |
| 📡 Segment CIDR | 10.0.0.0/24 |
| 🐧 Kali IP | 10.0.0.2/24 |
| 🚪 Gateway | 10.0.0.1 |
| 🌍 DNS | 8.8.8.8 |
| 🔮 Reserved Target Range | 10.0.0.3 – 10.0.0.99 |

---

## 06 · Build Log

### Step 1 — Archive Extraction Utility
Installed **7-Zip** to extract the Kali Linux `.7z` distribution package.
🔗 [7-Zip Download](https://7-zip.org/download.html)

### Step 2 — Hypervisor Installation
Installed **VirtualBox 7.2** as the type-2 hypervisor hosting all guest machines.
🔗 [VirtualBox Download](https://virtualbox.org/wiki/Downloads)

### Step 3 — NAT Network Creation
```text
Network Name : NatNetwork
IPv4 Prefix   : 10.0.0.0/24
DHCP          : Enabled
IPv6          : Disabled
```
*(Insert: `network-segment-configuration.png`)*

A NAT Network was selected over a standard NAT adapter because it allows multiple VMs on the same segment to communicate with each other — essential groundwork for future attacker-target exercises.

### Step 4 — Kali Linux Import
```text
Adapter 1
Attached to   : NAT Network
Network       : NatNetwork
Adapter Type  : Intel PRO/1000 MT Desktop
RAM Allocated : 2048 MB
```
*(Insert: `guest-import-configuration.png`)*

A shared folder was configured to transfer files between host and guest without external media.

### Step 5 — Static IP Configuration
```text
IP Address   : 10.0.0.2
Subnet Mask  : 255.255.255.0
Gateway      : 10.0.0.1
DNS          : 8.8.8.8
```
*(Insert: `guest-network-configuration.png`)*

### Step 6 — Baseline Snapshot
```text
Snapshot Name : Clean Kali — Post-Network Provisioning
```
Captured immediately after configuration to serve as a rollback point for future exercises.

---

## 07 · Verification Suite

| ✅ Test | 🧾 Command | 🎯 Expected Result | Status |
|---|---|---|---|
| Interface addressing | `ip a` | Correct static IP shown | ✅ Pass |
| Gateway reachability | `ping 10.0.0.1` | Consistent replies | ✅ Pass |
| Internet connectivity | `ping 8.8.8.8` | Consistent replies | ✅ Pass |
| DNS resolution | `nslookup kali.org` | Domain resolves | ✅ Pass |
| Tooling integrity | `nmap --version` | Version returned | ✅ Pass |
| Snapshot fidelity | Restore → `ip a` | Baseline reproduced exactly | ✅ Pass |

```text
Interface : 10.0.0.2/24
Gateway   : 10.0.0.1
DNS       : 8.8.8.8
Result    : ✅ All systems verified
```

---

## 08 · Troubleshooting Journal

### 🔧 Issue 1 — Connectivity Loss After Static IP Assignment
**Symptom:** Internet access failed intermittently after manual IPv4 configuration.

**Fix:**
```bash
sudo nmcli connection modify "Wired connection 1" ipv4.dad-timeout 0
```
Connection restarted, connectivity confirmed.

> 💡 *Lesson:* Always check exact connection names first with `nmcli connection show` — they differ across systems.

### 🔧 Issue 2 — VT-x Virtualization Error
**Symptom:** VM failed to boot; hardware virtualization error.

**Fix:**
1. Reboot → enter BIOS/UEFI
2. Enable **Intel VT-x** (or AMD-V)
3. Save & exit
4. Restart host, relaunch VM

✅ Resolved — VM booted successfully post-BIOS change.

---

## 09 · Key Takeaways

| Concept | What Was Learned |
|---|---|
| **NAT vs. NAT Network** | NAT Network enables inter-VM communication; standard NAT isolates each guest individually |
| **Virtual Networking** | How VirtualBox adapters govern guest connectivity across network types |
| **Static Addressing** | Configuring and verifying IPv4, subnetting, gateways, and DNS via GUI and `nmcli` |
| **Snapshot Discipline** | Always capture a clean baseline *before* risky changes |
| **Documentation Rigor** | Professional-grade write-ups turn a personal exercise into a portfolio asset |

---

## 10 · Roadmap

- [ ] Deploy Metasploitable2/3 as a reserved target (`10.0.0.3`)
- [ ] Add DVWA for structured OWASP Top 10 practice
- [ ] Configure Wireshark for full segment packet capture
- [ ] Document a full reconnaissance → exploitation → reporting cycle
- [ ] Expand lab toward OSCP-style multi-host attack chains

---

## 11 · References

- **7-Zip** — [7-zip.org](https://7-zip.org/download.html)
- **VirtualBox** — [virtualbox.org](https://virtualbox.org/wiki/Downloads)
- **Kali Linux** — [kali.org/get-kali](https://kali.org/get-kali)
- **OWASP Top 10** — [owasp.org](https://owasp.org/www-project-top-ten/)
- **Metasploitable** — [sourceforge.net/projects/metasploitable](https://sourceforge.net/projects/metasploitable/)

---

## 12 · Contact

**[Yash Jethva]**
BSc Information Technology · Aspiring Cybersecurity & Red Team Professional

📎 GitHub — `github.com/yourusername`
📎 LinkedIn — `linkedin.com/in/yourusername`
📎 Portfolio — *(add link)*

<div align="center">

---

*Built as part of a self-directed cybersecurity learning path — one documented lab at a time.*

</div>
