# Install mysql
Mysql is installed on the first listed node of the cluster (54.93.48.207).

## Add repositories
The first step is to download the rpm and install the repo.
```
[ec2-user@ip-10-1-0-4 ~]$ wget http://dev.mysql.com/get/mysql57-community-release-el7-9.noarch.rpm

[...]

2017-01-27 09:08:55 (162 MB/s) - ‘mysql57-community-release-el7-9.noarch.rpm’ saved [9224/9224]

[ec2-user@ip-10-1-0-4 ~]$ sudo rpm -ivh mysql57-community-release-el7-9.noarch.rpm
warning: mysql57-community-release-el7-9.noarch.rpm: Header V3 DSA/SHA1 Signature, key ID 5072e1f5: NOKEY
Preparing...                          ################################# [100%]
Updating / installing...
   1:mysql57-community-release-el7-9  ################################# [100%]
```

Now we need to enable the repo for mysql 5.5 (after disabling the one for 5.7):
```
[ec2-user@ip-10-1-0-4 ~]$ sudo yum-config-manager --enable mysql55-community
[ec2-user@ip-10-1-0-4 ~]$ sudo yum-config-manager --disable mysql57-community
```

We can check if it's correctly configured using the following command:
```
[ec2-user@ip-10-1-0-4 ~]$ sudo yum repolist enabled | grep "mysql.*-community.*"
mysql-connectors-community/x86_64                MySQL Connectors Communi     30
mysql-tools-community/x86_64                     MySQL Tools Community        41
mysql55-community/x86_64                         MySQL 5.5 Community Serv    291
```

The previous commands need the be executed on every node in order to install the right version of the connector.

### Installation mysql
On the first node, we can install mysql-server, check the version and start the service:
```
[ec2-user@ip-10-1-0-4 ~]$ sudo yum install -y mysql-server

[ec2-user@ip-10-1-0-4 ~]$ mysqld --version
mysqld  Ver 5.5.54 for Linux on x86_64 (MySQL Community Server (GPL))

[ec2-user@ip-10-1-0-4 ~]$ sudo service mysqld start
Redirecting to /bin/systemctl start  mysqld.service

[ec2-user@ip-10-1-0-4 ~]$ sudo service mysqld status
Redirecting to /bin/systemctl status  mysqld.service
● mysqld.service - MySQL Community Server
   Loaded: loaded (/usr/lib/systemd/system/mysqld.service; disabled; vendor preset: disabled)
   Active: active (running) since Fri 2017-01-27 09:14:13 EST; 5s ago
  Process: 28504 ExecStartPost=/usr/bin/mysql-systemd-start post (code=exited, status=0/SUCCESS)
  Process: 28447 ExecStartPre=/usr/bin/mysql-systemd-start pre (code=exited, status=0/SUCCESS)
 Main PID: 28503 (mysqld_safe)
   CGroup: /system.slice/mysqld.service
           ├─28503 /bin/sh /usr/bin/mysqld_safe --basedir=/usr
           └─28660 /usr/sbin/mysqld --basedir=/usr --datadir=/var/lib/mysql --plugin-dir=/usr/lib64/mysql/plugin --log-error=/var/log/mysqld.log --pid-file=/var/run/mysqld/mysqld.pid --socket=/var/lib/mysql/mysql.sock

Jan 27 09:14:09 ip-10-1-0-4.eu-central-1.compute.internal systemd[1]: Starting MySQL Community Server...
Jan 27 09:14:11 ip-10-1-0-4.eu-central-1.compute.internal mysql-systemd-start[28447]: 170127  9:14:11 [Note] Ignoring --secure-file-priv value as server is running with --bootstrap.
Jan 27 09:14:11 ip-10-1-0-4.eu-central-1.compute.internal mysql-systemd-start[28447]: 170127  9:14:11 [Note] /usr/sbin/mysqld (mysqld 5.5.54) starting as process 28490 ...
Jan 27 09:14:11 ip-10-1-0-4.eu-central-1.compute.internal mysql-systemd-start[28447]: 170127  9:14:11 [Note] Ignoring --secure-file-priv value as server is running with --bootstrap.
Jan 27 09:14:11 ip-10-1-0-4.eu-central-1.compute.internal mysql-systemd-start[28447]: 170127  9:14:11 [Note] /usr/sbin/mysqld (mysqld 5.5.54) starting as process 28497 ...
Jan 27 09:14:11 ip-10-1-0-4.eu-central-1.compute.internal mysql-systemd-start[28447]: PLEASE REMEMBER TO SET A PASSWORD FOR THE MySQL root USER !
Jan 27 09:14:11 ip-10-1-0-4.eu-central-1.compute.internal mysql-systemd-start[28447]: To do so, start the server, then issue the following commands:
Jan 27 09:14:11 ip-10-1-0-4.eu-central-1.compute.internal mysqld_safe[28503]: 170127 09:14:11 mysqld_safe Logging to '/var/log/mysqld.log'.
Jan 27 09:14:11 ip-10-1-0-4.eu-central-1.compute.internal mysqld_safe[28503]: 170127 09:14:11 mysqld_safe Starting mysqld daemon with databases from /var/lib/mysql
Jan 27 09:14:13 ip-10-1-0-4.eu-central-1.compute.internal systemd[1]: Started MySQL Community Server.
```

