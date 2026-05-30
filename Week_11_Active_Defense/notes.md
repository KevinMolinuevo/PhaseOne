# Week 11 - Active Defense: Firewalls, IDS and EDR
**TKH Innovation Fellowship 2026 | Phase 1 | Cybersecurity**

## What I Learned
This week focused on active defense using firewall rules, intrusion detection signatures, endpoint telemetry, and layered security controls. The work connected prevention, detection, and response by showing how perimeter, network, and endpoint controls work together.

## Artifacts
**firewall_config.sh**  
This script configures iptables rules for a DMZ host by flushing existing rules, allowing web traffic on ports 80 and 443, allowing database traffic to port 3306, and dropping other outbound traffic to the internal subnet. It demonstrates traffic filtering and egress control.

**custom_ids.rules**  
This Suricata rule file includes custom alert examples for ICMP detection and a malware scanner signature containing `Ghost_Scanner_v1`. It demonstrates how IDS rules can detect suspicious network activity.

**edr_policy.xml**  
This Sysmon policy includes a process creation rule that detects command lines containing `delete shadows`. It demonstrates endpoint detection logic for behavior associated with destructive activity.

**Operation_Fortress_Report.md**  
This TLAB report documents defense in depth across three layers: iptables egress blocking, Suricata detection for `cmd=whoami`, and Sysmon detection for a payload download using curl.

**firewall_task.sh**  
This TLAB script is a firewall task scaffold for blocking outbound traffic to the C2 subnet `198.51.100.0/24`.

**suricata_task.rules**  
This TLAB file is a Suricata task scaffold for detecting HTTP traffic containing `cmd=whoami`.

**sysmon_task.xml**  
This TLAB file is a Sysmon task scaffold for detecting suspicious process command lines.

## Challenges & How I Solved Them
The main challenge was understanding how different controls fit together instead of treating firewall, IDS, and EDR work as separate tasks. I solved it by documenting each layer's objective and the rule or condition used to enforce or detect behavior.

## Reflection
This week helped me see active defense as a layered system where each control supports the others. I would improve future work by replacing remaining scaffold placeholders with final executable rules where needed.

## References
Open Information Security Foundation. (2024). *Suricata user guide*. https://docs.suricata.io  
Microsoft. (2024). *Sysmon*. https://learn.microsoft.com/sysinternals/downloads/sysmon  
Netfilter Project. (2024). *iptables documentation*. https://www.netfilter.org/documentation/
