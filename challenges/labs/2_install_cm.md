## Install cloudera manager server
The first step is to add the repo on every node:
```
[ec2-user@ip-10-1-0-4 ~]$ ansible all -a 'wget https://archive.cloudera.com/cm5/redhat/5/x86_64/cm/cloudera-manager.repo'

[...]

[ec2-user@ip-10-1-0-4 ~]$ ansible all -a 'sudo cp cloudera-manager.repo /etc/yum.repos.d/'
```

We can now install cloudera manger server on node sebc2 (54.93.102.220):
```
[ec2-user@ip-10-1-0-7 ~]$ sudo yum install -y cloudera-manager-server cloudera-manager-daemons
```

And prepare the database:
```
[ec2-user@ip-10-1-0-7 ~]$ sudo /usr/share/cmf/schema/scm_prepare_database.sh -h ip-172-30-2-4.eu-central-1.compute.internal mysql scm cloudera-scm
```

We can now start cloudra-scm-server:
```
[ec2-user@ip-10-1-0-7 ~]$ sudo service cloudera-scm-server start
Starting cloudera-scm-server (via systemctl):              [  OK  ]
```