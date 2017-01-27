## Hostname:
* Public IP: 54.93.48.207
* Public Address: ec2-54-93-48-207.eu-central-1.compute.amazonaws.com
* Private IP: 10.1.0.4
* Private hostname: sebc1

## Output `mysql --version`
```
[ec2-user@ip-10-1-0-4 ~]$ ansible all -a 'mysql --version'
sebc5 | SUCCESS | rc=0 >>
mysql  Ver 14.14 Distrib 5.5.54, for Linux (x86_64) using readline 5.1

sebc3 | SUCCESS | rc=0 >>
mysql  Ver 14.14 Distrib 5.5.54, for Linux (x86_64) using readline 5.1

sebc1 | SUCCESS | rc=0 >>
mysql  Ver 14.14 Distrib 5.5.54, for Linux (x86_64) using readline 5.1

sebc2 | SUCCESS | rc=0 >>
mysql  Ver 14.14 Distrib 5.5.54, for Linux (x86_64) using readline 5.1

sebc4 | SUCCESS | rc=0 >>
mysql  Ver 14.14 Distrib 5.5.54, for Linux (x86_64) using readline 5.1
```

## List databases
```
[ec2-user@ip-10-1-0-4 ~]$ mysql -u root -p
Enter password:
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 14
Server version: 5.5.54 MySQL Community Server (GPL)

Copyright (c) 2000, 2016, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| hive               |
| hue                |
| mysql              |
| oozie              |
| performance_schema |
| rman               |
| scm                |
| sentry             |
+--------------------+
9 rows in set (0.00 sec)

mysql> exit
Bye
```