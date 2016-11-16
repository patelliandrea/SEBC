## Verify user privileges
```
[ec2-user@ip-172-20-0-4 ~]$ kinit patelliandrea
Password for patelliandrea@EU-CENTRAL-1.COMPUTE.INTERNAL:
```
```
[ec2-user@ip-172-20-0-4 ~]$ beeline
beeline> !connect jdbc:hive2://ip-172-20-0-5.eu-central-1.compute.internal:10000/default;principal=hive/ip-172-20-0-5.eu-central-1.compute.internal@EU-CENTRAL-1.COMPUTE.INTERNAL
scan complete in 2ms
Connecting to jdbc:hive2://ip-172-20-0-5.eu-central-1.compute.internal:10000/default;principal=hive/ip-172-20-0-5.eu-central-1.compute.internal@EU-CENTRAL-1.COMPUTE.INTERNAL
Connected to: Apache Hive (version 1.1.0-cdh5.9.0)
Driver: Hive JDBC (version 1.1.0-cdh5.9.0)
Transaction isolation: TRANSACTION_REPEATABLE_READ
0: jdbc:hive2://ip-172-20-0-5.eu-central-1.co> show tables;
INFO  : Compiling command(queryId=hive_20161116115252_312870cb-1692-41ff-96d6-23c8418b70d5): show tables
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:[FieldSchema(name:tab_name, type:string, comment:from deserializer)], properties:null)
INFO  : Completed compiling command(queryId=hive_20161116115252_312870cb-1692-41ff-96d6-23c8418b70d5); Time taken: 0.766 seconds
INFO  : Executing command(queryId=hive_20161116115252_312870cb-1692-41ff-96d6-23c8418b70d5): show tables
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20161116115252_312870cb-1692-41ff-96d6-23c8418b70d5); Time taken: 0.297 seconds
INFO  : OK
+-----------+--+
| tab_name  |
+-----------+--+
+-----------+--+
No rows selected (2.424 seconds)
```

## Create role with full authorization
```
0: jdbc:hive2://ip-172-20-0-5.eu-central-1.co> CREATE ROLE sentry_admin;
INFO  : Compiling command(queryId=hive_20161116115454_719743c2-0fa5-4932-b25c-46ef85a31544): CREATE ROLE sentry_admin
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:null, properties:null)
INFO  : Completed compiling command(queryId=hive_20161116115454_719743c2-0fa5-4932-b25c-46ef85a31544); Time taken: 0.08 seconds
INFO  : Executing command(queryId=hive_20161116115454_719743c2-0fa5-4932-b25c-46ef85a31544): CREATE ROLE sentry_admin
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20161116115454_719743c2-0fa5-4932-b25c-46ef85a31544); Time taken: 0.433 seconds
INFO  : OK
No rows affected (0.573 seconds)
0: jdbc:hive2://ip-172-20-0-5.eu-central-1.co> GRANT ALL ON SERVER server1 TO ROLE sentry_admin;
INFO  : Compiling command(queryId=hive_20161116115454_c4d9df1b-3333-4072-8487-0f535ec81407): GRANT ALL ON SERVER server1 TO ROLE sentry_admin
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:null, properties:null)
INFO  : Completed compiling command(queryId=hive_20161116115454_c4d9df1b-3333-4072-8487-0f535ec81407); Time taken: 0.064 seconds
INFO  : Executing command(queryId=hive_20161116115454_c4d9df1b-3333-4072-8487-0f535ec81407): GRANT ALL ON SERVER server1 TO ROLE sentry_admin
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20161116115454_c4d9df1b-3333-4072-8487-0f535ec81407); Time taken: 0.108 seconds
INFO  : OK
No rows affected (0.186 seconds)
0: jdbc:hive2://ip-172-20-0-5.eu-central-1.co> GRANT ROLE sentry_admin TO GROUP patelliandrea;
INFO  : Compiling command(queryId=hive_20161116115454_d2faf956-fae5-4df1-b2db-c37b98306a26): GRANT ROLE sentry_admin TO GROUP patelliandrea
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:null, properties:null)
INFO  : Completed compiling command(queryId=hive_20161116115454_d2faf956-fae5-4df1-b2db-c37b98306a26); Time taken: 0.061 seconds
INFO  : Executing command(queryId=hive_20161116115454_d2faf956-fae5-4df1-b2db-c37b98306a26): GRANT ROLE sentry_admin TO GROUP patelliandrea
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20161116115454_d2faf956-fae5-4df1-b2db-c37b98306a26); Time taken: 0.08 seconds
INFO  : OK
No rows affected (0.155 seconds)
0: jdbc:hive2://ip-172-20-0-5.eu-central-1.co> SHOW TABLES;
INFO  : Compiling command(queryId=hive_20161116115454_65ca026a-6c70-4f6e-a32b-346dab777685): SHOW TABLES
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:[FieldSchema(name:tab_name, type:string, comment:from deserializer)], properties:null)
INFO  : Completed compiling command(queryId=hive_20161116115454_65ca026a-6c70-4f6e-a32b-346dab777685); Time taken: 0.052 seconds
INFO  : Executing command(queryId=hive_20161116115454_65ca026a-6c70-4f6e-a32b-346dab777685): SHOW TABLES
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20161116115454_65ca026a-6c70-4f6e-a32b-346dab777685); Time taken: 0.143 seconds
INFO  : OK
+------------+--+
|  tab_name  |
+------------+--+
| customers  |
| sample_07  |
| sample_08  |
| web_logs   |
+------------+--+
4 rows selected (0.287 seconds)
```

