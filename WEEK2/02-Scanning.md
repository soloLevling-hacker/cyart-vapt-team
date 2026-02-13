# Vulnerability Scanning Phase

## Objective
To systematically identify exposed services, software versions, and confirmed vulnerabilities on the target system using automated security scanning tools, and to assess their severity and exploitation potential.

---

## Target
192.168.1.8 (Metasploitable2)

---

## Tools Used
- Nmap (Service & Version Enumeration)
- Nikto (Web Server Misconfiguration Analysis)
- OpenVAS (Automated Vulnerability Assessment & CVE Mapping)

---

## Methodology

1. Executed service enumeration using:
   nmap -sV 192.168.1.8

2. Performed web application analysis using:
   nikto -h 192.168.1.8

3. Conducted a full OpenVAS scan to:
   - Identify known CVEs
   - Assign CVSS scores
   - Categorize vulnerabilities by severity

4. Correlated findings across tools to reduce false positives and validate exposure accuracy.

---

# Nmap Scan Results
```
+------+------------+-------------------------------------------+
| Port | Service    | Version                                   |
+------+------------+-------------------------------------------+
| 21   | FTP        | vsftpd 2.3.4                              |
| 22   | SSH        | OpenSSH 4.7p1 Debian                      |
| 23   | Telnet     | Linux telnetd                             |
| 25   | SMTP       | Postfix smtpd                             |
| 53   | DNS        | ISC BIND 9.4.2                            |
| 80   | HTTP       | Apache httpd 2.2.8 (Ubuntu)               |
| 139  | SMB        | Samba smbd 3.X - 4.X                      |
| 445  | SMB        | Samba smbd 3.X - 4.X                      |
| 3306 | MySQL      | MySQL 5.0.51a                             |
| 8180 | HTTP       | Apache Tomcat/Coyote JSP engine 1.1       |
+------+------------+-------------------------------------------+
```
### Observation
The system exposes multiple legacy and outdated services simultaneously, significantly expanding the attack surface and increasing the probability of successful exploitation.

---

# Nikto Web Server Findings
```
+----------------------+----------------------------------------------+
| Finding              | Description                                  |
+----------------------+----------------------------------------------+
| X-Frame-Options      | Header missing (Clickjacking risk)           |
| X-Content-Type       | Header not set (MIME sniffing risk)          |
| HTTP TRACE           | Enabled (Possible Cross-Site Tracing risk)   |
| phpinfo()            | Information disclosure                       |
| Directory Indexing   | /doc/, /test/, /icons/ exposed               |
| Apache 2.2.8         | Outdated and End-of-Life                     |
+----------------------+----------------------------------------------+
```
### Observation
Web server misconfigurations increase reconnaissance value for attackers and facilitate exploitation by disclosing internal system details.

---

# OpenVAS High-Severity Findings
```
+---------+--------------------------------------+--------+-----------+--------------+
| Scan ID | Vulnerability                        | CVSS   | Priority  | Host         |
+---------+--------------------------------------+--------+-----------+--------------+
| 001     | vsFTPd 2.3.4 Backdoor                | 10.0   | Critical  | 192.168.1.8  |
| 002     | Apache 2.2.8 (End-of-Life)           | 9.8    | Critical  | 192.168.1.8  |
| 003     | Apache Tomcat AJP RCE (Ghostcat)     | 9.8    | Critical  | 192.168.1.8  |
| 004     | TWiki Multiple XSS / Command Exec    | 10.0   | Critical  | 192.168.1.8  |
| 005     | rlogin Passwordless Login            | 10.0   | Critical  | 192.168.1.8  |
| 006     | HTTP TRACE Enabled                   | 6.5    | Medium    | 192.168.1.8  |
| 007     | Directory Indexing Enabled           | 5.3    | Medium    | 192.168.1.8  |
+---------+--------------------------------------+--------+-----------+--------------+
```
---

## Severity Summary (OpenVAS)

- Critical: 12  
- High: 10  
- Medium: 40  
- Low: 6  
- Highest CVSS Observed: 10.0 (Critical)

---

# Business Impact

- Remote Code Execution vulnerabilities may result in complete system compromise.
- Backdoored FTP services can provide unauthorized remote shell access.
- Legacy and unsupported software increases the likelihood of publicly available exploit usage.
- Misconfigurations aid attackers in reconnaissance and privilege escalation.
- Simultaneous exposure of multiple high-risk services compounds overall security risk.

---

# Remediation Recommendations

1. Upgrade Apache to a currently supported and patched version.
2. Remove or disable FTP service if not operationally required.
3. Disable HTTP TRACE method.
4. Restrict or completely disable rlogin service.
5. Implement secure HTTP headers:
   - X-Frame-Options
   - X-Content-Type-Options
6. Patch or restrict Apache Tomcat AJP connector exposure.
7. Apply principle of least privilege across exposed services.

---

# Escalation Email (Executive Summary)

Subject: Critical Vulnerabilities Identified on 192.168.1.8

Dear Development Team,

During the recent vulnerability assessment, multiple critical security issues were identified on the system (192.168.1.8). High-risk findings include a vsFTPd backdoor vulnerability, Apache 2.2.8 end-of-life exposure, Apache Tomcat AJP RCE risk, and passwordless rlogin access, with CVSS scores reaching 10.0.

These vulnerabilities significantly increase the likelihood of remote compromise and unauthorized system access. Immediate remediation is strongly recommended, including patching outdated services, disabling unnecessary protocols, and implementing secure configuration standards.

Please advise if a detailed technical breakdown or proof-of-concept validation is required.

Regards,  
Khush Rupapara

---

# Evidence Screenshots

## Nmap Service Version Scan
![Nmap Service Scan](Images/scanning/nmap_service_version_scan.png)

---

## Nikto Web Vulnerability Scan
![Nikto Scan](Images/scanning/nikto_web_vulnerability_scan.png)

---

## OpenVAS Severity Overview
![OpenVAS Severity](Images/scanning/openvas_severity_overview.png)

---

## OpenVAS Results Summary
![OpenVAS Results](Images/scanning/openvas_results_summary.png)

---

## Critical Vulnerabilities Identified
![OpenVAS Critical](Images/scanning/openvas_critical_vulnerabilities.png)

---

## Scan Configuration & Metadata
![OpenVAS Scan Info](Images/scanning/openvas_scan_information.png)
