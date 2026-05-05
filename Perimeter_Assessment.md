# TITANCORP: PERIMETER ASSESSMENT REPORT
**Operator:** **Target Subnet:** 172.88.0.0/24

## PHASE 1: ACTIVE ENUMERATION (NMAP)
*(List the live IPs discovered and their running services/versions)*
* **Host 1 (172.88.0.10):** SERVICE http VERSION nginx 1.14.2
* **Host 2 (172.88.0.15):** ALL PORTS ARE CLOSED
* **Host 3 (172.88.0.20):** SERVICE http  VERSION Apache httpd 2.4.66 ((Unix))


## PHASE 2: VULNERABILITY AUDIT (NIKTO)
*(Run Nikto against the TWO web servers discovered above. List one major finding for each.)*
* **Web Server 1 Finding:** Server leaks inodes via ETags, header found with file /, fields: 0x5cadc28a 0x264
* **Web Server 2 Finding:** OSVDB-877: HTTP TRACE method is active, suggesting the host is vulnerable to XST


## PHASE 3: RISK TRIAGE
*(Review your findings. Identify the SINGLE highest-risk vulnerability across the entire DMZ. Justify why it is the top priority using the Likelihood x Impact formula.)*

* **Top Priority Remediation:** NGINX Version
 **Justification:** The current version of NGINX doesn't recieve any more patches which makes it extremely vulnerable to any threats. The vulnerabilties of that version are well known and easily expolitable which can lead to attackers gaining access to sensitive information. 
