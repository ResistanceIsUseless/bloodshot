---
description: >-
  Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor
  incididunt ut labore et dolore magna aliqua.
---

# SMB

## **Ports:**

| Port | Protocol | Service |
| --- | --- | --- | --- | --- | --- |
| 135 | TCP | MS-RPC endpoint mapper |
| 137 | UDP | NetBIOS Name Service |
| 138 | UDP | NetBIOS Datagram Service |
| 139 | TCP | NetBIOS Session Service |
| 445 | TCP | SMB Protocol |

## Enumeration

{% hint style="info" %}
 Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum
{% endhint %}

### Enum4linux

> Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum

```text
enum4linux -a -u USER -p PASSWORD -U <HOST(S)>
```

### Crackmapexec

 Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum

```text
cme smb <HOST(S)> -u USER -p PASSWORD -H HASH--sam --sessions --shares -X <COMMAND>
```

### nmblookup

```text
nmblookup -A <HOST(S)>
```

### nbtscan

```text
nbtscan -r <HOST(S)>
```

### ReconScan

```text
reconscan.py <HOST(S)>
```

### ridenum

```text
ridenum.py <HOST(S)> 500 50000 dict.txt
```

## Various Tools

### impacket

```text
python2 /usr/share/doc/python-impacket-doc/examples/samrdump.py <HOST(S)>
```

```text
python2 /usr/share/doc/python-impacket-doc/examples/smbexec.py DOMAIN/User:password@<HOST>
```

### smbclient

```text
smbclient //MOUNT/share -I <HOST(S)> -N 
```

### smbget

### smb4k

**Mount File Shares**

* **NFS on LInux:** `mount 192.168.1.1:/vol/share /mnt/nfs`
* **SMB on Linux:** `mount -t cifs -o username=user,password=pass,domain=DOMAIN //192.168.1.X/share-name /mnt/cifs`
* **SMB on Windows:** `net use Z: \\win-server\share password /user:domain\janedoe /savecred /p:no`

## Exploit

### nmap

#### **SMB OS Discovery**

```text
nmap -p 445 --script smb-os-discovery 192.168.1.0/24
```

#### **SMB Brute Force**

```text
nmap -sV -p 445 --script smb-brute <target>
```

```text
nmap -sU -sS --script smb-brute.nse -p U:137,T:139 <host>
```

**SMB Enumerate Services**

```text
nmap --script smb-enum-services.nse -p445 <host>
```

```text
nmap --script smb-enum-services.nse --script-args smbusername=<username>,smbpass=<password> -p445 <host>
```

#### **Samba &lt;3.6.3 RCE**

```text
nmap --script=samba-vuln-cve-2012-1182  -p 139 <target>
```

**Samba RCE 3.5.0 to 4.4.13**

```text
nmap --script smb-vuln-cve-2017-7494 -p 445 <target>
```

#### **MS RPC DNS ms07-029**

```text
 nmap --script smb-vuln-ms07-029.nse -p445 <host>
```

```text
nmap -sU --script smb-vuln-ms07-029.nse -p U:137,T:139 <host>
```

#### **MS RAS RPC**

```text
nmap --script smb-vuln-ms06-025.nse -p445 <host>
```

```text
nmap -sU --script smb-vuln-ms06-025.nse -p U:137,T:139 <host>
```

#### **ms10-054 SMB**

```text
nmap  -p 445 --script=smb-vuln-ms10-054 --script-args unsafe <target>
```

#### **ms10-061 SMB**

```text
nmap  -p 445 --script=smb-vuln-ms10-061 <target>
```

#### **Eternal Blue ms17-010**

```text
nmap -p445 --script smb-vuln-ms17-010 <target>
```

```text
nmap -p445 --script vuln <target>
```

### metasploit



