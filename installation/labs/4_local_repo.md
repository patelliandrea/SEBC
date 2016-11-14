## Create a Local Repository
The local repository is installed on the last node of the cluster (padrinocluster5).
To install it, simply start the httpd daemon and enable auto startup:
```
[ec2-user@ip-172-20-0-8 ~]$ sudo service httpd start
[ec2-user@ip-172-20-0-8 ~]$ sudo chkconfig httpd on
```
Once the daemon is started,