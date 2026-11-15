# NETWORKWALKS-B84-WK2-PM2-Footprintingand-recon
- Updated With Nmap*
# Ethical Hacking - Footprinting & Reconnaissance

**Target:** networkwalks.com (192.232.216.135)
**Lab Network:** 192.168.1.0/24
**Date:** 13 November 2026
**Environment:** Kali Linux on VirtualBox + Windows Host
**Methodology:** PTES Phase 1 + OWASP Testing Guide v4.2
**Scope:** Passive Reconnaissance Only - No Exploitation
**Note:** MAC addresses blurred for privacy. Full version submitted to lecturer.

## Part A - Local Network Discovery (Nmap / Zenmap)

**Attacker Machine:**
- Local IP: 192.168.1.225
- Subnet Mask: 255.255.255.0
- Subnet: 192.168.1.0/24
- Gateway: 192.168.1.1

**Command:**
`nmap -sn 192.168.1.0/24`

**Result:**
`Nmap done: 256 IP addresses (9 hosts up) scanned in 15.44 seconds`


**Observation:** Most devices show (Unknown) vendor because modern phones use Randomized MACs for privacy.

## Part B - Target Recon - Key Findings

| Category | Finding |
| --- | --- |
| Hosting | HostGator, USA |
| IP | 192.232.216.135 |
| Name Servers | NS6135.HOSTGATOR.COM, NS6136.HOSTGATOR.COM |
| Web Server | Apache + Nginx Cache |
| CMS | WordPress |
| Plugin | WP Download Manager |
| Protection | ModSecurity WAF (SpiderLabs) |
| DNS Software | BIND 9.16.23-RH |
| Email Security | SPF Configured |
| Overall Risk | LOW-MEDIUM |

## Tools Used - 7 Tools

### 1. Nmap / Zenmap
Ping sweep to find live hosts on local subnet.
Command: `nmap -sn 192.168.1.0/24`
Found: 9 hosts up, Gateway 192.168.1.1, Attacker 192.168.1.225.

### 2. whois
Finds who owns the domain and where it is hosted.
Command: `whois networkwalks.com`
Found: HostGator hosting in USA.

### 3. nslookup
Resolves domain name to IP address.
Command: `nslookup networkwalks.com`
Found: 192.232.216.135 via local router 192.168.1.1

### 4. dnsrecon
Full DNS enumeration - SOA, NS, MX, TXT, SRV records.
Command: `dnsrecon -d networkwalks.com`
Found: NS6135/NS6136, MX mail.networkwalks.com on same IP, SPF record, BIND 9.16.23-RH, No Zone Transfer.

### 5. WhatWeb
Identifies web technologies from headers and HTML.
Command: `whatweb https://networkwalks.com`
Found: Apache, WordPress, WP Download Manager, Nginx cache.

### 6. curl -I
Shows HTTP headers only, to confirm server and CMS.
Command: `curl -I https://networkwalks.com`
Found: Server: Apache, wp-json link (WordPress proof), wpdm_client cookie, reCAPTCHA/hCaptcha in Permissions-Policy.

### 7. WAFW00F
Detects if a Web Application Firewall is present.
Command: `wafw00f https://networkwalks.com`
Found: ModSecurity (SpiderLabs) WAF in only 2 requests. Means future scans may be blocked with 403.

## Full Report
See [REPORT.md](REPORT.md) for full findings and recommendations.
*File 2: `REPORT.md`*
Use your full report, but now *KEEP* the Live Host Discovery section with the blurred table above. Keep Finding 1 to 5 as before.

*File 3: `commands.sh` - Updated, With Nmap*
# Footprinting & Recon - 7 Tools
nmap -sn 192.168.1.0/24
whois networkwalks.com
nslookup networkwalks.com
dnsrecon -d networkwalks.com
whatweb https://networkwalks.com
curl -I https://networkwalks.com
wafw00f https://networkwalks.com
### What Was Blurred

- *Blurred:* Last 3 parts of every MAC - e.g. `74:24:9F:XX:XX:XX`
- *Kept:* Private IPs `192.168.1.x` - safe, every home uses them
- *Removed:* Your IPv6 `2605:59c0...` - never post that publicly
<img width="1366" height="643" alt="20287" src="https://github.com/user-attachments/assets/2d971692-57d1-4506-8bd4-33113db07d2d" />
<img width="1366" height="643" alt="20286" src="https://github.com/user-attachments/assets/58ac520a-51b9-48f0-95c3-09104751fecc" />
<img width="1366" height="643" alt="20285" src="https://github.com/user-attachments/assets/f45fce87-e077-44ce-95ba-80b9f24b7463" />
<img width="1366" height="643" alt="20284" src="https://github.com/user-attachments/assets/4677f359-2567-4a33-a730-ad6d3a5fa9ec" />
<img width="1366" height="643" alt="20283" src="https://github.com/user-attachments/assets/61d5ff81-f238-4a33-98fc-c339a801abcd" />
<img width="1366" height="643" alt="20281" src="https://github.com/user-attachments/assets/cb7aa6b0-ccf9-47d8-bb92-523d51f4f3b4" />
<img width="1366" height="643" alt="20280" src="https://github.com/user-attachments/assets/eb275a94-4c40-4ce6-baa1-223424e7640f" />
<img width="1366" height="643" alt="20282" src="https://github.com/user-attachments/assets/5e901a4c-8e29-4f83-b762-6ae1975642f5" />
