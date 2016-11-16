## CM Monitoring Lab
### What is ubertask optimization?
When ubertask optimization is enabled, sufficient small jobs will run sequentially within a single JVM. How small the jobs have to be is defined using the properties `maxmaps`, `maxreduces`, and `maxbytes`.

### Where in CM is the Kerberos Security Realm value displayed?
The Kerberos Security Realm is displayed in Administration->Settings under "Kerberos Security Realm" (default_realm).

### Which CDH service(s) host a property for enabling Kerberos authentication?
All the core services have a property for enabling Kerberos authentication. The core services are: HDFS, Hive, Hue, Oozie, YARN, ZooKeeper, and Cloudera Management Service.

### How do you upgrade the CM agents?
The CM agents can be updated using the upgrade wizard or the updated version can be manually installed on every node.

To run the upgrade wizard, simply click on "Re-run Upgrade Wizard" from the "All Hosts" page.

### Give the `tsquery` statement used to chart Hue's CPU utilization?
select (cpu_system_rate + cpu_user_rate) where serviceName=hue

### Name all the roles that make up the Hive service
* Hive Metastore Server
* HiveServer2
* Hive Gateway

### What steps must be completed before integrating Cloudera Manager with Kerberos?
	* `openldap-clients` have to be installed on the Cloudera Manager Server host
	* `krb5-workstation` installed on every host
	* `krb5-libs` installed on every host
	* The realm has to support renewable tickets
	* If using AES-256 encryption, install the JCE policy file
	* Get or create a Kerberos Principal for the Cloudera Manager Server
	* Enable Kerberos using the Wizard
After enabling Kerberos, you need to:
	* Create HDFS superuser
	* Get or Create a Kerberos principal for each user account
	* Prepare the cluster for each user (create home dir)
	* Check that Kerberos is actually working (kinit for your user account, submit mapreduce job)