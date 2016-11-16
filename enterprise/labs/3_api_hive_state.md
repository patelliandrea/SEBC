## Stop the Hive Service
```
[ec2-user@ip-172-20-0-4 ~]$ curl -X POST -u patelliandrea:cloudera 'http://54.93.129.189:7180/api/v2/clusters/patelliandrea/services/hive/commands/stop'
{
  "id" : 862,
  "name" : "Stop",
  "startTime" : "2016-11-16T10:02:53.613Z",
  "active" : true,
  "serviceRef" : {
    "clusterName" : "cluster",
    "serviceName" : "hive"
  }
}
```

## Start the Hive Service
```
[ec2-user@ip-172-20-0-4 ~]$ curl -X POST -u patelliandrea:cloudera 'http://54.93.129.189:7180/api/v2/clusters/patelliandrea/services/hive/commands/start'
{
  "id" : 866,
  "name" : "Start",
  "startTime" : "2016-11-16T10:03:55.573Z",
  "active" : true,
  "serviceRef" : {
    "clusterName" : "cluster",
    "serviceName" : "hive"
  }
}
```

## Check the Hive Service
```
[ec2-user@ip-172-20-0-4 ~]$ curl -u patelliandrea:cloudera 'http://54.93.129.189:7180/api/v2/clusters/patelliandrea/services/hive'
{
  "name" : "hive",
  "type" : "HIVE",
  "clusterRef" : {
    "clusterName" : "cluster"
  },
  "serviceUrl" : "http://ip-172-20-0-4.eu-central-1.compute.internal:7180/cmf/serviceRedirect/hive",
  "serviceState" : "STARTED",
  "healthSummary" : "GOOD",
  "healthChecks" : [ {
    "name" : "HIVE_HIVEMETASTORES_HEALTHY",
    "summary" : "GOOD"
  }, {
    "name" : "HIVE_HIVESERVER2S_HEALTHY",
    "summary" : "GOOD"
  } ],
  "configStale" : false,
  "maintenanceMode" : false,
  "maintenanceOwners" : [ ],
  "displayName" : "Hive"
}
```