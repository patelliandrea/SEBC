## The kinit command you use to authenticate your test user
```
[ec2-user@ip-172-20-0-4 ~]$ kinit patelliandrea
Password for patelliandrea@EU-CENTRAL-1.COMPUTE.INTERNAL:
```


## The output from a klist command listing your credentials and ticket lifetime
```
[ec2-user@ip-172-20-0-4 ~]$ klist
Ticket cache: FILE:/tmp/krb5cc_1000
Default principal: patelliandrea@EU-CENTRAL-1.COMPUTE.INTERNAL

Valid starting       Expires              Service principal
11/16/2016 11:05:54  11/17/2016 11:05:54  krbtgt/EU-CENTRAL-1.COMPUTE.INTERNAL@EU-CENTRAL-1.COMPUTE.INTERNAL
        renew until 11/23/2016 11:05:54
```
