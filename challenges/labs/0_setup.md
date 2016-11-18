## Preinstall
Before starting, ansible was installed in order to run commands easier on everynode of the cluster:
```
sudo yum update -y
sudo yum install wget
wget http://dl.fedoraproject.org/pub/epel/7/x86_64/e/epel-release-7-8.noarch.rpm
rpm -ivh epel-release-7-8.noarch.rpm
sudo rpm -ivh epel-release-7-8.noarch.rpm
rm epel-release-7-8.noarch.rpm
sudo yum install ansible
```

Then the `vm.swappiness` was set to 1 and the services `nscd` and `ntpd` were installed and started:
```
ansible all -a 'sudo sysctl vm.swappiness=1'
ansible all -a 'sudo yum install nscd -y'
ansible all -a 'sudo service nscd start'
ansible all -a 'sudo yum install ntp -y'
ansible all -a 'sudo service ntpd start'
```

## Amazon instances info
* Region: eu-central-1
* AMI ID: RHEL-7.1_HVM-20150803-x86_64-1-Hourly2-GP2 (ami-38d2d625)
* OS: Red Hat 7.1

## Volume space available
```
[ec2-user@ip-172-30-2-4 ~]$ ansible all -a 'df -h'
cluster2 | SUCCESS | rc=0 >>
Filesystem      Size  Used Avail Use% Mounted on
/dev/xvda2      100G  1.6G   99G   2% /
devtmpfs        7.3G     0  7.3G   0% /dev
tmpfs           7.2G     0  7.2G   0% /dev/shm
tmpfs           7.2G   33M  7.2G   1% /run
tmpfs           7.2G     0  7.2G   0% /sys/fs/cgroup
tmpfs           1.5G     0  1.5G   0% /run/user/1000

cluster5 | SUCCESS | rc=0 >>
Filesystem      Size  Used Avail Use% Mounted on
/dev/xvda2      100G  1.5G   99G   2% /
devtmpfs        7.3G     0  7.3G   0% /dev
tmpfs           7.2G     0  7.2G   0% /dev/shm
tmpfs           7.2G   33M  7.2G   1% /run
tmpfs           7.2G     0  7.2G   0% /sys/fs/cgroup
tmpfs           1.5G     0  1.5G   0% /run/user/1000

cluster3 | SUCCESS | rc=0 >>
Filesystem      Size  Used Avail Use% Mounted on
/dev/xvda2      100G  1.6G   99G   2% /
devtmpfs        7.3G     0  7.3G   0% /dev
tmpfs           7.2G     0  7.2G   0% /dev/shm
tmpfs           7.2G   33M  7.2G   1% /run
tmpfs           7.2G     0  7.2G   0% /sys/fs/cgroup
tmpfs           1.5G     0  1.5G   0% /run/user/1000

cluster1 | SUCCESS | rc=0 >>
Filesystem      Size  Used Avail Use% Mounted on
/dev/xvda2      100G  1.6G   99G   2% /
devtmpfs        7.3G     0  7.3G   0% /dev
tmpfs           7.2G  172K  7.2G   1% /dev/shm
tmpfs           7.2G   33M  7.2G   1% /run
tmpfs           7.2G     0  7.2G   0% /sys/fs/cgroup
tmpfs           1.5G     0  1.5G   0% /run/user/1000

cluster4 | SUCCESS | rc=0 >>
Filesystem      Size  Used Avail Use% Mounted on
/dev/xvda2      100G  1.6G   99G   2% /
devtmpfs        7.3G     0  7.3G   0% /dev
tmpfs           7.2G     0  7.2G   0% /dev/shm
tmpfs           7.2G   17M  7.2G   1% /run
tmpfs           7.2G     0  7.2G   0% /sys/fs/cgroup
tmpfs           1.5G     0  1.5G   0% /run/user/1000
```

