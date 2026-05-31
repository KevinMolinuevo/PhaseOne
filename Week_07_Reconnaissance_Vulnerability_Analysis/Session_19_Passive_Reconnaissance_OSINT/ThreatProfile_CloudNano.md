# TARGET THREAT PROFILE: CloudNano 
**Classification:** Passive Security Audit
**Operator:** ## 1. Subdomain Discovery 
* **Tool Used:** Sublist3r
* **Subdomains Found:** *  
  bssauth.3721.yahoo.com
hk.admin.7-eleven.yahoo.com


## 2. Tech Stack Mapping 
* **Tool Used:** BuiltWith / Wappalyzer
* **Identified Technologies (CMS/CDN/Backend):** * Cloudfare hosting 
  * Vercel

## 3. Major Exposure Points & Dangers 
*(List three major exposure points discovered during your OSINT audit and explain why they are dangerous)*
1. ** Previous Data Breach ** The credentials that were leaked could still be viable or give insight into possible patterns. 
2. ** Old Subdoamins:** Using a tool like Sublist3r can help find a domain that isn't actively monitored or updated and it can be a entry point into the system. 
3. ** Exposed services :** A tool like shodan can find any open ports connected to the internet and a misconfiguration can allow access from outsiders. 