## Create additional test users
```
[ec2-user@ip-172-20-0-4 ~]$ ansible  padrinocluster -a "sudo groupadd selector"
[ec2-user@ip-172-20-0-4 ~]$ ansible  padrinocluster -a "sudo groupadd inserters"
[ec2-user@ip-172-20-0-4 ~]$ ansible  padrinocluster -a "sudo useradd -u 1100 -g selector george"
[ec2-user@ip-172-20-0-4 ~]$ ansible  padrinocluster -a "sudo useradd -u 1200 -g inserters ferdinand"
[ec2-user@ip-172-20-0-4 ~]$ kadmin.local: add_principal george
[ec2-user@ip-172-20-0-4 ~]$ kadmin.local: add_principal ferdinand
```

## Create user roles
```
0: jdbc:hive2://ip-172-20-0-5.eu-central-1.co> CREATE ROLE reads;
INFO  : Compiling command(queryId=hive_20161116120000_ba2748e2-8185-489e-a54b-ae84934fd3cc): CREATE ROLE reads
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:null, properties:null)
INFO  : Completed compiling command(queryId=hive_20161116120000_ba2748e2-8185-489e-a54b-ae84934fd3cc); Time taken: 0.064 seconds
INFO  : Executing command(queryId=hive_20161116120000_ba2748e2-8185-489e-a54b-ae84934fd3cc): CREATE ROLE reads
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20161116120000_ba2748e2-8185-489e-a54b-ae84934fd3cc); Time taken: 0.038 seconds
INFO  : OK
No rows affected (0.152 seconds)
0: jdbc:hive2://ip-172-20-0-5.eu-central-1.co> CREATE ROLE writes;
INFO  : Compiling command(queryId=hive_20161116120000_de7def93-cec1-4c6d-bc37-e819019b383d): CREATE ROLE writes
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:null, properties:null)
INFO  : Completed compiling command(queryId=hive_20161116120000_de7def93-cec1-4c6d-bc37-e819019b383d); Time taken: 0.062 seconds
INFO  : Executing command(queryId=hive_20161116120000_de7def93-cec1-4c6d-bc37-e819019b383d): CREATE ROLE writes
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20161116120000_de7def93-cec1-4c6d-bc37-e819019b383d); Time taken: 0.023 seconds
INFO  : OK
No rows affected (0.095 seconds)
```

