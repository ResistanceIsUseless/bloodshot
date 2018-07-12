# HTTP/S

## **HTTP Service Scan and Enumeration**

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

## Exploiting HTTP Services and Web Applications

### LFISuite

### fimap

### SQLMap

{% hint style="info" %}

{% endhint %}

{% page-ref page="../../tools/sqlmap.md" %}

