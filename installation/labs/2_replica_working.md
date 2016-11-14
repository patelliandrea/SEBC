# Installation MySQL
An instance of MySQL Server is installed on the first two nodes of the cluster (padrinocluster1 and padrinocluster2)
```
[ec2-user@ip-172-20-0-4 ~]$ wget http://repo.mysql.com/mysql-community-release-el7-5.noarch.rpm
[ec2-user@ip-172-20-0-4 ~]$ sudo rpm -ivh mysql-community-release-el7-5.noarch.rpm
[ec2-user@ip-172-20-0-4 ~]$ sudo yum update
[ec2-user@ip-172-20-0-4 ~]$ sudo yum install mysql-server
[ec2-user@ip-172-20-0-4 ~]$ sudo service mysqld start
```
To install the mysql client, on everynode the following commands were executed:
```
[ec2-user@ip-172-20-0-4 ~]$ wget http://repo.mysql.com/mysql-community-release-el7-5.noarch.rpm
[ec2-user@ip-172-20-0-4 ~]$ sudo rpm -ivh mysql-community-release-el7-5.noarch.rpm
[ec2-user@ip-172-20-0-4 ~]$ sudo yum update
[ec2-user@ip-172-20-0-4 ~]$ sudo yum install mysql
[ec2-user@ip-172-20-0-4 ~]$ sudo rm mysql-community-release-el7-5.noarch.rpm
```

## Configure MySQL Server
All the following commands need to be executed on both replicas, so on hosts padrinocluster1 and padrinocluster2. 

```
[ec2-user@ip-172-20-0-4 ~]$ mysql_secure_installation



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

Remove anonymous users? [Y/n] y
 ... Success!

Disallow root login remotely? [Y/n] n
 ... skipping.

Remove test database and access to it? [Y/n] y
 ... Success!

Reload privilege tables now? [Y/n] y
 ... Success!

```