## Grant read privilege for all tables to `reads`
```
0: jdbc:hive2://ip-172-20-0-5.eu-central-1.co> GRANT SELECT ON DATABASE default TO ROLE reads;
INFO  : Compiling command(queryId=hive_20161116120101_f375f3f3-eb49-4cd2-adb7-43d4e0ac94d0): GRANT SELECT ON DATABASE default TO ROLE reads
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:null, properties:null)
INFO  : Completed compiling command(queryId=hive_20161116120101_f375f3f3-eb49-4cd2-adb7-43d4e0ac94d0); Time taken: 0.053 seconds
INFO  : Executing command(queryId=hive_20161116120101_f375f3f3-eb49-4cd2-adb7-43d4e0ac94d0): GRANT SELECT ON DATABASE default TO ROLE reads
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20161116120101_f375f3f3-eb49-4cd2-adb7-43d4e0ac94d0); Time taken: 0.043 seconds
INFO  : OK
No rows affected (0.107 seconds)
0: jdbc:hive2://ip-172-20-0-5.eu-central-1.co> GRANT ROLE reads TO GROUP selector;
INFO  : Compiling command(queryId=hive_20161116120101_b1374577-f163-411e-bfe4-2c401c7bbb40): GRANT ROLE reads TO GROUP selector
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:null, properties:null)
INFO  : Completed compiling command(queryId=hive_20161116120101_b1374577-f163-411e-bfe4-2c401c7bbb40); Time taken: 0.046 seconds
INFO  : Executing command(queryId=hive_20161116120101_b1374577-f163-411e-bfe4-2c401c7bbb40): GRANT ROLE reads TO GROUP selector
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20161116120101_b1374577-f163-411e-bfe4-2c401c7bbb40); Time taken: 0.041 seconds
INFO  : OK
No rows affected (0.095 seconds)
```

## Grant read privilege for `default.sample07` only to 'writes':
```
0: jdbc:hive2://ip-172-20-0-5.eu-central-1.co> GRANT SELECT ON DATABASE default TO ROLE reads;
INFO  : Compiling command(queryId=hive_20161116120101_7f80ec00-89b5-41f7-851d-4673f0537c79): GRANT SELECT ON DATABASE default TO ROLE reads
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:null, properties:null)
INFO  : Completed compiling command(queryId=hive_20161116120101_7f80ec00-89b5-41f7-851d-4673f0537c79); Time taken: 0.044 seconds
INFO  : Executing command(queryId=hive_20161116120101_7f80ec00-89b5-41f7-851d-4673f0537c79): GRANT SELECT ON DATABASE default TO ROLE reads
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20161116120101_7f80ec00-89b5-41f7-851d-4673f0537c79); Time taken: 0.022 seconds
INFO  : OK
No rows affected (0.077 seconds)
0: jdbc:hive2://ip-172-20-0-5.eu-central-1.co> GRANT ROLE reads TO GROUP selector;
INFO  : Compiling command(queryId=hive_20161116120101_cbc4a574-cf81-4cd7-af15-e110ff751e40): GRANT ROLE reads TO GROUP selector
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:null, properties:null)
INFO  : Completed compiling command(queryId=hive_20161116120101_cbc4a574-cf81-4cd7-af15-e110ff751e40); Time taken: 0.043 seconds
INFO  : Executing command(queryId=hive_20161116120101_cbc4a574-cf81-4cd7-af15-e110ff751e40): GRANT ROLE reads TO GROUP selector
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20161116120101_cbc4a574-cf81-4cd7-af15-e110ff751e40); Time taken: 0.017 seconds
INFO  : OK
No rows affected (0.073 seconds)
```

## Grant read privilege for `default.sample07` only to 'writes':
```
0: jdbc:hive2://ip-172-20-0-5.eu-central-1.co> REVOKE ALL ON DATABASE default FROM ROLE writes;
INFO  : Compiling command(queryId=hive_20161116120202_833cc211-b258-4f86-b1a2-5ba62c3089b5): REVOKE ALL ON DATABASE default FROM ROLE writes
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:null, properties:null)
INFO  : Completed compiling command(queryId=hive_20161116120202_833cc211-b258-4f86-b1a2-5ba62c3089b5); Time taken: 0.048 seconds
INFO  : Executing command(queryId=hive_20161116120202_833cc211-b258-4f86-b1a2-5ba62c3089b5): REVOKE ALL ON DATABASE default FROM ROLE writes
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20161116120202_833cc211-b258-4f86-b1a2-5ba62c3089b5); Time taken: 0.088 seconds
INFO  : OK
No rows affected (0.146 seconds)
0: jdbc:hive2://ip-172-20-0-5.eu-central-1.co> GRANT SELECT ON default.sample_07 TO ROLE writes;
INFO  : Compiling command(queryId=hive_20161116120202_84fb776c-ed7e-49fa-939d-7a20e550c46c): GRANT SELECT ON default.sample_07 TO ROLE writes
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:null, properties:null)
INFO  : Completed compiling command(queryId=hive_20161116120202_84fb776c-ed7e-49fa-939d-7a20e550c46c); Time taken: 0.05 seconds
INFO  : Executing command(queryId=hive_20161116120202_84fb776c-ed7e-49fa-939d-7a20e550c46c): GRANT SELECT ON default.sample_07 TO ROLE writes
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20161116120202_84fb776c-ed7e-49fa-939d-7a20e550c46c); Time taken: 0.028 seconds
INFO  : OK
No rows affected (0.089 seconds)
0: jdbc:hive2://ip-172-20-0-5.eu-central-1.co> GRANT ROLE writes TO GROUP inserters;
INFO  : Compiling command(queryId=hive_20161116120202_5852ff7b-7aa4-458d-8d96-6afa0d342978): GRANT ROLE writes TO GROUP inserters
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:null, properties:null)
INFO  : Completed compiling command(queryId=hive_20161116120202_5852ff7b-7aa4-458d-8d96-6afa0d342978); Time taken: 0.059 seconds
INFO  : Executing command(queryId=hive_20161116120202_5852ff7b-7aa4-458d-8d96-6afa0d342978): GRANT ROLE writes TO GROUP inserters
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20161116120202_5852ff7b-7aa4-458d-8d96-6afa0d342978); Time taken: 0.036 seconds
INFO  : OK
No rows affected (0.106 seconds)
```

