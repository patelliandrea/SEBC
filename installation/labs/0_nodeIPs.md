# Node Ips & names
## /etc/hosts
```
[ec2-user@ip-172-20-0-4 ~]$ ansible padrinocluster -a 'cat /etc/hosts'
padrinocluster4 | SUCCESS | rc=0 >>
127.0.0.1   localhost localhost.localdomain padrinocluster4 ip-172-20-0-7.eu-central-1.compute.internal
172.20.0.4      ip-172-20-0-4.eu-central-1.compute.internal padrinocluster1
172.20.0.5      ip-172-20-0-5.eu-central-1.compute.internal padrinocluster2
172.20.0.6      ip-172-20-0-6.eu-central-1.compute.internal padrinocluster3
172.20.0.7      ip-172-20-0-7.eu-central-1.compute.internal padrinocluster4
172.20.0.8      ip-172-20-0-8.eu-central-1.compute.internal padrinocluster5

padrinocluster5 | SUCCESS | rc=0 >>
127.0.0.1   localhost localhost.localdomain padrinocluster6 ip-172-20-0-8.eu-central-1.compute.internal
172.20.0.4      ip-172-20-0-4.eu-central-1.compute.internal padrinocluster1
172.20.0.5      ip-172-20-0-5.eu-central-1.compute.internal padrinocluster2
172.20.0.6      ip-172-20-0-6.eu-central-1.compute.internal padrinocluster3
172.20.0.7      ip-172-20-0-7.eu-central-1.compute.internal padrinocluster4
172.20.0.8      ip-172-20-0-8.eu-central-1.compute.internal padrinocluster5

padrinocluster1 | SUCCESS | rc=0 >>
127.0.0.1   localhost localhost.localdomain padrinocluster1 ip-172-20-0-4.eu-central-1.compute.internal
172.20.0.4      ip-172-20-0-4.eu-central-1.compute.internal padrinocluster1
172.20.0.5      ip-172-20-0-5.eu-central-1.compute.internal padrinocluster2
172.20.0.6      ip-172-20-0-6.eu-central-1.compute.internal padrinocluster3
172.20.0.7      ip-172-20-0-7.eu-central-1.compute.internal padrinocluster4
172.20.0.8      ip-172-20-0-8.eu-central-1.compute.internal padrinocluster5

padrinocluster2 | SUCCESS | rc=0 >>
127.0.0.1   localhost localhost.localdomain padrinocluster2 ip-172-20-0-5.eu-central-1.compute.internal
172.20.0.4      ip-172-20-0-4.eu-central-1.compute.internal padrinocluster1
172.20.0.5      ip-172-20-0-5.eu-central-1.compute.internal padrinocluster2
172.20.0.6      ip-172-20-0-6.eu-central-1.compute.internal padrinocluster3
172.20.0.7      ip-172-20-0-7.eu-central-1.compute.internal padrinocluster4
172.20.0.8      ip-172-20-0-8.eu-central-1.compute.internal padrinocluster5

padrinocluster3 | SUCCESS | rc=0 >>
127.0.0.1   localhost localhost.localdomain padrinocluster3 ip-172-20-0-6.eu-central-1.compute.internal
172.20.0.4      ip-172-20-0-4.eu-central-1.compute.internal padrinocluster1
172.20.0.5      ip-172-20-0-5.eu-central-1.compute.internal padrinocluster2
172.20.0.6      ip-172-20-0-6.eu-central-1.compute.internal padrinocluster3
172.20.0.7      ip-172-20-0-7.eu-central-1.compute.internal padrinocluster4
172.20.0.8      ip-172-20-0-8.eu-central-1.compute.internal padrinocluster5
```

## /etc/hostname
```
[ec2-user@ip-172-20-0-4 ~]$ ansible padrinocluster -a 'cat /etc/hostname'
padrinocluster4 | SUCCESS | rc=0 >>
ip-172-20-0-7.eu-central-1.compute.internal

padrinocluster2 | SUCCESS | rc=0 >>
ip-172-20-0-5.eu-central-1.compute.internal

padrinocluster3 | SUCCESS | rc=0 >>
ip-172-20-0-6.eu-central-1.compute.internal

padrinocluster1 | SUCCESS | rc=0 >>
ip-172-20-0-4.eu-central-1.compute.internal

padrinocluster5 | SUCCESS | rc=0 >>
ip-172-20-0-8.eu-central-1.compute.internal
```

## IPs mapping

```
| Public IP | Private IP     | Hostname | Alias |
|-----------|----------------|----------|-------|
|  | 172.20.0.4 | ip-172-20-0-4.eu-central-1.compute.internal | padrinocluster1 |
|  | 172.20.0.5 | ip-172-20-0-5.eu-central-1.compute.internal | padrinocluster2 |
|  | 172.20.0.6 | ip-172-20-0-6.eu-central-1.compute.internal | padrinocluster3 |
|  | 172.20.0.7 | ip-172-20-0-7.eu-central-1.compute.internal | padrinocluster4 |
|  | 172.20.0.8 | ip-172-20-0-8.eu-central-1.compute.internal | padrinocluster5 |
```
