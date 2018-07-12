---
description: >-
  Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor
  incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis
  nostrud exercitation ullamco laboris nisi ut a
---

# SSH

## Enumeration

### Nmap

#### SSH Key Acceptance

```text
nmap -p 22 --script ssh-publickey-acceptance --script-args "ssh.usernames={'root', 'user'}, ssh.privatekeys={'./id_rsa1', './id_rsa2'}"  <target>
```

#### SSH Brute

```text
nmap -p 22 --script ssh-brute --script-args userdb=users.lst,passdb=pass.lst \ --script-args ssh-brute.timeout=4s <target>
```

#### SSH Weak Keys

```text
nmap -p 22,443 --script rsa-vuln-roca <target>
```

## **SSH Known Bad Keys**