## `kinit` as george, then login to beeline and show tables
```
[ec2-user@ip-172-20-0-4 ~]$ kinit george
Password for george@EU-CENTRAL-1.COMPUTE.INTERNAL:

[ec2-user@ip-172-20-0-4 ~]$ beeline
beeline> !connect jdbc:hive2://ip-172-20-0-5.eu-central-1.compute.internal:10000/default;principal=hive/

0: jdbc:hive2://ip-172-20-0-5.eu-central-1.co> show tables;
INFO  : Compiling command(queryId=hive_20161116120303_eac879a4-fd6c-4bdf-aa2d-c9aab8aeede8): show tables
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:[FieldSchema(name:tab_name, type:string, comment:from deserializer)], properties:null)
INFO  : Completed compiling command(queryId=hive_20161116120303_eac879a4-fd6c-4bdf-aa2d-c9aab8aeede8); Time taken: 0.057 seconds
INFO  : Executing command(queryId=hive_20161116120303_eac879a4-fd6c-4bdf-aa2d-c9aab8aeede8): show tables
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20161116120303_eac879a4-fd6c-4bdf-aa2d-c9aab8aeede8); Time taken: 0.135 seconds
INFO  : OK
+------------+--+
|  tab_name  |
+------------+--+
| customers  |
| sample_07  |
| sample_08  |
| web_logs   |
+------------+--+
4 rows selected (0.272 seconds)
0: jdbc:hive2://ip-172-20-0-5.eu-central-1.co>
```
## `kinit` as ferdinand, then login to beeline and show tables
```
[ec2-user@ip-172-20-0-4 ~]$ kinit ferdinand
Password for ferdinand@EU-CENTRAL-1.COMPUTE.INTERNAL:

[ec2-user@ip-172-20-0-4 ~]$ beeline
Java HotSpot(TM) 64-Bit Server VM warning: ignoring option MaxPermSize=512M; support was removed in 8.0
Java HotSpot(TM) 64-Bit Server VM warning: ignoring option MaxPermSize=512M; support was removed in 8.0taining PrefixTreeCodec is not present.  Continuing without it.
Beeline version 1.1.0-cdh5.9.0 by Apache Hive
beeline> !connect jdbc:hive2://ip-172-20-0-5.eu-central-1.compute.internal:10000/

0: jdbc:hive2://ip-172-20-0-5.eu-central-1.co> show tables;
INFO  : Compiling command(queryId=hive_20161116120303_51628c86-07f8-492f-b3f1-a5a406730df8): show tables
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:[FieldSchema(name:tab_name, type:string, comment:from deserializer)], properties:null)
INFO  : Completed compiling command(queryId=hive_20161116120303_51628c86-07f8-492f-b3f1-a5a406730df8); Time taken: 0.052 seconds
INFO  : Executing command(queryId=hive_20161116120303_51628c86-07f8-492f-b3f1-a5a406730df8): show tables
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20161116120303_51628c86-07f8-492f-b3f1-a5a406730df8); Time taken: 0.11 seconds
INFO  : OK
+------------+--+
|  tab_name  |
+------------+--+
| sample_07  |
+------------+--+
1 row selected (0.243 seconds)
```