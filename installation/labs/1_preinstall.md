## 1. Check `vm.swappiness` on all your nodes
```
[ec2-user@ip-172-20-0-4 ~]$ ansible padrinocluster -a 'sudo sysctl vm.swappiness'
padrinocluster2 | SUCCESS | rc=0 >>
vm.swappiness = 30

padrinocluster4 | SUCCESS | rc=0 >>
vm.swappiness = 30

padrinocluster5 | SUCCESS | rc=0 >>
vm.swappiness = 30

padrinocluster1 | SUCCESS | rc=0 >>
vm.swappiness = 30

padrinocluster3 | SUCCESS | rc=0 >>
vm.swappiness = 30
```
The default swappiness is 30, needs to be changed to one:
```
[ec2-user@ip-172-20-0-4 ~]$ ansible padrinocluster -a 'sudo sysctl vm.swappiness=1'
padrinocluster5 | SUCCESS | rc=0 >>
vm.swappiness = 1

padrinocluster1 | SUCCESS | rc=0 >>
vm.swappiness = 1

padrinocluster4 | SUCCESS | rc=0 >>
vm.swappiness = 1

padrinocluster3 | SUCCESS | rc=0 >>
vm.swappiness = 1

padrinocluster2 | SUCCESS | rc=0 >>
vm.swappiness = 1
```
Check if the swappiness is correctly configured:
```
[ec2-user@ip-172-20-0-4 ~]$ ansible padrinocluster -a 'sudo sysctl vm.swappiness'
padrinocluster4 | SUCCESS | rc=0 >>
vm.swappiness = 1

padrinocluster3 | SUCCESS | rc=0 >>
vm.swappiness = 1

padrinocluster2 | SUCCESS | rc=0 >>
vm.swappiness = 1

padrinocluster1 | SUCCESS | rc=0 >>
vm.swappiness = 1

padrinocluster5 | SUCCESS | rc=0 >>
vm.swappiness = 1
```
## 2. Show the mount attributes of all volumes
Result of the command `mount`:
``` 
[ec2-user@ip-172-20-0-4 ~]$ mount
sysfs on /sys type sysfs (rw,nosuid,nodev,noexec,relatime,seclabel)
proc on /proc type proc (rw,nosuid,nodev,noexec,relatime)
devtmpfs on /dev type devtmpfs (rw,nosuid,seclabel,size=7598144k,nr_inodes=1899536,mode=755)
securityfs on /sys/kernel/security type securityfs (rw,nosuid,nodev,noexec,relatime)
tmpfs on /dev/shm type tmpfs (rw,nosuid,nodev,seclabel)
devpts on /dev/pts type devpts (rw,nosuid,noexec,relatime,seclabel,gid=5,mode=620,ptmxmode=000)
tmpfs on /run type tmpfs (rw,nosuid,nodev,seclabel,mode=755)
tmpfs on /sys/fs/cgroup type tmpfs (ro,nosuid,nodev,noexec,seclabel,mode=755)
cgroup on /sys/fs/cgroup/systemd type cgroup (rw,nosuid,nodev,noexec,relatime,xattr,release_agent=/usr/lib/systemd/systemd-cgroups-agent,name=systemd)
pstore on /sys/fs/pstore type pstore (rw,nosuid,nodev,noexec,relatime)
cgroup on /sys/fs/cgroup/net_cls,net_prio type cgroup (rw,nosuid,nodev,noexec,relatime,net_prio,net_cls)
cgroup on /sys/fs/cgroup/devices type cgroup (rw,nosuid,nodev,noexec,relatime,devices)
cgroup on /sys/fs/cgroup/pids type cgroup (rw,nosuid,nodev,noexec,relatime,pids)
cgroup on /sys/fs/cgroup/hugetlb type cgroup (rw,nosuid,nodev,noexec,relatime,hugetlb)
cgroup on /sys/fs/cgroup/perf_event type cgroup (rw,nosuid,nodev,noexec,relatime,perf_event)
cgroup on /sys/fs/cgroup/blkio type cgroup (rw,nosuid,nodev,noexec,relatime,blkio)
cgroup on /sys/fs/cgroup/cpu,cpuacct type cgroup (rw,nosuid,nodev,noexec,relatime,cpuacct,cpu)
cgroup on /sys/fs/cgroup/memory type cgroup (rw,nosuid,nodev,noexec,relatime,memory)
cgroup on /sys/fs/cgroup/cpuset type cgroup (rw,nosuid,nodev,noexec,relatime,cpuset)
cgroup on /sys/fs/cgroup/freezer type cgroup (rw,nosuid,nodev,noexec,relatime,freezer)
configfs on /sys/kernel/config type configfs (rw,relatime)
/dev/xvda2 on / type xfs (rw,relatime,seclabel,attr2,inode64,noquota)
selinuxfs on /sys/fs/selinux type selinuxfs (rw,relatime)
debugfs on /sys/kernel/debug type debugfs (rw,relatime)
mqueue on /dev/mqueue type mqueue (rw,relatime,seclabel)
systemd-1 on /proc/sys/fs/binfmt_misc type autofs (rw,relatime,fd=30,pgrp=1,timeout=300,minproto=5,maxproto=5,direct)
hugetlbfs on /dev/hugepages type hugetlbfs (rw,relatime,seclabel)
tmpfs on /run/user/1000 type tmpfs (rw,nosuid,nodev,relatime,seclabel,size=1497260k,mode=700,uid=1000,gid=1000)
```
## 3. Show the reserve space of any non-root, ext-based volumes
```
[ec2-user@ip-172-20-0-4 ~]$ df -h
Filesystem      Size  Used Avail Use% Mounted on
/dev/xvda2      100G  1.5G   99G   2% /
devtmpfs        7.3G     0  7.3G   0% /dev
tmpfs           7.2G     0  7.2G   0% /dev/shm
tmpfs           7.2G   17M  7.2G   1% /run
tmpfs           7.2G     0  7.2G   0% /sys/fs/cgroup
tmpfs           1.5G     0  1.5G   0% /run/user/1000
```
```
[ec2-user@ip-172-20-0-4 ~]$ sudo fdisk -l
WARNING: fdisk GPT support is currently new, and therefore in an experimental phase. Use at your own discretion.

Disk /dev/xvda: 107.4 GB, 107374182400 bytes, 209715200 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk label type: gpt


#         Start          End    Size  Type            Name
 1         2048         4095      1M  BIOS boot parti
 2         4096    209715166    100G  Microsoft basic
 ```