## `yum repolist enabled`
```
[ec2-user@ip-172-30-2-4 ~]$ ansible all -a 'sudo yum repolist enabled'
cluster2 | SUCCESS | rc=0 >>
Loaded plugins: amazon-id, rhui-lb, search-disabled-repos
repo id                                           repo name               status
!rhui-REGION-client-config-server-7/x86_64        Red Hat Update Infrastr      4
!rhui-REGION-rhel-server-releases/7Server/x86_64  Red Hat Enterprise Linu 13,390
!rhui-REGION-rhel-server-rh-common/7Server/x86_64 Red Hat Enterprise Linu    209
repolist: 13,603

cluster3 | SUCCESS | rc=0 >>
Loaded plugins: amazon-id, rhui-lb, search-disabled-repos
repo id                                           repo name               status
!rhui-REGION-client-config-server-7/x86_64        Red Hat Update Infrastr      4
!rhui-REGION-rhel-server-releases/7Server/x86_64  Red Hat Enterprise Linu 13,390
!rhui-REGION-rhel-server-rh-common/7Server/x86_64 Red Hat Enterprise Linu    209
repolist: 13,603

cluster5 | SUCCESS | rc=0 >>
Loaded plugins: amazon-id, rhui-lb, search-disabled-repos
repo id                                           repo name               status
!rhui-REGION-client-config-server-7/x86_64        Red Hat Update Infrastr      4
!rhui-REGION-rhel-server-releases/7Server/x86_64  Red Hat Enterprise Linu 13,390
!rhui-REGION-rhel-server-rh-common/7Server/x86_64 Red Hat Enterprise Linu    209
repolist: 13,603

cluster1 | SUCCESS | rc=0 >>
Loaded plugins: amazon-id, rhui-lb, search-disabled-repos
repo id                                           repo name               status
!epel/x86_64                                      Extra Packages for Ente 10,829
!rhui-REGION-client-config-server-7/x86_64        Red Hat Update Infrastr      4
!rhui-REGION-rhel-server-releases/7Server/x86_64  Red Hat Enterprise Linu 13,390
!rhui-REGION-rhel-server-rh-common/7Server/x86_64 Red Hat Enterprise Linu    209
repolist: 24,432

cluster4 | SUCCESS | rc=0 >>
Loaded plugins: amazon-id, rhui-lb, search-disabled-repos
repo id                                           repo name               status
!rhui-REGION-client-config-server-7/x86_64        Red Hat Update Infrastr      4
!rhui-REGION-rhel-server-releases/7Server/x86_64  Red Hat Enterprise Linu 13,390
!rhui-REGION-rhel-server-rh-common/7Server/x86_64 Red Hat Enterprise Linu    209
repolist: 13,603
```

## Add Users

### Add `bavaria` user
```
[ec2-user@ip-172-30-2-4 ~]$ ansible all -a 'sudo useradd bavaria -u 2700'
cluster2 | SUCCESS | rc=0 >>


cluster5 | SUCCESS | rc=0 >>


cluster3 | SUCCESS | rc=0 >>


cluster1 | SUCCESS | rc=0 >>


cluster4 | SUCCESS | rc=0 >>
```

### Add `saxony` user
```
[ec2-user@ip-172-30-2-4 ~]$ ansible all -a 'sudo useradd saxony -u 2800'
cluster2 | SUCCESS | rc=0 >>


cluster5 | SUCCESS | rc=0 >>


cluster3 | SUCCESS | rc=0 >>


cluster4 | SUCCESS | rc=0 >>


cluster1 | SUCCESS | rc=0 >>
```

### Create `democratic` group
```
[ec2-user@ip-172-30-2-4 ~]$ ansible all -a 'sudo groupadd democratic -g 1001'
cluster2 | SUCCESS | rc=0 >>


cluster5 | SUCCESS | rc=0 >>


cluster3 | SUCCESS | rc=0 >>


cluster1 | SUCCESS | rc=0 >>


cluster4 | SUCCESS | rc=0 >>
```

