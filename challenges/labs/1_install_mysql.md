# Install mysql
Mysql is installed on the first node of the cluster (ip-172-30-2-4.eu-central-1.compute.internal) where cloudera manager server will run.

## Add repositories
The first step is to download the rpm and install the repo.
```
[ec2-user@ip-172-30-2-4 ~]$ wget http://dev.mysql.com/get/mysql57-community-release-el7-9.noarch.rpm

[...]

2016-11-18 03:11:12 (687 MB/s) - ‘mysql57-community-release-el7-9.noarch.rpm’ saved [6140/6140]

[ec2-user@ip-172-30-2-4 ~]$ [ec2-user@ip-172-30-2-4 ~]$ sudo rpm -ivh mysql57-community-release-el7-9.noarch.rpm
Preparing...                          ################################# [100%]
Updating / installing...
   1:mysql57-community-release-el7-9  ################################# [100%]
```

Now we need to enable the repo for mysql 5.6:
```
[ec2-user@ip-172-30-2-4 ~]$ sudo yum-config-manager --disable mysql57-community
[ec2-user@ip-172-30-2-4 ~]$ sudo yum-config-manager --enable mysql56-community
```

We can check if it's correctly configured using the following command:
```
[ec2-user@ip-172-30-2-4 ~]$ sudo yum repolist enabled | grep "mysql.*-community.*"
mysql-connectors-community/x86_64                MySQL Connectors Communi     24
mysql-tools-community/x86_64                     MySQL Tools Community        38
mysql56-community/x86_64                         MySQL 5.6 Community Serv    289
```

The previous commands need the be executed on every node in order to install the right version of the connector.

### Installation mysql
On the first node, we can install mysql-server and start the service:
```
[ec2-user@ip-172-30-2-4 ~]$ sudo yum install -y mysql-server

[ec2-user@ip-172-30-2-4 ~]$ sudo service mysqld start
Redirecting to /bin/systemctl start  mysqld.service

[ec2-user@ip-172-30-2-4 ~]$ sudo service mysqld status
Redirecting to /bin/systemctl status  mysqld.service
● mysqld.service - MySQL Community Server
   Loaded: loaded (/usr/lib/systemd/system/mysqld.service; enabled; vendor preset: disabled)
   Active: active (running) since Fri 2016-11-18 03:27:53 EST; 4s ago
  Process: 25524 ExecStartPost=/usr/bin/mysql-systemd-start post (code=exited, status=0/SUCCESS)
  Process: 25462 ExecStartPre=/usr/bin/mysql-systemd-start pre (code=exited, status=0/SUCCESS)
 Main PID: 25523 (mysqld_safe)
   CGroup: /system.slice/mysqld.service
           ├─25523 /bin/sh /usr/bin/mysqld_safe
           └─25676 /usr/sbin/mysqld --basedir=/usr --datadir=/var/lib/mysql --plugin-dir=/usr/lib64/mysql/plugin --log-error=/var/log/mysqld.log --pid-file=/var/run/mysqld/mysqld.pid --socket=/var/lib/mysql/mysql.sock

Nov 18 03:27:52 ip-172-30-2-4.eu-central-1.compute.internal mysql-systemd-start[25462]: PLEASE REMEMBER TO SET A PASSWORD FOR THE MySQL root USER !
Nov 18 03:27:52 ip-172-30-2-4.eu-central-1.compute.internal mysql-systemd-start[25462]: To do so, start the server, then issue the following commands:
Nov 18 03:27:52 ip-172-30-2-4.eu-central-1.compute.internal mysql-systemd-start[25462]: /usr/bin/mysqladmin -u root password 'new-password'
Nov 18 03:27:52 ip-172-30-2-4.eu-central-1.compute.internal mysql-systemd-start[25462]: /usr/bin/mysqladmin -u root -h ip-172-30-2-4.eu-central-1.compute.internal password 'new-password'
Nov 18 03:27:52 ip-172-30-2-4.eu-central-1.compute.internal mysql-systemd-start[25462]: Alternatively you can run:
Nov 18 03:27:52 ip-172-30-2-4.eu-central-1.compute.internal mysql-systemd-start[25462]: /usr/bin/mysql_secure_installation
Nov 18 03:27:52 ip-172-30-2-4.eu-central-1.compute.internal mysql-systemd-start[25462]: which will also give you the option of removing the test
Nov 18 03:27:52 ip-172-30-2-4.eu-central-1.compute.internal mysqld_safe[25523]: 161118 03:27:52 mysqld_safe Logging to '/var/log/mysqld.log'.
Nov 18 03:27:52 ip-172-30-2-4.eu-central-1.compute.internal mysqld_safe[25523]: 161118 03:27:52 mysqld_safe Starting mysqld daemon with databases from /var/lib/mysql
Nov 18 03:27:53 ip-172-30-2-4.eu-central-1.compute.internal systemd[1]: Started MySQL Community Server.
```

### Installation mysql clients
```
[ec2-user@ip-172-30-2-4 ~]$ ansible all -a 'sudo yum install mysql -y'
```