## 4. Show that transparent hugepages is disabled
The command `cat /sys/kernel/mm/transparent_hugepage/enabled` is executed on every node of the cluster:
```
[ec2-user@ip-172-20-0-4 ~]$ ansible padrinocluster -a 'cat /sys/kernel/mm/transparent_hugepage/enabled'
padrinocluster4 | SUCCESS | rc=0 >>
[always] madvise never

padrinocluster1 | SUCCESS | rc=0 >>
[always] madvise never

padrinocluster5 | SUCCESS | rc=0 >>
[always] madvise never

padrinocluster3 | SUCCESS | rc=0 >>
[always] madvise never

padrinocluster2 | SUCCESS | rc=0 >>
[always] madvise never
```
## 5. Report the network interface attributes
```
[ec2-user@ip-172-20-0-4 ~]$ ifconfig
eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 9001
        inet 172.20.0.4  netmask 255.255.255.240  broadcast 172.20.0.15
        inet6 fe80::c4:dbff:fed3:d171  prefixlen 64  scopeid 0x20<link>
        ether 02:c4:db:d3:d1:71  txqueuelen 1000  (Ethernet)
        RX packets 3359  bytes 338165 (330.2 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 2829  bytes 2130323 (2.0 MiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1  (Local Loopback)
        RX packets 759  bytes 490856 (479.3 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 759  bytes 490856 (479.3 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```