### Installation mysql clients
Now we can install the mysql clients on every node and check again that the right version was installed:
```
[ec2-user@ip-10-1-0-4 ~]$ ansible all -a 'sudo yum install mysql -y'

[ec2-user@ip-10-1-0-4 ~]$ ansible all -a 'mysql --version'
sebc5 | SUCCESS | rc=0 >>
mysql  Ver 14.14 Distrib 5.5.54, for Linux (x86_64) using readline 5.1

sebc3 | SUCCESS | rc=0 >>
mysql  Ver 14.14 Distrib 5.5.54, for Linux (x86_64) using readline 5.1

sebc2 | SUCCESS | rc=0 >>
mysql  Ver 14.14 Distrib 5.5.54, for Linux (x86_64) using readline 5.1

sebc1 | SUCCESS | rc=0 >>
mysql  Ver 14.14 Distrib 5.5.54, for Linux (x86_64) using readline 5.1

sebc4 | SUCCESS | rc=0 >>
mysql  Ver 14.14 Distrib 5.5.54, for Linux (x86_64) using readline 5.1
```

## Installation mysql connector
We first need to install java on every node:
```
[ec2-user@ip-10-1-0-4 ~]$ ansible all -a 'wget --no-cookies --no-check-certificate --header "Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com%2F; oraclelicense=accept-securebackup-cookie" "http://download.oracle.com/otn-pub/java/jdk/8u111-b14/jdk-8u111-linux -x64.rpm"'

[ec2-user@ip-10-1-0-4 ~]$ ansible all -a 'sudo yum localinstall jdk-8u111-linux-x64.rpm -y'

[ec2-user@ip-10-1-0-4 ~]$ ansible all -a 'java -version'
sebc4 | SUCCESS | rc=0 >>
java version "1.8.0_111"
Java(TM) SE Runtime Environment (build 1.8.0_111-b14)
Java HotSpot(TM) 64-Bit Server VM (build 25.111-b14, mixed mode)

sebc5 | SUCCESS | rc=0 >>
java version "1.8.0_111"
Java(TM) SE Runtime Environment (build 1.8.0_111-b14)
Java HotSpot(TM) 64-Bit Server VM (build 25.111-b14, mixed mode)

sebc2 | SUCCESS | rc=0 >>
java version "1.8.0_111"
Java(TM) SE Runtime Environment (build 1.8.0_111-b14)
Java HotSpot(TM) 64-Bit Server VM (build 25.111-b14, mixed mode)

sebc3 | SUCCESS | rc=0 >>
java version "1.8.0_111"
Java(TM) SE Runtime Environment (build 1.8.0_111-b14)
Java HotSpot(TM) 64-Bit Server VM (build 25.111-b14, mixed mode)

sebc1 | SUCCESS | rc=0 >>
java version "1.8.0_111"
Java(TM) SE Runtime Environment (build 1.8.0_111-b14)
Java HotSpot(TM) 64-Bit Server VM (build 25.111-b14, mixed mode)
```

Then we can download and copy the sql connector:
```
[ec2-user@ip-10-1-0-4 ~]$ ansible all -a 'wget http://dev.mysql.com/get/Downloads/Connector-J/mysql-connector-java-5.1.40.tar.gz'

[ec2-user@ip-10-1-0-4 ~]$ ansible all -a 'tar -zxvf mysql-connector-java-5.1.40.tar.gz'

[ec2-user@ip-10-1-0-4 ~]$ ansible all -a 'sudo cp mysql-connector-java-5.1.40/mysql-connector-java-5.1.40-bin.jar /usr/share/java/mysql-connector-java.jar'

[ec2-user@ip-10-1-0-4 ~]$ ansible all -a 'ls /usr/share/java/'
sebc3 | SUCCESS | rc=0 >>
mysql-connector-java.jar

sebc5 | SUCCESS | rc=0 >>
mysql-connector-java.jar

sebc2 | SUCCESS | rc=0 >>
mysql-connector-java.jar

sebc1 | SUCCESS | rc=0 >>
mysql-connector-java.jar

sebc4 | SUCCESS | rc=0 >>
mysql-connector-java.jar
```

