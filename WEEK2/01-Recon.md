# Reconnaissance Phase

## Objective
Perform structured reconnaissance on the Metasploitable2 lab target to identify exposed services, outdated software versions, and potential attack vectors prior to active exploitation.

---

## Target
192.168.1.8 (Metasploitable2)

---

## Tools Used
- Shodan (OSINT intelligence)
- Maltego (Asset relationship mapping)
- Service Banner Analysis
- Nmap (Service verification)

---

## Methodology

1. Conducted OSINT searches in Shodan for historically vulnerable service versions:
   - apache 2.2.8
   - vsftpd 2.3.4

2. Reviewed service banners for version disclosure.
3. Enumerated open ports and services.
4. Mapped exposed services and relationships in Maltego.
5. Correlated identified versions with known CVEs and public exploit references.

---

## Recon Activity Log
```
+---------------------+--------------+-----------------------------+------------------+
| Timestamp           | Target IP    | Vulnerability / Service     | PTES Phase       |
+---------------------+--------------+-----------------------------+------------------+
| 2026-02-12 10:17:09 | Public OSINT | Apache 2.2.8 Exposure       | Reconnaissance   |
| 2026-02-12 10:17:44 | Public OSINT | vsFTPd 2.3.4 Exposure       | Reconnaissance   |
| 2026-02-12 11:45:27 | 192.168.1.8  | Multiple Open Ports Found   | Reconnaissance   |
+---------------------+--------------+-----------------------------+------------------+

---

## Identified Services (Asset Mapping)

+------+---------+------------------+
| Port | Service | Version          |
+------+---------+------------------+
| 21   | FTP     | vsFTPd 2.3.4     |
| 22   | SSH     | OpenSSH 4.7p1    |
| 23   | Telnet  | Linux Telnet     |
| 25   | SMTP    | Postfix          |
| 53   | DNS     | BIND 9.x         |
| 80   | HTTP    | Apache 2.2.8     |
| 139  | SMB     | Samba 3.x        |
| 3306 | MySQL   | MySQL 5.x        |
+------+---------+------------------+
```
---

## Key Observations

- Multiple outdated software versions identified.
- Service banner disclosure enabled precise version fingerprinting.
- Legacy services (Telnet, vsFTPd 2.3.4, Apache 2.2.8) significantly increase attack surface.
- Simultaneous exposure of FTP, HTTP, SMB, and MySQL provides multiple potential entry vectors.
- Public OSINT confirms these versions are historically associated with critical vulnerabilities.

---

## Recon Summary

The reconnaissance phase successfully identified outdated and vulnerable services running on the target system. OSINT intelligence confirmed Apache 2.2.8 and vsFTPd 2.3.4 exposures, both historically associated with remote exploitation and backdoor vulnerabilities. Asset mapping revealed multiple exposed ports, substantially expanding the attack surface and presenting several viable entry points for the exploitation phase.

---

# Asset Mapping (Maltego)

The target IP (192.168.1.8) was mapped using Maltego to visualize exposed services and port relationships.

![Maltego Asset Map](Images/recon/maltego_asset_mapping.png)

*Figure 1: Asset relationship graph showing exposed ports and services.*

---

# OSINT – Apache 2.2.8 Exposure

Shodan search confirmed publicly exposed instances running Apache 2.2.8, a version associated with known security vulnerabilities.

![Apache Exposure](Images/recon/shodan_apache_2_2_8_exposure.png)

*Figure 2: Shodan results identifying Apache 2.2.8 servers.*

---

# OSINT – vsFTPd 2.3.4 Exposure

Shodan reconnaissance identified exposed vsFTPd 2.3.4 services, a version historically linked to a backdoor vulnerability.

![vsFTPd Exposure](Images/recon/shodan_vsftpd_2_3_4_exposure.png)

*Figure 3: Shodan results identifying vsFTPd 2.3.4 servers.*

---

## Risk Perspective

The combination of legacy services and outdated software versions presents a high likelihood of successful exploitation. Immediate patching, service hardening, and exposure minimization would be required in a real-world environment.