## 6. Show forward and reverse host lookups using `getent` and `nslookup`
```
[ec2-user@ip-172-20-0-4 ~]$ getent hosts ip-172-20-0-4
172.20.0.4      ip-172-20-0-4.eu-central-1.compute.internal
[ec2-user@ip-172-20-0-4 ~]$ getent hosts ip-172-20-0-5
172.20.0.5      ip-172-20-0-5.eu-central-1.compute.internal
[ec2-user@ip-172-20-0-4 ~]$ getent hosts ip-172-20-0-6
172.20.0.6      ip-172-20-0-6.eu-central-1.compute.internal
[ec2-user@ip-172-20-0-4 ~]$ getent hosts ip-172-20-0-7
172.20.0.7      ip-172-20-0-7.eu-central-1.compute.internal
[ec2-user@ip-172-20-0-4 ~]$ getent hosts ip-172-20-0-8
172.20.0.8      ip-172-20-0-8.eu-central-1.compute.internal
```

```
[ec2-user@ip-172-20-0-4 ~]$ getent hosts 172.20.0.4
172.20.0.4      padrinocluster1 ip-172-20-0-4.eu-central-1.compute.internal
[ec2-user@ip-172-20-0-4 ~]$ getent hosts 172.20.0.5
172.20.0.5      padrinocluster2 ip-172-20-0-5.eu-central-1.compute.internal
[ec2-user@ip-172-20-0-4 ~]$ getent hosts 172.20.0.6
172.20.0.6      padrinocluster3 ip-172-20-0-6.eu-central-1.compute.internal
[ec2-user@ip-172-20-0-4 ~]$ getent hosts 172.20.0.7
172.20.0.7      padrinocluster4 ip-172-20-0-7.eu-central-1.compute.internal
[ec2-user@ip-172-20-0-4 ~]$ getent hosts 172.20.0.8
172.20.0.8      padrinocluster5 ip-172-20-0-8.eu-central-1.compute.internal
```

```
[ec2-user@ip-172-20-0-4 ~]$ nslookup ip-172-20-0-4
Server:         172.20.0.2
Address:        172.20.0.2#53

Non-authoritative answer:
Name:   ip-172-20-0-4.eu-central-1.compute.internal
Address: 172.20.0.4

[ec2-user@ip-172-20-0-4 ~]$ nslookup ip-172-20-0-5
Server:         172.20.0.2
Address:        172.20.0.2#53

Non-authoritative answer:
Name:   ip-172-20-0-5.eu-central-1.compute.internal
Address: 172.20.0.5

[ec2-user@ip-172-20-0-4 ~]$ nslookup ip-172-20-0-6
Server:         172.20.0.2
Address:        172.20.0.2#53

Non-authoritative answer:
Name:   ip-172-20-0-6.eu-central-1.compute.internal
Address: 172.20.0.6

[ec2-user@ip-172-20-0-4 ~]$ nslookup ip-172-20-0-7
Server:         172.20.0.2
Address:        172.20.0.2#53

Non-authoritative answer:
Name:   ip-172-20-0-7.eu-central-1.compute.internal
Address: 172.20.0.7

[ec2-user@ip-172-20-0-4 ~]$ nslookup ip-172-20-0-8
Server:         172.20.0.2
Address:        172.20.0.2#53

Non-authoritative answer:
Name:   ip-172-20-0-8.eu-central-1.compute.internal
Address: 172.20.0.8
```