And now we need to add the connector to the java classpath (on every node):
```
[ec2-user@ip-10-1-0-4 ~]$ ansible all -a "sudo bash -c \"echo 'export CLASSPATH=/usr/share/java/mysql-connector-java-5.1.40-bin.jar:$CLASSPATH' > /etc/profile.d/classpath.sh\""

[ec2-user@ip-10-1-0-4 ~]$ ansible all -a "sudo cat /etc/profile.d/classpath.sh"
sebc3 | SUCCESS | rc=0 >>
export CLASSPATH=/usr/share/java/mysql-connector-java.jar:$CLASSPATH

sebc2 | SUCCESS | rc=0 >>
export CLASSPATH=/usr/share/java/mysql-connector-java.jar:$CLASSPATH

sebc4 | SUCCESS | rc=0 >>
export CLASSPATH=/usr/share/java/mysql-connector-java.jar:$CLASSPATH

sebc5 | SUCCESS | rc=0 >>
export CLASSPATH=/usr/share/java/mysql-connector-java.jar:$CLASSPATH

sebc1 | SUCCESS | rc=0 >>
export CLASSPATH=/usr/share/java/mysql-connector-java.jar:$CLASSPATH
```

## Stup root password for mysql:
```
[ec2-user@ip-10-1-0-4 ~]$ mysql_secure_installation

NOTE: RUNNING ALL PARTS OF THIS SCRIPT IS RECOMMENDED FOR ALL MySQL
      SERVERS IN PRODUCTION USE!  PLEASE READ EACH STEP CAREFULLY!


In order to log into MySQL to secure it, we'll need the current
password for the root user.  If you've just installed MySQL, and
you haven't set the root password yet, the password will be blank,
so you should just press enter here.

Enter current password for root (enter for none):
OK, successfully used password, moving on...

Setting the root password ensures that nobody can log into the MySQL
root user without the proper authorisation.

Set root password? [Y/n] y
New password:
Re-enter new password:
Password updated successfully!
Reloading privilege tables..
 ... Success!


By default, a MySQL installation has an anonymous user, allowing anyone
to log into MySQL without having to have a user account created for
them.  This is intended only for testing, and to make the installation
go a bit smoother.  You should remove them before moving into a
production environment.

Remove anonymous users? [Y/n] y
 ... Success!

Normally, root should only be allowed to connect from 'localhost'.  This
ensures that someone cannot guess at the root password from the network.

Disallow root login remotely? [Y/n] y
 ... Success!

By default, MySQL comes with a database named 'test' that anyone can
access.  This is also intended only for testing, and should be removed
before moving into a production environment.

Remove test database and access to it? [Y/n] y
 - Dropping test database...
 ... Success!
 - Removing privileges on test database...
 ... Success!

Reloading the privilege tables will ensure that all changes made so far
will take effect immediately.

Reload privilege tables now? [Y/n] y
 ... Success!

Cleaning up...



All done!  If you've completed all of the above steps, your MySQL
installation should now be secure.

Thanks for using MySQL!
```

## Create databases
We need to create the databases needed by CDH"
```
[ec2-user@ip-10-1-0-4 ~]$ mysql -u root -p
Enter password:
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 13
Server version: 5.5.54 MySQL Community Server (GPL)

Copyright (c) 2000, 2016, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> create database scm DEFAULT CHARACTER SET utf8;
Query OK, 1 row affected (0.00 sec)

mysql> grant all on scm.* TO 'cloudera-scm'@'%' IDENTIFIED BY 'cloudera-scm';
Query OK, 0 rows affected (0.00 sec)

mysql> create database rman DEFAULT CHARACTER SET utf8;
Query OK, 1 row affected (0.00 sec)

mysql> grant all on rman.* TO 'rman'@'%' IDENTIFIED BY 'rman';
Query OK, 0 rows affected (0.00 sec)

mysql> create database hive DEFAULT CHARACTER SET utf8;
Query OK, 1 row affected (0.00 sec)

mysql> grant all on hive.* TO 'hive'@'%' IDENTIFIED BY 'hive';
Query OK, 0 rows affected (0.00 sec)

mysql> create database hue DEFAULT CHARACTER SET utf8;
Query OK, 1 row affected (0.00 sec)

mysql> grant all on hue.* to 'hue'@'%' IDENTIFIED BY 'hue';
Query OK, 0 rows affected (0.00 sec)

mysql> create database oozie DEFAULT CHARACTER SET utf8;
Query OK, 1 row affected (0.00 sec)

mysql> grant all on oozie.* to 'oozie'@'%' IDENTIFIED BY 'oozie';
Query OK, 0 rows affected (0.00 sec)

mysql> create database sentry DEFAULT CHARACTER SET utf8;
Query OK, 1 row affected (0.00 sec)

mysql> grant all on sentry.* to 'sentry'@'%' IDENTIFIED BY 'sentry';
Query OK, 0 rows affected (0.00 sec)
```