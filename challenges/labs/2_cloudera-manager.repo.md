```
[ec2-user@ip-10-1-0-4 ~]$ ansible all -a 'cat /etc/yum.repos.d/cloudera-manager.repo'
sebc3 | SUCCESS | rc=0 >>
[cloudera-manager]
# Packages for Cloudera Manager, Version 5, on RedHat or CentOS 5 x86_64
name=Cloudera Manager
baseurl=https://archive.cloudera.com/cm5/redhat/5/x86_64/cm/5/
gpgkey =https://archive.cloudera.com/cm5/redhat/5/x86_64/cm/RPM-GPG-KEY-cloudera
gpgcheck = 1

sebc5 | SUCCESS | rc=0 >>
[cloudera-manager]
# Packages for Cloudera Manager, Version 5, on RedHat or CentOS 5 x86_64
name=Cloudera Manager
baseurl=https://archive.cloudera.com/cm5/redhat/5/x86_64/cm/5/
gpgkey =https://archive.cloudera.com/cm5/redhat/5/x86_64/cm/RPM-GPG-KEY-cloudera
gpgcheck = 1

sebc4 | SUCCESS | rc=0 >>
[cloudera-manager]
# Packages for Cloudera Manager, Version 5, on RedHat or CentOS 5 x86_64
name=Cloudera Manager
baseurl=https://archive.cloudera.com/cm5/redhat/5/x86_64/cm/5/
gpgkey =https://archive.cloudera.com/cm5/redhat/5/x86_64/cm/RPM-GPG-KEY-cloudera
gpgcheck = 1

sebc2 | SUCCESS | rc=0 >>
[cloudera-manager]
# Packages for Cloudera Manager, Version 5, on RedHat or CentOS 5 x86_64
name=Cloudera Manager
baseurl=https://archive.cloudera.com/cm5/redhat/5/x86_64/cm/5/
gpgkey =https://archive.cloudera.com/cm5/redhat/5/x86_64/cm/RPM-GPG-KEY-cloudera
gpgcheck = 1

sebc1 | SUCCESS | rc=0 >>
[cloudera-manager]
# Packages for Cloudera Manager, Version 5, on RedHat or CentOS 5 x86_64
name=Cloudera Manager
baseurl=https://archive.cloudera.com/cm5/redhat/5/x86_64/cm/5/
gpgkey =https://archive.cloudera.com/cm5/redhat/5/x86_64/cm/RPM-GPG-KEY-cloudera
gpgcheck = 1
```