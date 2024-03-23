## Install Kerberos
The first step is to install the needed packages on the host where mysql server was installed:
```
[ec2-user@ip-10-1-0-4 ~]$ sudo yum -y install krb5-server krb5-libs krb5-auth-dialog krb5-workstation
```

And the packages needed by the clients on every other node of the cluster:
```
[ec2-user@ip-10-1-0-4 ~]$ ansible all -a 'sudo yum -y install krb5-workstation krb5-libs krb5-auth-dialog'
```

In the server we need then to change the Realm in the file `/var/kerberos/krb5kdc/kdc.conf` to `PATELLIANDREA.REMOTE`