```
[ec2-user@ip-172-20-0-4 ~]$ nslookup 172.20.0.4
Server:         172.20.0.2
Address:        172.20.0.2#53

Non-authoritative answer:
4.0.20.172.in-addr.arpa name = ip-172-20-0-4.eu-central-1.compute.internal.

Authoritative answers can be found from:

[ec2-user@ip-172-20-0-4 ~]$ nslookup 172.20.0.5
Server:         172.20.0.2
Address:        172.20.0.2#53

Non-authoritative answer:
5.0.20.172.in-addr.arpa name = ip-172-20-0-5.eu-central-1.compute.internal.

Authoritative answers can be found from:

[ec2-user@ip-172-20-0-4 ~]$ nslookup 172.20.0.6
Server:         172.20.0.2
Address:        172.20.0.2#53

Non-authoritative answer:
6.0.20.172.in-addr.arpa name = ip-172-20-0-6.eu-central-1.compute.internal.

Authoritative answers can be found from:

[ec2-user@ip-172-20-0-4 ~]$ nslookup 172.20.0.7
Server:         172.20.0.2
Address:        172.20.0.2#53

Non-authoritative answer:
7.0.20.172.in-addr.arpa name = ip-172-20-0-7.eu-central-1.compute.internal.

Authoritative answers can be found from:

[ec2-user@ip-172-20-0-4 ~]$ nslookup 172.20.0.8
Server:         172.20.0.2
Address:        172.20.0.2#53

Non-authoritative answer:
8.0.20.172.in-addr.arpa name = ip-172-20-0-8.eu-central-1.compute.internal.

Authoritative answers can be found from:

```
## 7. Verify the <code>nscd</code> service is running
The `nscd` service is not installed, so it has to be installed on every node. To do that, the following command has been executed:
```
[ec2-user@ip-172-20-0-4 ~]$ ansible padrinocluster -a 'sudo yum install -y nscd'
```
And then the service has been started on every node:
```
[ec2-user@ip-172-20-0-4 ~]$ ansible padrinocluster -a 'sudo service nscd restart'
padrinocluster1 | SUCCESS | rc=0 >>
Redirecting to /bin/systemctl restart  nscd.service

padrinocluster4 | SUCCESS | rc=0 >>
Redirecting to /bin/systemctl restart  nscd.service

padrinocluster3 | SUCCESS | rc=0 >>
Redirecting to /bin/systemctl restart  nscd.service

padrinocluster2 | SUCCESS | rc=0 >>
Redirecting to /bin/systemctl restart  nscd.service

padrinocluster5 | SUCCESS | rc=0 >>
Redirecting to /bin/systemctl restart  nscd.service
```
To check that the service is running, simply run the following command:
```
[ec2-user@ip-172-20-0-4 ~]$ sudo service nscd status
Redirecting to /bin/systemctl status  nscd.service
● nscd.service - Name Service Cache Daemon
   Loaded: loaded (/usr/lib/systemd/system/nscd.service; disabled; vendor preset: disabled)
   Active: active (running) since Mon 2016-11-14 09:25:11 EST; 2min 17s ago
  Process: 3618 ExecStop=/usr/sbin/nscd --shutdown (code=exited, status=0/SUCCESS)
  Process: 3620 ExecStart=/usr/sbin/nscd $NSCD_OPTIONS (code=exited, status=0/SUCCESS)
 Main PID: 3621 (nscd)
   CGroup: /system.slice/nscd.service
           └─3621 /usr/sbin/nscd

Nov 14 09:25:11 ip-172-20-0-4.eu-central-1.compute.internal nscd[3621]: 3621 monitoring directory `/etc` (2)
Nov 14 09:25:11 ip-172-20-0-4.eu-central-1.compute.internal nscd[3621]: 3621 monitoring file `/etc/resolv.conf` (5)
Nov 14 09:25:11 ip-172-20-0-4.eu-central-1.compute.internal nscd[3621]: 3621 monitoring directory `/etc` (2)
Nov 14 09:25:11 ip-172-20-0-4.eu-central-1.compute.internal nscd[3621]: 3621 monitoring file `/etc/services` (6)
Nov 14 09:25:11 ip-172-20-0-4.eu-central-1.compute.internal nscd[3621]: 3621 monitoring directory `/etc` (2)
Nov 14 09:25:11 ip-172-20-0-4.eu-central-1.compute.internal nscd[3621]: 3621 disabled inotify-based monitoring for file `/etc/netgroup': No such file or directory
Nov 14 09:25:11 ip-172-20-0-4.eu-central-1.compute.internal nscd[3621]: 3621 stat failed for file `/etc/netgroup'; will try again later: No such file or directory
Nov 14 09:25:11 ip-172-20-0-4.eu-central-1.compute.internal systemd[1]: Started Name Service Cache Daemon.
Nov 14 09:25:11 ip-172-20-0-4.eu-central-1.compute.internal nscd[3621]: 3621 Access Vector Cache (AVC) started
Nov 14 09:25:30 ip-172-20-0-4.eu-central-1.compute.internal nscd[3621]: 3621 checking for monitored file `/etc/netgroup': No such file or directory
```

## 8. Verify the <code>ntpd</code> service is running<br>
As for the previous service, `ntpd` has to be installed on every node. 
To do that, the following command was used:
```
[ec2-user@ip-172-20-0-4 ~]$ ansible padrinocluster -a 'sudo yum install -y ntp'
```
Once the service was installed, we just need to start it and check that it's properly working:
```
[ec2-user@ip-172-20-0-4 ~]$ ansible padrinocluster -a 'sudo service ntpd restart'
padrinocluster4 | SUCCESS | rc=0 >>
Redirecting to /bin/systemctl restart  ntpd.service