Copy and paste the following in the file `/etc/my.cnf` (it wasn't there, so I had to create one). Set the `server_id=1` in master (padrinocluster1) and 2 in all slaves (padrinocluster2).
```
[client]
port    	= 3306
socket 	= /var/lib/mysql/mysql.sock
 
# The MySQL server
[mysqld]
port    	= 3306
socket	= /var/lib/mysql/mysql.sock
skip-external-locking
key_buffer  	= 32M
key_buffer_size = 64M
max_allowed_packet = 32M
thread_stack   	= 256K
thread_cache_size  = 64
query_cache_limit  = 16M
query_cache_size   = 64M
query_cache_type   = 1
max_connections	= 700
table_open_cache = 256
sort_buffer_size = 8M
join_buffer_size = 8M
net_buffer_length = 8K
read_buffer_size = 2M
read_rnd_buffer_size = 16M
myisam_sort_buffer_size = 64M
thread_concurrency = 8
binlog_format=row
 
log-bin=mysql-bin 	#Added for MySQL Replication
server-id	= 1     #Note: this should be 2 on the slave node
 
innodb_file_per_table = 1
innodb_flush_log_at_trx_commit  = 1 #Changed from 2 to 1 for Replication
innodb_log_buffer_size      	= 64M
innodb_buffer_pool_size     	= 6G
innodb_thread_concurrency   	= 16
innodb_flush_method         	= O_DIRECT
innodb_log_file_size = 1024M
sync_binlog=1     	#Added for MySQL Replication
 
[mysqldump]
quick
max_allowed_packet = 16M
 
[mysql]
no-auto-rehash
 
[myisamchk]
key_buffer_size = 128M
sort_buffer_size = 128M
read_buffer = 2M
write_buffer = 2M
 
[mysqlhotcopy]
interactive-timeout
 
[mysqld_safe]
log-error=/var/log/mysqld.log
pid-file=/var/run/mysqld/mysqld.pid
```

After updating the configuration, we can stop the service, delete the old log files from both replicas and start the service.
```
[ec2-user@ip-172-20-0-4 ~]$ sudo service mysqld stop
Redirecting to /bin/systemctl stop  mysqld.service
[ec2-user@ip-172-20-0-4 ~]$ sudo rm /var/lib/mysql/ib_logfile*
[ec2-user@ip-172-20-0-4 ~]$ sudo service mysqld start
Redirecting to /bin/systemctl start  mysqld.service
```

On the master node we need to enable replication:
```
[ec2-user@ip-172-20-0-4 ~]$ mysql -u root -p
Enter password:
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 2
Server version: 5.6.34-log MySQL Community Server (GPL)

Copyright (c) 2000, 2016, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> GRANT REPLICATION SLAVE ON *.* TO 'slave_user'@'%' IDENTIFIED BY 'password';
Query OK, 0 rows affected (0.00 sec)

mysql> SET GLOBAL binlog_format = 'ROW';
Query OK, 0 rows affected (0.00 sec)

mysql> FLUSH PRIVILEGES;
Query OK, 0 rows affected (0.00 sec)

mysql> flush tables with read lock;
Query OK, 0 rows affected (0.00 sec)

mysql> show master status;
+------------------+----------+--------------+------------------+-------------------+
| File             | Position | Binlog_Do_DB | Binlog_Ignore_DB | Executed_Gtid_Set |
+------------------+----------+--------------+------------------+-------------------+
| mysql-bin.000001 |      403 |              |                  |                   |
+------------------+----------+--------------+------------------+-------------------+
1 row in set (0.00 sec)

mysql> unlock tables;
Query OK, 0 rows affected (0.00 sec)

mysql> exit;
Bye
```

And then we need to "connect" the slave to the master:
```
[ec2-user@ip-172-20-0-5 ~]$ mysql -u root -p
Enter password:
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 3
Server version: 5.6.34-log MySQL Community Server (GPL)

Copyright (c) 2000, 2016, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> CHANGE MASTER TO MASTER_HOST='ip-172-20-0-4.eu-central-1.compute.internal',MASTER_USER='slave_user', MASTER_PASSWORD='password', MASTER_LOG_FILE='mysql-bin.000001', MASTER_LOG_POS=403;
Query OK, 0 rows affected, 2 warnings (0.02 sec)

mysql> START SLAVE;
Query OK, 0 rows affected (0.01 sec)

mysql> show slave status;
[...]
1 row in set (0.00 sec)

mysql> exit;
Bye
```

We can now create the needed databases from the master:
```
[ec2-user@ip-172-20-0-4 ~]$ mysql -u root -p
Enter password:
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 4
Server version: 5.6.34-log MySQL Community Server (GPL)

Copyright (c) 2000, 2016, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> create database scm DEFAULT CHARACTER SET utf8;
Query OK, 1 row affected (0.00 sec)

mysql> grant all on scm.* TO 'cloudera-scm'@'%' IDENTIFIED BY 'cloudera-scm';
Query OK, 0 rows affected (0.00 sec)

mysql> create database amon DEFAULT CHARACTER SET utf8;
Query OK, 1 row affected (0.00 sec)

mysql> grant all on amon.* TO 'amon'@'%' IDENTIFIED BY 'amon';
Query OK, 0 rows affected (0.01 sec)

mysql> create database rman DEFAULT CHARACTER SET utf8;
Query OK, 1 row affected (0.01 sec)

mysql> grant all on rman.* TO 'rman'@'%' IDENTIFIED BY 'rman';
Query OK, 0 rows affected (0.00 sec)

mysql> create database nav DEFAULT CHARACTER SET utf8;
Query OK, 1 row affected (0.01 sec)

mysql> grant all on nav.* TO 'nav'@'%' IDENTIFIED BY 'nav';
Query OK, 0 rows affected (0.00 sec)

mysql> create database metastore DEFAULT CHARACTER SET utf8;

Query OK, 1 row affected (0.01 sec)

mysql> grant all on metastore.* TO 'hive'@'%' IDENTIFIED BY 'hive';
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

mysql> create database navms DEFAULT CHARACTER SET utf8;
Query OK, 1 row affected (0.00 sec)

mysql> grant all on navms.* to 'navms'@'%' IDENTIFIED BY 'navms';
Query OK, 0 rows affected (0.00 sec)

mysql> exit;
Bye
```

We can now check if the replica is correctly working executing, from the replica node, the following command;
```
[ec2-user@ip-172-20-0-5 ~]$ mysql -u root -p
Enter password:
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 7
Server version: 5.6.34-log MySQL Community Server (GPL)

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
| amon               |
| hue                |
| metastore          |
| mysql              |
| nav                |
| oozie              |
| performance_schema |
| rman               |
| scm                |
| sentry             |
| navms              |
+--------------------+
10 rows in set (0.00 sec)
```

## Installation Oracle JDK 8
On every node of the cluster:
```
[ec2-user@ip-172-20-0-4 ~]$ wget --no-cookies --no-check-certificate --header "Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com%2F; oraclelicense=accept-securebackup-cookie" \
"http://download.oracle.com/otn-pub/java/jdk/8u111-b14/jdk-8u111-linux-x64.rpm"
[ec2-user@ip-172-20-0-4 ~]$ sudo yum localinstall jdk-8u111-linux-x64.rpm -y
```
And then download the mysql connector driver on every node:
```
wget http://dev.mysql.com/get/Downloads/Connector-J/mysql-connector-java-5.1.40.tar.gz
tar -zxvf mysql-connector-java-5.1.40.tar.gz
sudo mkdir -p /usr/share/java
sudo cp mysql-connector-java-5.1.40/mysql-connector-java-5.1.40-bin.jar /usr/share/java/mysql-connector-java.jar
sudo su
echo 'export CLASSPATH=/usr/share/java/mysql-connector-java.jar:$CLASSPATH' > /etc/profile.d/classpath.sh
```