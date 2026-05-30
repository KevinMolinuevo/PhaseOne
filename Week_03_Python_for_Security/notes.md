# Week 3 - Python Scripting for Security
**TKH Innovation Fellowship 2026 | Phase 1 | Cybersecurity**

## What I Learned
This week focused on using Python to automate security tasks such as log parsing, process inspection, TCP connection testing, and threat report generation. The work connected scripting to repeatable security operations because automation reduces manual effort and creates consistent evidence.

## Artifacts
**security_audit.py**  
This script reads an authentication audit log, searches for lines containing `Failed password`, writes matching entries to `brute_report.txt`, and counts the number of detected attack signatures. It demonstrates basic file handling and pattern matching for brute-force detection.

**system_interrogation.py**  
This script runs `ps aux` through Python's `subprocess` module and searches for an `unauthorized_cryptominer` process. If the process is found, it writes a JSON alert with event, severity, and process details.

**tcp_connect.py**  
This script uses Python sockets to test whether TCP port 22 is open on several target IP addresses. It demonstrates basic service enumeration and timeout handling.

**incident_response.py**  
This TLAB script runs a grep search against `/var/log/titan_sim/auth_sim.log`, extracts attacker IP addresses, and writes them into `threat_report.json`. It connects Python automation directly to incident response reporting.

**threat_report.json**  
This TLAB artifact stores the extracted brute-force attacker IP addresses in structured JSON format. The file shows how script output can become machine-readable security evidence.

## Challenges & How I Solved Them
The main challenge was parsing command output accurately, especially when extracting IP addresses from log lines. I solved it by splitting output into individual lines and then using list logic to collect only the fields needed for the report.

## Reflection
This week showed me why Python is useful for security work: it turns repeated manual checks into repeatable tools. I would improve future scripts by adding exception handling, input validation, and clearer output messages.

## References
Python Software Foundation. (2024). *The Python standard library*. https://docs.python.org/3/library/  
Python Software Foundation. (2024). *socket — Low-level networking interface*. https://docs.python.org/3/library/socket.html
