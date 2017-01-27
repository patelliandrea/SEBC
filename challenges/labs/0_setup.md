## Preinstall
Before starting, ansible was installed in order to run commands easier on everynode of the cluster:
```
sudo yum update -y
sudo yum install wget -y
wget https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
sudo rpm -ivh epel-release-latest-7.noarch.rpm
rm epel-release-latest-7.noarch.rpm
sudo yum install ansible
```

## Amazon instances info
* Region: eu-central-1b
* AMI ID: RHEL-7.2_HVM-20161025-x86_64-1-Hourly2-GP2 (ami-7def1712)
* OS: Red Hat 7.2

## Volume space available
```
[ec2-user@ip-10-1-0-4 ~]$ ansible all -a 'df -h'
sebc5 | SUCCESS | rc=0 >>
Filesystem      Size  Used Avail Use% Mounted on
/dev/xvda2      100G  1.7G   99G   2% /
devtmpfs        7.3G     0  7.3G   0% /dev
tmpfs           7.2G     0  7.2G   0% /dev/shm
tmpfs           7.2G   25M  7.2G   1% /run
tmpfs           7.2G     0  7.2G   0% /sys/fs/cgroup
tmpfs           1.5G     0  1.5G   0% /run/user/1000

sebc3 | SUCCESS | rc=0 >>
Filesystem      Size  Used Avail Use% Mounted on
/dev/xvda2      100G  1.7G   99G   2% /
devtmpfs        7.3G     0  7.3G   0% /dev
tmpfs           7.2G     0  7.2G   0% /dev/shm
tmpfs           7.2G   25M  7.2G   1% /run
tmpfs           7.2G     0  7.2G   0% /sys/fs/cgroup
tmpfs           1.5G     0  1.5G   0% /run/user/1000

sebc1 | SUCCESS | rc=0 >>
Filesystem      Size  Used Avail Use% Mounted on
/dev/xvda2      100G  1.7G   99G   2% /
devtmpfs        7.3G     0  7.3G   0% /dev
tmpfs           7.2G  172K  7.2G   1% /dev/shm
tmpfs           7.2G   25M  7.2G   1% /run
tmpfs           7.2G     0  7.2G   0% /sys/fs/cgroup
tmpfs           1.5G     0  1.5G   0% /run/user/1000

sebc2 | SUCCESS | rc=0 >>
Filesystem      Size  Used Avail Use% Mounted on
/dev/xvda2      100G  1.7G   99G   2% /
devtmpfs        7.3G     0  7.3G   0% /dev
tmpfs           7.2G     0  7.2G   0% /dev/shm
tmpfs           7.2G   25M  7.2G   1% /run
tmpfs           7.2G     0  7.2G   0% /sys/fs/cgroup
tmpfs           1.5G     0  1.5G   0% /run/user/1000

sebc4 | SUCCESS | rc=0 >>
Filesystem      Size  Used Avail Use% Mounted on
/dev/xvda2      100G  1.7G   99G   2% /
devtmpfs        7.3G     0  7.3G   0% /dev
tmpfs           7.2G     0  7.2G   0% /dev/shm
tmpfs           7.2G   25M  7.2G   1% /run
tmpfs           7.2G     0  7.2G   0% /sys/fs/cgroup
tmpfs           1.5G     0  1.5G   0% /run/user/1000
```

## `yum repolist enabled`
```
[ec2-user@ip-10-1-0-4 ~]$ ansible all -a 'sudo yum repolist enabled'
sebc5 | SUCCESS | rc=0 >>
Loaded plugins: amazon-id, rhui-lb, search-disabled-repos
repo id                                          repo name                status
epel/x86_64                                      Extra Packages for Enter 11,075
rhui-REGION-client-config-server-7/x86_64        Red Hat Update Infrastru      4
rhui-REGION-rhel-server-releases/7Server/x86_64  Red Hat Enterprise Linux 13,816
rhui-REGION-rhel-server-rh-common/7Server/x86_64 Red Hat Enterprise Linux    209
repolist: 25,104

sebc3 | SUCCESS | rc=0 >>
Loaded plugins: amazon-id, rhui-lb, search-disabled-repos
repo id                                          repo name                status
epel/x86_64                                      Extra Packages for Enter 11,075
rhui-REGION-client-config-server-7/x86_64        Red Hat Update Infrastru      4
rhui-REGION-rhel-server-releases/7Server/x86_64  Red Hat Enterprise Linux 13,816
rhui-REGION-rhel-server-rh-common/7Server/x86_64 Red Hat Enterprise Linux    209
repolist: 25,104

sebc4 | SUCCESS | rc=0 >>
Loaded plugins: amazon-id, rhui-lb, search-disabled-repos
repo id                                          repo name                status
epel/x86_64                                      Extra Packages for Enter 11,075
rhui-REGION-client-config-server-7/x86_64        Red Hat Update Infrastru      4
rhui-REGION-rhel-server-releases/7Server/x86_64  Red Hat Enterprise Linux 13,816
rhui-REGION-rhel-server-rh-common/7Server/x86_64 Red Hat Enterprise Linux    209
repolist: 25,104

sebc1 | SUCCESS | rc=0 >>
Loaded plugins: amazon-id, rhui-lb, search-disabled-repos
repo id                                          repo name                status
epel/x86_64                                      Extra Packages for Enter 11,075
rhui-REGION-client-config-server-7/x86_64        Red Hat Update Infrastru      4
rhui-REGION-rhel-server-releases/7Server/x86_64  Red Hat Enterprise Linux 13,816
rhui-REGION-rhel-server-rh-common/7Server/x86_64 Red Hat Enterprise Linux    209
repolist: 25,104

sebc2 | SUCCESS | rc=0 >>
Loaded plugins: amazon-id, rhui-lb, search-disabled-repos
repo id                                          repo name                status
epel/x86_64                                      Extra Packages for Enter 11,075
rhui-REGION-client-config-server-7/x86_64        Red Hat Update Infrastru      4
rhui-REGION-rhel-server-releases/7Server/x86_64  Red Hat Enterprise Linux 13,816
rhui-REGION-rhel-server-rh-common/7Server/x86_64 Red Hat Enterprise Linux    209
repolist: 25,104
```

