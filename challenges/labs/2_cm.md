# `ls /etc/yum.repos.d`
```
[ec2-user@ip-10-1-0-4 ~]$ ansible all -a 'ls /etc/yum.repos.d'
sebc3 | SUCCESS | rc=0 >>
cloudera-manager.repo
epel.repo
epel-testing.repo
mysql-community.repo
mysql-community-source.repo
redhat.repo
redhat-rhui-client-config.repo
redhat-rhui.repo
rhui-load-balancers.conf

sebc2 | SUCCESS | rc=0 >>
cloudera-manager.repo
epel.repo
epel-testing.repo
mysql-community.repo
mysql-community-source.repo
redhat.repo
redhat-rhui-client-config.repo
redhat-rhui.repo
rhui-load-balancers.conf

sebc5 | SUCCESS | rc=0 >>
cloudera-manager.repo
epel.repo
epel-testing.repo
mysql-community.repo
mysql-community-source.repo
redhat.repo
redhat-rhui-client-config.repo
redhat-rhui.repo
rhui-load-balancers.conf

sebc1 | SUCCESS | rc=0 >>
cloudera-manager.repo
epel.repo
epel-testing.repo
mysql-community.repo
mysql-community-source.repo
redhat.repo
redhat-rhui-client-config.repo
redhat-rhui.repo
rhui-load-balancers.conf

sebc4 | SUCCESS | rc=0 >>
cloudera-manager.repo
epel.repo
epel-testing.repo
mysql-community.repo
mysql-community-source.repo
redhat.repo
redhat-rhui-client-config.repo
redhat-rhui.repo
rhui-load-balancers.conf
```

# `scm_prepare_database.sh`
```
[ec2-user@ip-10-1-0-7 ~]$ sudo /usr/share/cmf/schema/scm_prepare_database.sh -h sebc1 mysql scm cloudera-scm
Enter SCM password:
JAVA_HOME=/usr/java/jdk1.8.0_111
Verifying that we can write to /etc/cloudera-scm-server
Creating SCM configuration file in /etc/cloudera-scm-server
Executing:  /usr/java/jdk1.8.0_111/bin/java -cp /usr/share/java/mysql-connector-java.jar:/usr/share/java/oracle-connector-java.jar:/usr/share/cmf/schema/../lib/* com.cloudera.enterprise.dbutil.DbCommandExecutor /etc/cloudera-scm-server/db.properties com.cloudera.cmf.db.
[                          main] DbCommandExecutor              INFO  Successfully connected to database.
All done, your SCM database is configured correctly!
```