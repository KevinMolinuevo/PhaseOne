# Week 2 - Networking and Protocol Analysis
**TKH Innovation Fellowship 2026 | Phase 1 | Cybersecurity**

## What I Learned
This week focused on network interfaces, IP addressing, subnetting, service checks, and protocol behavior. The work connected networking fundamentals to security monitoring because accurate network interpretation is required before an analyst can identify abnormal traffic.

## Artifacts
**network_audit.txt**  
This artifact records interface details for loopback and `enp0s1`, including IPv4 and IPv6 addresses, and confirms external connectivity with successful pings to `8.8.8.8`. I produced it by collecting interface and connectivity evidence from the Linux command line.

**subnet_blueprint.txt**  
This artifact documents subnet calculations for `10.50.50.150/24` and a smaller `10.50.50.0/27` network. It identifies network addresses, host ranges, broadcast addresses, wildcard masks, and usable host counts.

**protocol_audit.txt**  
This artifact captures protocol interrogation evidence, including an HTTP `200 OK` response from nginx and successful DNS resolution and ICMP connectivity to `google.com`. It demonstrates how protocol output can confirm service availability and network function.

**tlab_report.txt**  
This TLAB artifact documents Operation Blackout tasks, including subnet remediation and TCP three-way handshake evidence. The SYN, SYN-ACK, and ACK sequence shows that I was able to identify connection establishment at the packet level.

## Challenges & How I Solved Them
The main challenge was keeping subnet math and protocol evidence organized so the results could be interpreted clearly. I solved this by recording the exact network ranges, host boundaries, and packet flags instead of only writing conclusions.

## Reflection
This week strengthened my ability to reason about networks from evidence instead of assumptions. In future work, I would include the exact commands used for every network capture so another analyst could reproduce the audit.

## References
Internet Engineering Task Force. (1981). *Internet Protocol* (RFC 791). https://www.rfc-editor.org/rfc/rfc791  
Wireshark Foundation. (2024). *Wireshark user’s guide*. https://www.wireshark.org/docs/
