1. Executive Summary

This project simulates a full Vulnerability Assessment and Penetration Testing (VAPT) cycle against a deliberately vulnerable environment (Metasploitable2 & DVWA). The objective was to identify, validate, and exploit security weaknesses following PTES methodology. Critical vulnerabilities including SQL Injection and Remote Code Execution were successfully identified and exploited. Sensitive database information was extracted, demonstrating real-world impact. Remediation steps were documented and validated.

2. Scope & Target

Target IP: 192.168.1.8
Environment: Metasploitable2
Applications Tested:

Apache Tomcat 5.5 (Port 8180)

DVWA (Damn Vulnerable Web Application)

Testing Methodology: PTES-aligned structured assessment.

3. Reconnaissance Phase

Tools Used:

Nmap

Manual service enumeration

Findings:

Multiple open ports detected (21, 22, 80, 8180, 3306, etc.)

Apache Tomcat service exposed

DVWA web application accessible

Impact:
Attack surface confirmed and services mapped successfully.

4. Vulnerability Scanning Phase

Tools Used:

OpenVAS

Nmap service detection

OpenVAS identified:

Outdated Apache components

Web application vulnerabilities

Exposed services

Detection Log (ASCII Format)
Timestamp            | Target IP      | Vulnerability       | PTES Phase
--------------------|----------------|---------------------|--------------
2026-02-12 16:50:00 | 192.168.1.8    | SQL Injection       | Exploitation
2026-02-12 17:00:00 | 192.168.1.8    | Tomcat RCE Exposure | Exploitation


Risk Level: Critical

5. Exploitation Phase
5.1 Tomcat Remote Code Execution

Tool: Metasploit
Module Used: exploit/multi/http/tomcat_mgr_upload
Payload: java/meterpreter/reverse_tcp

Result:
Meterpreter session successfully opened.

Exploit ID | Description | Target IP     | Status  | Payload
-----------|-------------|---------------|---------|-------------
003        | Tomcat RCE  | 192.168.1.8   | Success | Java Shell


Validation:

whoami confirmed shell access

Session persistence verified

Impact:
Remote command execution achieved on target server.

5.2 SQL Injection – DVWA

Tool: sqlmap

Injection Type:

Boolean-based blind

Error-based

Time-based blind

UNION-based

Result:
Database enumeration successful.

Extracted:

Database: dvwa

Table: users

Usernames and password hashes dumped

Impact:
Sensitive credentials exposed, demonstrating high-risk data breach scenario.

6. Post-Exploitation Findings

System user: tomcat55

Database credentials exposed

Apache & PHP outdated versions detected

Multiple attack paths confirmed

This stage demonstrated real privilege compromise and sensitive data extraction.

7. Remediation Recommendations

Implement prepared statements (parameterized queries)

Enforce input validation and output encoding

Disable Tomcat Manager or restrict via IP allowlist

Upgrade Apache, PHP, and MySQL

Apply least-privilege principle

Close unused ports

Re-run vulnerability scan after patching

8. Conclusion

The full VAPT cycle successfully demonstrated how reconnaissance, scanning, and exploitation can lead to complete system compromise. SQL Injection enabled database extraction, while Tomcat misconfiguration allowed remote code execution. The assessment highlights the importance of secure coding practices, regular patch management, and proactive vulnerability scanning. Proper remediation significantly reduces attack surface and prevents privilege escalation.

9. Non-Technical Briefing (100 Words)

During this security assessment, we identified critical weaknesses that allowed unauthorized access to the system. An attacker could execute commands remotely and extract sensitive database information, including user credentials. These issues were caused by outdated software and insecure input handling. If left unpatched, such vulnerabilities could lead to data breaches or full server compromise. Immediate remediation steps include updating software, restricting administrative interfaces, and implementing secure coding practices. After applying fixes, a re-assessment should be conducted to ensure vulnerabilities are properly resolved. Addressing these issues will significantly strengthen the organization’s security posture.
