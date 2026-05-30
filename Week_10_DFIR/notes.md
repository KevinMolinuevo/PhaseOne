# Week 10 - Digital Forensics and Incident Response
**TKH Innovation Fellowship 2026 | Phase 1 | Cybersecurity**

## What I Learned
This week focused on digital forensics, incident response, chain of custody, timeline analysis, disk artifacts, and evidence hashing. The work connected technical evidence collection to investigative integrity because security findings must be preserved and explained clearly.

## Artifacts
**collection_log.txt**  
This collection log records a suspicious process, process ID, a memory dump MD5 hash, and an artifact SHA-256 hash. It demonstrates chain-of-custody thinking by preserving evidence identifiers.

**attack_timeline.csv**  
This timeline documents failed login activity, domain admin escalation, lateral movement, and data exfiltration. It turns separate events into a chronological incident narrative.

**forensic_findings.md**  
This malware autopsy report identifies `rootkit_beacon.exe`, a lure file named `Resume.exe`, a timestamp, and the behavior `HIDDEN_PROCESS_NO_WINDOW`. It summarizes who, what, when, and how for the forensic finding.

**Incident_Response_Report.md**  
This TLAB report documents SIEM correlation, live triage, chain of custody, disk forensics, a suspicious PID, evidence hash, deleted inode, and extracted payload data. It connects alerting, evidence handling, and forensic recovery into a complete response workflow.

## Challenges & How I Solved Them
The main challenge was keeping evidence specific enough to be useful while still summarizing the incident clearly. I solved it by recording hashes, timestamps, process identifiers, and event descriptions in separate artifacts.

## Reflection
This week helped me understand that incident response depends on disciplined documentation as much as technical skill. I would improve future work by adding more context around how each evidence item was collected.

## References
National Institute of Standards and Technology. (2012). *Computer security incident handling guide* (SP 800-61 Rev. 2). https://doi.org/10.6028/NIST.SP.800-61r2  
National Institute of Standards and Technology. (2006). *Guide to integrating forensic techniques into incident response* (SP 800-86). https://doi.org/10.6028/NIST.SP.800-86
