## Asset Mapping (Maltego)

The target IP (192.168.1.8) was mapped using Maltego to visualize exposed services and port relationships.

![Maltego Asset Map](Images/recon/maltego_asset_mapping.png)

*Figure 1: Asset relationship graph showing exposed ports and services.*

---

## OSINT – Apache 2.2.8 Exposure

Shodan search confirmed multiple publicly exposed instances running Apache 2.2.8, a version associated with known vulnerabilities.

![Apache Exposure](Images/recon/shodan_apache_2_2_8_exposure.png)

*Figure 2: Shodan results identifying Apache 2.2.8 servers.*

---

## OSINT – vsFTPd 2.3.4 Exposure

Shodan reconnaissance revealed exposed vsFTPd 2.3.4 services, a version historically associated with backdoor vulnerabilities.

![vsFTPd Exposure](Images/recon/shodan_vsftpd_2_3_4_exposure.png)

*Figure 3: Shodan results identifying vsFTPd 2.3.4 servers.*


