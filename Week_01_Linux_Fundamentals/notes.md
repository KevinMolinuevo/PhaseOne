# Week 1 - Linux Fundamentals and Filesystem Navigation
**TKH Innovation Fellowship 2026 | Phase 1 | Cybersecurity**

## What I Learned
This week focused on Linux filesystem navigation, permissions, and command-line log parsing. The work connected basic system administration to security principles such as least privilege, secure file handling, and evidence discovery during an investigation.

## Artifacts
**discovery.txt**  
This artifact documents discovered system paths and secrets, including `/var/log/syslog`, `/opt/alpha/mission.txt`, and `/var/tmp/.blackout/token.txt`. I produced it by navigating the Linux filesystem and recording evidence paths and recovered values.

**harden.sh**  
This script hardens sensitive files by setting `~/Vault/secrets.txt` to permission mode `600`, setting `/etc/shadow` to `640`, and assigning `/etc/shadow` to the `root:shadow` ownership group. Producing it required using `chmod` and `chown` to apply least-privilege access controls.

**threat_ips.txt**  
This artifact lists threat IP addresses extracted from log data using a pipeline built around `grep`, `awk`, `sort`, and `uniq`. It demonstrates how stream editing and shell one-liners can support fast incident triage.

**final_threat_report.txt**  
This TLAB artifact contains final suspicious IP findings from the week. It represents the final reporting step after collecting and filtering threat indicators.

## Challenges & How I Solved Them
The main challenge was making sure the correct files and values were identified without mixing normal system data with security-relevant evidence. I worked through this by recording exact paths, using specific filtering commands, and separating discovery artifacts from hardening and reporting artifacts.

## Reflection
This week helped me understand that Linux fundamentals are not separate from cybersecurity work; they are the base layer of investigation and defense. I would improve future work by adding more command output context so each artifact is easier to verify later.

## References
The Linux Documentation Project. (2024). *The Linux system administrator's guide*. https://tldp.org  
GNU Project. (2024). *Coreutils: GNU core utilities*. https://www.gnu.org/software/coreutils/manual/
