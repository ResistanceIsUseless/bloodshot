# Windows

{% hint style="info" %}
### Unquoted Service Paths
{% endhint %}

### Unquoted Service Paths

* [ ] `wmic service get name,displayname,pathname,startmode |findstr /i "Auto" |findstr /i /v "C:\Windows\" |findstr /i /v """`
* [ ] `accesschk64.exe -uwcqv "Authenticated Users" * /accepteula`
* [ ] `windows-privesc-check2.exe --audit -a -o wpc-report`





