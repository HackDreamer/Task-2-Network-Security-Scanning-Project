# 🔐 Network Security & Scanning Project

## Overview

This repository documents a complete **Network Security & Scanning lab** performed in a controlled environment.
The project demonstrates how network reconnaissance, vulnerability assessment, and packet analysis are carried out using industry-standard tools.

The tools used include:

* **Nmap** for port and service scanning
* **OpenVAS (Greenbone)** for vulnerability assessment
* **Wireshark** for network traffic analysis

All activities were conducted strictly for **educational purposes** on authorized lab systems.

---

## Objective

The main objectives of this project are:

* To identify live hosts, open ports, and running services
* To analyze service versions and operating system details
* To detect vulnerabilities and classify them based on severity
* To inspect network traffic and understand protocol-level behavior
* To understand the security risks of unencrypted network communication

---

## Lab Environment

* **Attacker Machine:** Kali Linux
* **Target Machine:** Metasploitable2
* **Network Type:** Host-only / Internal network
* **Target IP Address:** `Your_IP`

---

# 🔍 Nmap Scan Details

## Tool Description

Nmap (Network Mapper) is a powerful open-source tool used for network discovery and security auditing. It helps identify open ports, running services, and operating systems on target hosts.

---

## Nmap Command Used

```bash
nmap -sS -sV -O 192.168.56.101 -oN nmap_scan_report.txt
```

---

## Explanation of Scan Options

* `-sS` → Performs a TCP SYN (stealth) scan
* `-sV` → Detects service versions running on open ports
* `-O` → Attempts to identify the target operating system
* `-oN` → Saves the output in a text file

---

## Nmap Scan Observations

The scan revealed multiple open TCP ports on the target system.
Several services such as FTP, SSH, Telnet, HTTP, and MySQL were found running.

Most of the detected services were outdated and known to contain vulnerabilities.
The operating system was identified as a Linux-based system.

These findings indicate a large attack surface and highlight the importance of minimizing exposed services.

---

## Nmap Scan Conclusion

Nmap scanning provided a clear overview of the target’s network exposure.
The information obtained from this scan serves as the foundation for vulnerability assessment and further security testing.

---

# 🛡️ OpenVAS Vulnerability Assessment

## Tool Description

OpenVAS (Greenbone Vulnerability Manager) is a comprehensive vulnerability scanning framework used to detect known security issues in systems and services.

---

## Scan Configuration

* **Scan Type:** Full and Fast
* **Target:** Metasploitable2
* **Scanner:** OpenVAS Default

---

## Vulnerability Assessment Process

1. Target system was added using its IP address
2. A scan task was created using a full scan configuration
3. The scan was executed and allowed to complete
4. Results were reviewed and analyzed

---

## Expected Scan Output

After completion, OpenVAS generated a detailed vulnerability report containing:

* Identified vulnerabilities
* Affected services and ports
* CVE identifiers
* Severity ratings
* Recommended mitigation steps

Since Metasploitable2 is intentionally vulnerable, a high number of security issues were detected.

---

## Vulnerability Severity Categories

* **Critical:**
  Vulnerabilities that can be exploited immediately and may lead to full system compromise.

* **High:**
  Serious vulnerabilities that pose a significant security risk.

* **Medium:**
  Vulnerabilities that require specific conditions to exploit.

* **Low:**
  Minor vulnerabilities or misconfigurations.

* **Log / Informational:**
  Informational findings with no direct impact on security.

---

## OpenVAS Analysis Summary

The vulnerability scan confirmed that the target system is highly insecure.
Multiple critical and high-risk vulnerabilities were identified, emphasizing the importance of regular patching, service hardening, and secure configuration.

---

# 📡 Wireshark Network Traffic Analysis

## Tool Description

Wireshark is a network protocol analyzer used to capture and inspect network packets in real time. It allows detailed analysis of protocol behavior and security weaknesses.

---

## Packet Capture Setup

* Network interface selected: `eth0`
* Live packet capture initiated
* Display filters applied to analyze specific traffic types

---

## HTTP Traffic Analysis

**Display Filter:**

```
http
```

**Observation:**
HTTP packets were captured showing unencrypted web traffic.
Requests and responses were visible in plain text, demonstrating the lack of confidentiality in HTTP communication.

**Security Implication:**
Sensitive information transmitted over HTTP can be intercepted by attackers.

---

## UDP Traffic Analysis

**Display Filter:**

```
udp
```

**Observation:**
UDP packets such as DNS queries and responses were captured.
Packet headers revealed source and destination details.

**Security Implication:**
UDP-based services can be abused for reconnaissance or amplification attacks if not properly secured.

---

## FTP Traffic Analysis

**Display Filter:**

```
ftp
```

**Observation:**
FTP control packets were captured, including authentication commands such as `USER` and `PASS`.
Credentials were visible in plain text.

**Security Implication:**
FTP is insecure and should be replaced with encrypted alternatives such as SFTP or FTPS.

---

## TCP SYN Packet Analysis

**Display Filter:**

```
tcp.flags.syn == 1 && tcp.flags.ack == 0
```

**Observation:**
Multiple TCP SYN packets were observed without corresponding ACK responses.
These packets indicate connection initiation attempts commonly generated during port scanning.

**Security Implication:**
Such traffic patterns can indicate reconnaissance or SYN flood activity and should be monitored by firewalls or intrusion detection systems.

---

# ✅ Final Conclusion

This project successfully demonstrated:

* Network reconnaissance and port scanning using Nmap
* Vulnerability identification and risk assessment using OpenVAS
* Packet-level traffic inspection using Wireshark

The results highlight the importance of secure configurations, encrypted communication, and continuous security monitoring.

---

## ⚠️ Disclaimer

This project was conducted in a controlled lab environment strictly for educational purposes.
No unauthorized systems were scanned or attacked.

---