## Add Users

### Add `donald` user
```
[ec2-user@ip-10-1-0-4 ~]$ ansible all -a 'sudo useradd donald -u 2700'
sebc1 | SUCCESS | rc=0 >>


sebc2 | SUCCESS | rc=0 >>


sebc3 | SUCCESS | rc=0 >>


sebc5 | SUCCESS | rc=0 >>


sebc4 | SUCCESS | rc=0 >>
```

### Add `vladimir` user
```
[ec2-user@ip-10-1-0-4 ~]$ ansible all -a 'sudo useradd vladimir -u 2800'
sebc5 | SUCCESS | rc=0 >>


sebc3 | SUCCESS | rc=0 >>


sebc4 | SUCCESS | rc=0 >>


sebc2 | SUCCESS | rc=0 >>


sebc1 | SUCCESS | rc=0 >>
```

### Create `hackers` group
```
[ec2-user@ip-10-1-0-4 ~]$ ansible all -a 'sudo groupadd hackers -g 1001'
sebc3 | SUCCESS | rc=0 >>


sebc5 | SUCCESS | rc=0 >>


sebc1 | SUCCESS | rc=0 >>


sebc2 | SUCCESS | rc=0 >>


sebc4 | SUCCESS | rc=0 >>
```

### Create `crackers` group
```
[ec2-user@ip-10-1-0-4 ~]$ ansible all -a 'sudo groupadd crackers -g 1002'
sebc2 | SUCCESS | rc=0 >>


sebc5 | SUCCESS | rc=0 >>


sebc3 | SUCCESS | rc=0 >>


sebc4 | SUCCESS | rc=0 >>


sebc1 | SUCCESS | rc=0 >>
```

## Add `vladimir` to `hackers` group
```
[ec2-user@ip-10-1-0-4 ~]$ ansible all -a 'sudo usermod -aG hackers vladimir'
sebc2 | SUCCESS | rc=0 >>


sebc1 | SUCCESS | rc=0 >>


sebc3 | SUCCESS | rc=0 >>


sebc5 | SUCCESS | rc=0 >>


sebc4 | SUCCESS | rc=0 >>
```

## Add `donald` to `crackers` group
```
[ec2-user@ip-10-1-0-4 ~]$ ansible all -a 'sudo usermod -aG crackers donald'
sebc2 | SUCCESS | rc=0 >>


sebc3 | SUCCESS | rc=0 >>


sebc1 | SUCCESS | rc=0 >>


sebc4 | SUCCESS | rc=0 >>


sebc5 | SUCCESS | rc=0 >>
```

### List `/etc/passwd` for `donald` and `vladimir`
```
[ec2-user@ip-10-1-0-4 ~]$ ansible all -a 'getent passwd donald'
sebc4 | SUCCESS | rc=0 >>
donald:x:2700:2700::/home/donald:/bin/bash

sebc3 | SUCCESS | rc=0 >>
donald:x:2700:2700::/home/donald:/bin/bash

sebc2 | SUCCESS | rc=0 >>
donald:x:2700:2700::/home/donald:/bin/bash

sebc5 | SUCCESS | rc=0 >>
donald:x:2700:2700::/home/donald:/bin/bash

sebc1 | SUCCESS | rc=0 >>
donald:x:2700:2700::/home/donald:/bin/bash

[ec2-user@ip-10-1-0-4 ~]$ ansible all -a 'getent passwd vladimir'
sebc3 | SUCCESS | rc=0 >>
vladimir:x:2800:2800::/home/vladimir:/bin/bash

sebc2 | SUCCESS | rc=0 >>
vladimir:x:2800:2800::/home/vladimir:/bin/bash

sebc5 | SUCCESS | rc=0 >>
vladimir:x:2800:2800::/home/vladimir:/bin/bash

sebc4 | SUCCESS | rc=0 >>
vladimir:x:2800:2800::/home/vladimir:/bin/bash

sebc1 | SUCCESS | rc=0 >>
vladimir:x:2800:2800::/home/vladimir:/bin/bash
```

### List `/etc/group` for `hackers` and `crackers`
```
[ec2-user@ip-10-1-0-4 ~]$ ansible all -a 'getent group hackers'
sebc3 | SUCCESS | rc=0 >>
hackers:x:1001:vladimir

sebc5 | SUCCESS | rc=0 >>
hackers:x:1001:vladimir

sebc2 | SUCCESS | rc=0 >>
hackers:x:1001:vladimir

sebc4 | SUCCESS | rc=0 >>
hackers:x:1001:vladimir

sebc1 | SUCCESS | rc=0 >>
hackers:x:1001:vladimir

[ec2-user@ip-10-1-0-4 ~]$ ansible all -a 'getent group crackers'
sebc2 | SUCCESS | rc=0 >>
crackers:x:1002:donald

sebc3 | SUCCESS | rc=0 >>
crackers:x:1002:donald

sebc5 | SUCCESS | rc=0 >>
crackers:x:1002:donald

sebc1 | SUCCESS | rc=0 >>
crackers:x:1002:donald

sebc4 | SUCCESS | rc=0 >>
crackers:x:1002:donald
```