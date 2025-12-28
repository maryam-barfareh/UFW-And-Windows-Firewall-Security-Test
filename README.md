#  Network Security Mini Project – Firewall Configuration (Windows & Linux)

##  Project Overview
In this project, I implemented basic host-based firewall security on:
- A **Windows host system**
- A **Debian Linux virtual machine**

The goal was to:
- Understand **packet filtering**
- Control **inbound and outbound traffic**
- Secure the system by blocking unnecessary services and protocols
- Verify firewall behavior using real network tests (ping, telnet, services)

---

## Concepts Practiced
- Inbound vs Outbound traffic
- Protocols & Ports
- ICMP behavior
- Host-based firewalls
- Security profiles (Windows)
- Logging and verification

---

##  Part 1: Windows Firewall Configuration

###  Firewall Profiles Used
- **Private Profile** (system is personal)
- Inbound: **Blocked**
- Outbound: **Allowed by default**, then selectively blocked

---

###  Blocked Protocols & Ports (Inbound)

| Protocol | Port | Reason |
|--------|------|--------|
| FTP | 21 | Insecure file transfer |
| SSH | 22 | Prevent remote shell access |
| Telnet | 23 | Unencrypted remote access |
| SMB | 445 | Prevent file sharing attacks |
| RDP | 3389 | Prevent remote desktop access |
| SNMP | 161 | Network information leakage |
| NetBIOS | 137–139 | Legacy Windows networking |

---

###  Blocked Protocols & Ports (Outbound)

| Protocol | Port | Reason |
|--------|------|--------|
| FTP | 21 | Prevent insecure uploads |
| Telnet | 23 | Prevent unencrypted sessions |
| ICMPv4 | N/A | Block ping (echo request) |
| ICMPv6 | N/A | Block IPv6 ping |
| SMB | 445 | Prevent outbound file sharing |

---

###  Tests Performed
- `ping google.com` → **Blocked**
- `telnet <ip> <port>` → **Blocked**
- Verified behavior via firewall logs

---

###  Logging
- Firewall logging enabled
- Logs checked at:
- C:\Windows\System32\LogFiles\Firewall\pfirewall.log
- ---

##  Part 2: Debian Linux Firewall (UFW)

###  Tool Used
- **UFW (Uncomplicated Firewall)**

---

###  Blocked Services (Inbound)

| Protocol | Port |
|--------|------|
| FTP | 21 |
| SSH | 22 |
| Telnet | 23 |
| SMB | 445 |

---

###  Blocked Services (Outbound)

| Protocol | Port |
|--------|------|
| FTP | 21 |
| Telnet | 23 |
| ICMP | N/A |

---

###  Tests Performed
- `ping google.com` → **Destination unreachable**
- `telnet localhost 21` → **Connection blocked**
- Allowed services confirmed working

---

###  UFW Status Check
```bash
sudo ufw status verbose
Systems successfully hardened
Unnecessary services blocked
Traffic filtering verified using real tools
Logs confirmed firewall actions.