padrinocluster3 | SUCCESS | rc=0 >>
Redirecting to /bin/systemctl restart  ntpd.service

padrinocluster1 | SUCCESS | rc=0 >>
Redirecting to /bin/systemctl restart  ntpd.service

padrinocluster2 | SUCCESS | rc=0 >>
Redirecting to /bin/systemctl restart  ntpd.service

padrinocluster5 | SUCCESS | rc=0 >>
Redirecting to /bin/systemctl restart  ntpd.service
```
```
[ec2-user@ip-172-20-0-4 ~]$ sudo service ntpd status
Redirecting to /bin/systemctl status  ntpd.service
● ntpd.service - Network Time Service
   Loaded: loaded (/usr/lib/systemd/system/ntpd.service; disabled; vendor preset: disabled)
   Active: active (running) since Mon 2016-11-14 09:29:21 EST; 2min 25s ago
  Process: 4188 ExecStart=/usr/sbin/ntpd -u ntp:ntp $OPTIONS (code=exited, status=0/SUCCESS)
 Main PID: 4189 (ntpd)
   CGroup: /system.slice/ntpd.service
           └─4189 /usr/sbin/ntpd -u ntp:ntp -g

Nov 14 09:29:21 ip-172-20-0-4.eu-central-1.compute.internal ntpd[4189]: Listen normally on 2 lo 127.0.0.1 UDP 123
Nov 14 09:29:21 ip-172-20-0-4.eu-central-1.compute.internal ntpd[4189]: Listen normally on 3 eth0 172.20.0.4 UDP 123
Nov 14 09:29:21 ip-172-20-0-4.eu-central-1.compute.internal ntpd[4189]: Listen normally on 4 lo ::1 UDP 123
Nov 14 09:29:21 ip-172-20-0-4.eu-central-1.compute.internal ntpd[4189]: Listen normally on 5 eth0 fe80::c4:dbff:fed3:d171 UDP 123
Nov 14 09:29:21 ip-172-20-0-4.eu-central-1.compute.internal ntpd[4189]: Listening on routing socket on fd #22 for interface updates
Nov 14 09:29:21 ip-172-20-0-4.eu-central-1.compute.internal systemd[1]: Started Network Time Service.
Nov 14 09:29:22 ip-172-20-0-4.eu-central-1.compute.internal ntpd[4189]: 0.0.0.0 c016 06 restart
Nov 14 09:29:22 ip-172-20-0-4.eu-central-1.compute.internal ntpd[4189]: 0.0.0.0 c012 02 freq_set kernel 0.000 PPM
Nov 14 09:29:22 ip-172-20-0-4.eu-central-1.compute.internal ntpd[4189]: 0.0.0.0 c011 01 freq_not_set
Nov 14 09:29:22 ip-172-20-0-4.eu-central-1.compute.internal ntpd[4189]: 0.0.0.0 c614 04 freq_mode
```