### Create `social` group
```
[ec2-user@ip-172-30-2-4 ~]$ ansible all -a 'sudo groupadd social -g 1002'
cluster2 | SUCCESS | rc=0 >>


cluster5 | SUCCESS | rc=0 >>


cluster3 | SUCCESS | rc=0 >>


cluster4 | SUCCESS | rc=0 >>


cluster1 | SUCCESS | rc=0 >>
```

### Add `saxony` to `democratic` group
```
[ec2-user@ip-172-30-2-4 ~]$ ansible all -a 'sudo usermod -a -G democratic saxony'
cluster2 | SUCCESS | rc=0 >>


cluster5 | SUCCESS | rc=0 >>


cluster3 | SUCCESS | rc=0 >>


cluster4 | SUCCESS | rc=0 >>


cluster1 | SUCCESS | rc=0 >>
```

### Add `bavaria` to `social` group
```
[ec2-user@ip-172-30-2-4 ~]$ ansible all -a 'sudo usermod -a -G social bavaria'
cluster2 | SUCCESS | rc=0 >>


cluster5 | SUCCESS | rc=0 >>


cluster3 | SUCCESS | rc=0 >>


cluster4 | SUCCESS | rc=0 >>


cluster1 | SUCCESS | rc=0 >>
```

### List `/etc/passwd` for `bavaria` and `saxony`
```
[ec2-user@ip-172-30-2-4 ~]$ ansible all -a 'getent passwd bavaria'
cluster2 | SUCCESS | rc=0 >>
bavaria:x:2700:2700::/home/bavaria:/bin/bash

cluster5 | SUCCESS | rc=0 >>
bavaria:x:2700:2700::/home/bavaria:/bin/bash

cluster3 | SUCCESS | rc=0 >>
bavaria:x:2700:2700::/home/bavaria:/bin/bash

cluster1 | SUCCESS | rc=0 >>
bavaria:x:2700:2700::/home/bavaria:/bin/bash

cluster4 | SUCCESS | rc=0 >>
bavaria:x:2700:2700::/home/bavaria:/bin/bash

[ec2-user@ip-172-30-2-4 ~]$ ansible all -a 'getent passwd saxony'
cluster2 | SUCCESS | rc=0 >>
saxony:x:2800:2800::/home/saxony:/bin/bash

cluster5 | SUCCESS | rc=0 >>
saxony:x:2800:2800::/home/saxony:/bin/bash

cluster3 | SUCCESS | rc=0 >>
saxony:x:2800:2800::/home/saxony:/bin/bash

cluster1 | SUCCESS | rc=0 >>
saxony:x:2800:2800::/home/saxony:/bin/bash

cluster4 | SUCCESS | rc=0 >>
saxony:x:2800:2800::/home/saxony:/bin/bash
```

### List `/etc/group` for `democratic` and `social`
```
[ec2-user@ip-172-30-2-4 ~]$ ansible all -a 'getent group democratic'
cluster2 | SUCCESS | rc=0 >>
democratic:x:1001:saxony

cluster3 | SUCCESS | rc=0 >>
democratic:x:1001:saxony

cluster5 | SUCCESS | rc=0 >>
democratic:x:1001:saxony

cluster1 | SUCCESS | rc=0 >>
democratic:x:1001:saxony

cluster4 | SUCCESS | rc=0 >>
democratic:x:1001:saxony

[ec2-user@ip-172-30-2-4 ~]$ ansible all -a 'getent group social'
cluster2 | SUCCESS | rc=0 >>
social:x:1002:bavaria

cluster5 | SUCCESS | rc=0 >>
social:x:1002:bavaria

cluster3 | SUCCESS | rc=0 >>
social:x:1002:bavaria

cluster4 | SUCCESS | rc=0 >>
social:x:1002:bavaria

cluster1 | SUCCESS | rc=0 >>
social:x:1002:bavaria
```