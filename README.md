# 🔍 Network Reconnaissance using Nmap | Cybersecurity Task

This repo includes results from a local network port scan using Nmap, with basic analysis, Wireshark insights, and answers to key cybersecurity questions. Completed as part of an internship task.

---

## 🎯 Objective

Scan the local network to discover live hosts and open ports, assess potential security exposure, and understand how basic network reconnaissance works.

---

## 🧰 Tools Used

- **Nmap** – for scanning the network and detecting open ports  
- **Wireshark** – for analyzing packet-level traffic  
- **Command Line Interface** – to execute scanning commands  
- **GitHub** – for documenting and sharing the task

---

## 🛠️ Steps Performed

### 1. Identified Local IP Range

Used `ipconfig` (on Windows) or used `ifconfig` (on Linux) to find my IP address:
IPv4 Address: `192.168.137.128`

From this, the subnet range is: `192.168.137.0/24`

---

### 2. Ran Nmap TCP SYN Scan

Command used:
`nmap -sS 192.168.137.0/24` 

---

### 3. Packet Capture with Wireshark
Opened Wireshark and started capture on active network interface

Ran the same Nmap scan while capturing

Applied filters like: `tcp.flags.syn == 1 && tcp.flags.ack == 0`

Observed handshake attempts and responses

---

### 4. Findings and Observations

| IP Address          | Open Ports | Services     | Risk Level | Notes                                                                                                                                                               |
| ------------------- | ---------- | ------------ | ---------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **192.168.137.1**   | 7070       | realserver   | 🔶 Medium  | Port 7070 is often used by streaming servers (RealServer). If unused, it should be closed to avoid potential misuse.                                                |
| **192.168.137.2**   | 53         | domain (DNS) | 🔴 High    | DNS port open indicates this host may be acting as a DNS server. If misconfigured or exposed externally, it’s vulnerable to DNS poisoning or amplification attacks. |
| **192.168.137.128** | None       | —            | 🟢 Low     | All scanned ports are closed (respond with reset). Host is well-secured.                                                                                            |
| **192.168.137.254** | None       | —            | 🟡 Unknown | All ports filtered (no response). Could be behind a firewall or intentionally silent. Needs further inspection.                                                     |


**🔍 Observations:**

- Two hosts (.128 and .254) have no open ports — one resets connections (likely protected), the other filters silently.
- Port 53 (DNS) is open on .2, which can be a security concern if exposed to external networks.
- Port 7070 is open on .1, typically used for RealMedia/RealServer, which should be disabled if unused.


**🔐 Risk Analysis Notes:**

- Open ports should only be enabled when necessary, especially for services like DNS (port 53).
- Unknown or less common ports like 7070 should be monitored and closed if not in active use.
- Devices with filtered ports might be protected by a firewall — but could also be hiding suspicious services.