## Installation mysql connector
We first need to install java on every node:
```
[ec2-user@ip-172-30-2-4 ~]$ ansible all -a 'wget --no-cookies --no-check-certificate --header "Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com%2F; oraclelicense=accept-securebackup-cookie" "http://download.oracle.com/otn-pub/java/jdk/8u111-b14/jdk-8u111-linux-x64.rpm"'

[ec2-user@ip-172-30-2-4 ~]$ ansible all -a 'sudo yum localinstall jdk-8u111-linux-x64.rpm -y'

[ec2-user@ip-172-30-2-4 ~]$ ansible all -a 'java -version'
cluster5 | SUCCESS | rc=0 >>
openjdk version "1.8.0_111"
OpenJDK Runtime Environment (build 1.8.0_111-b15)
OpenJDK 64-Bit Server VM (build 25.111-b15, mixed mode)

cluster2 | SUCCESS | rc=0 >>
openjdk version "1.8.0_111"
OpenJDK Runtime Environment (build 1.8.0_111-b15)
OpenJDK 64-Bit Server VM (build 25.111-b15, mixed mode)

cluster3 | SUCCESS | rc=0 >>
openjdk version "1.8.0_111"
OpenJDK Runtime Environment (build 1.8.0_111-b15)
OpenJDK 64-Bit Server VM (build 25.111-b15, mixed mode)

cluster1 | SUCCESS | rc=0 >>
openjdk version "1.8.0_111"
OpenJDK Runtime Environment (build 1.8.0_111-b15)
OpenJDK 64-Bit Server VM (build 25.111-b15, mixed mode)

cluster4 | SUCCESS | rc=0 >>
openjdk version "1.8.0_111"
OpenJDK Runtime Environment (build 1.8.0_111-b15)
OpenJDK 64-Bit Server VM (build 25.111-b15, mixed mode)
```

Then we can download and copy the sql connector
```
[ec2-user@ip-172-30-2-4 ~]$ ansible all -a 'wget http://dev.mysql.com/get/Downloads/Connector-J/mysql-connector-java-5.1.40.tar.gz'

[ec2-user@ip-172-30-2-4 ~]$ ansible all -a 'tar -zxvf mysql-connector-java-5.1.40.tar.gz'

[ec2-user@ip-172-30-2-4 ~]$ ansible all -a 'sudo cp mysql-connector-java-5.1.40/mysql-connector-java-5.1.40-bin.jar /usr/share/java/'
```
And  on every node we need to add it to the classpath
```
[ec2-user@ip-172-30-2-4 ~]$ echo 'export CLASSPATH=/usr/share/java/mysql-connector-java-5.1.40-bin.jar:$CLASSPATH' > /etc/profile.d/classpath.sh
```

## Setup roop password for mysql
```
[ec2-user@ip-172-30-2-4 ~]$ mysql_secure_installation



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

Set root password? [Y/n] n
 ... skipping.

By default, a MySQL installation has an anonymous user, allowing anyone
to log into MySQL without having to have a user account created for
them.  This is intended only for testing, and to make the installation
go a bit smoother.  You should remove them before moving into a
production environment.

Remove anonymous users? [Y/n] y
 ... Success!

Normally, root should only be allowed to connect from 'localhost'.  This
ensures that someone cannot guess at the root password from the network.

Disallow root login remotely? [Y/n] n
 ... skipping.

By default, MySQL comes with a database named 'test' that anyone can
access.  This is also intended only for testing, and should be removed
before moving into a production environment.

Remove test database and access to it? [Y/n] y
 - Dropping test database...
ERROR 1008 (HY000) at line 1: Can't drop database 'test'; database doesn't exist
 ... Failed!  Not critical, keep moving...
 - Removing privileges on test database...
 ... Success!

Reloading the privilege tables will ensure that all changes made so far
will take effect immediately.

Reload privilege tables now? [Y/n] y
 ... Success!




All done!  If you've completed all of the above steps, your MySQL
installation should now be secure.

Thanks for using MySQL!


Cleaning up...
```

## Create databases
We need to create the databases needed by CDH:
```
[ec2-user@ip-172-30-2-4 ~]$ mysql -u root
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 2
Server version: 5.6.34 MySQL Community Server (GPL)

Copyright (c) 2000, 2016, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> create database scm DEFAULT CHARACTER SET utf8;
Query OK, 1 row affected (0.00 sec)

mysql> grant all on scm.* TO 'cloudera-scm'@'%' IDENTIFIED BY 'cloudera-scm';

Query OK, 0 rows affected (0.00 sec)

mysql>
mysql> create database rman DEFAULT CHARACTER SET utf8;
Query OK, 1 row affected (0.00 sec)

mysql> grant all on rman.* TO 'rman'@'%' IDENTIFIED BY 'rman';
Query OK, 0 rows affected (0.00 sec)

mysql>
mysql> create database hive DEFAULT CHARACTER SET utf8;
Query OK, 1 row affected (0.00 sec)

mysql> grant all on hive.* TO 'hive'@'%' IDENTIFIED BY 'hive';
Query OK, 0 rows affected (0.00 sec)

mysql>
mysql> create database oozie DEFAULT CHARACTER SET utf8;
gQuery OK, 1 row affected (0.00 sec)

mysql> grant all on oozie.* TO 'oozie'@'%' IDENTIFIED BY 'oozie';

Query OK, 0 rows affected (0.00 sec)

mysql>
mysql> create database hue DEFAULT CHARACTER SET utf8;
Query OK, 1 row affected (0.00 sec)

mysql> grant all on hue.* TO 'hue'@'%' IDENTIFIED BY 'hue';
Query OK, 0 rows affected (0.00 sec)

mysql>
mysql> create database sentry DEFAULT CHARACTER SET utf8;
gQuery OK, 1 row affected (0.00 sec)

mysql> grant all on sentry.* TO 'sentry'@'%' IDENTIFIED BY 'sentry';
Query OK, 0 rows affected (0.00 sec)
```