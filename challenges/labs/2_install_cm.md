## Install cloudera manager server
The first step is to add the repo on every node:
```
[ec2-user@ip-172-30-2-5 ~]$ ansible all -a 'wget https://archive.cloudera.com/cm5/redhat/5/x86_64/cm/cloudera-manager.repo'
--2016-11-18 03:57:57--  https://archive.cloudera.com/cm5/redhat/5/x86_64/cm/cloudera-manager.repo
Resolving archive.cloudera.com (archive.cloudera.com)... 151.101.12.167
Connecting to archive.cloudera.com (archive.cloudera.com)|151.101.12.167|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 273
Saving to: ‘cloudera-manager.repo’

100%[=======================================================================================================================================================================================================================================>] 273         --.-K/s   in 0s

2016-11-18 03:57:57 (60.5 MB/s) - ‘cloudera-manager.repo’ saved [273/273]

[ec2-user@ip-172-30-2-5 ~]$ ansible all -a 'sudo cp cloudera-manager.repo /etc/yum.repos.d/'
```

We can now install cloudera manager server:
```
[ec2-user@ip-172-30-2-5 ~]$ sudo yum install -y cloudera-manager-server cloudera-manager-daemons
```

Prepare the database
```
[ec2-user@ip-172-30-2-5 ~]$ sudo /usr/share/cmf/schema/scm_prepare_database.sh -h ip-172-30-2-4.eu-central-1.compute.internal mysql scm cloudera-scm
```

## Grant scm only from CM node
```
 grant all on scm.* TO 'cloudera-scm'@'ip-172-30-2-4.eu-central-1.compute.internal' IDENTIFIED BY 'cloudera-scm';
```

And start cloudera-scm-server:
```
[ec2-user@ip-172-30-2-5 ~]$ sudo service cloudera-scm-server start
Starting cloudera-scm-server (via systemctl):              [  OK  ]
```
