# ethical-hacking-practice-lab
# Network Security Lab: Nmap & Scapy Analysis

## 📄 Overview
This repository documents a practical cybersecurity assignment focused on network reconnaissance and packet manipulation. The objective was to demonstrate proficiency with **Nmap** for scanning and **Scapy** for traffic analysis using a Kali Linux environment.

* **Target System:** Local Virtual Machine (IP: `10.0.2.15`)
* **Tools:** Nmap 7.94, Scapy 2.5.0, Kali Linux

---

## 🔍 Part 1: Nmap Network Scanning

### 1. Host Discovery (Ping Sweep)
**Command:** `nmap -sn 10.0.2.15/24`
**Objective:** To identify live hosts on the local network without performing a full port scan.
**Result:** The scan confirmed the target `10.0.2.15` is "up" with a latency of 0.011s.
![Host Discovery Scan]([Your_Image_Screenshot_2025-12-12_092133.jpg])

### 2. Basic Port Scanning
**Command:** `nmap 10.0.2.15`
**Objective:** To identify open TCP ports on the target.
**Result:** Port **22/tcp (ssh)** was found open. 999 other ports were closed/refused.
![Port Scan]([Your_Image_Screenshot_2025-12-12_091835.jpg])

### 3. Service Version Detection
**Command:** `nmap -v -p22 -sV -T4 10.0.2.15`
**Objective:** To enumerate the specific version of the SSH service running on port 22.
**Result:** * **Service:** SSH
* **Version:** OpenSSH 9.3p2 Debian 1 (Protocol 2.0)
* **Significance:** Knowing the exact version helps identify potential vulnerabilities specific to that software release.
![Service Version Scan]([Your_Image_Screenshot_2025-12-12_092540.jpg])

### 4. OS Fingerprinting
**Command:** `sudo nmap -O 10.0.2.15`
**Objective:** To determine the target's operating system based on TCP/IP stack behavior.
**Result:** The system was identified as running a **Linux 2.6.X kernel** (specifically matching Linux 2.6.32 signatures).
![OS Detection]([Your_Image_Screenshot_2025-12-12_092133.jpg])

---

## 🐍 Part 2: Scapy Packet Manipulation

### 1. Packet Structure Analysis
**Command:** `ls(IP)`
**Objective:** To inspect the default fields of an IP header within Scapy.
**Observation:** Verified standard IP fields such as `src` (Source), `dst` (Destination), `ttl` (Time to Live), and `proto` (Protocol).
![Scapy LS Command]([Your_Image_Screenshot_2025-12-12_095620.jpg])

### 2. Traffic Sniffing and Summary
**Command:** `a.summary()` (After running `sniff()`)
**Objective:** To capture live network traffic and summarize the protocols in use.
**Result:** Successfully captured a mix of traffic:
* **DNS:** Queries to `contile.services.mozilla.com`.
* **TCP/HTTPS:** Encrypted traffic on port 443 involving IP `34.36.137.203`.
* **Protocol Hierarchy:** The summary displays the encapsulation: `Ether / IP / TCP`.
![Scapy Sniff Summary]([Your_Image_Screenshot_2025-12-12_121958.jpg])

---

## 🚀 Key Takeaways
* **Nmap** is highly effective for quick asset inventory. The `-sV` flag provided critical detail about the SSH version that a standard scan missed.
* **Scapy** offers a granular view of network traffic. Unlike Wireshark which is purely visual, Scapy allows for programmatic interaction with packets, as seen in the `ls(IP)` structure analysis.
* **Troubleshooting:** During the Scapy lab, I attempted to run system commands (`ping`) directly inside the Python shell (Screenshot 095620), which threw a syntax error. This reinforced the distinction between the Bash shell (for OS commands) and the Scapy interactive shell (for Python objects).

---
