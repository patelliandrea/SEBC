```
[ec2-user@ip-10-1-0-9 ~]$ kinit vladimir
Password for vladimir@PATELLIANDREA.REMOTE:

[ec2-user@ip-10-1-0-9 ~]$ hadoop jar /opt/cloudera/parcels/CDH/lib/hadoop-mapreduce/hadoop-mapreduce-examples.jar pi 10 100
Number of Maps  = 10
Samples per Map = 100
Wrote input for Map #0
Wrote input for Map #1
Wrote input for Map #2
Wrote input for Map #3
Wrote input for Map #4
Wrote input for Map #5
Wrote input for Map #6
Wrote input for Map #7
Wrote input for Map #8
Wrote input for Map #9
Starting Job
17/01/27 12:02:48 INFO client.RMProxy: Connecting to ResourceManager at ip-10-1-0-10.eu-central-1.compute.internal/10.1.0.10:8032
17/01/27 12:02:49 INFO hdfs.DFSClient: Created token for vladimir: HDFS_DELEGATION_TOKEN owner=vladimir@PATELLIANDREA.REMOTE, renewer=yarn, realUser=, issueDate=1485536569050, maxDate=1486141369050, sequenceNumber=3, masterKeyId=2 on 10.1.0.10:8020
17/01/27 12:02:49 INFO security.TokenCache: Got dt for hdfs://ip-10-1-0-10.eu-central-1.compute.internal:8020; Kind: HDFS_DELEGATION_TOKEN, Service: 10.1.0.10:8020, Ident: (token for vladimir: HDFS_DELEGATION_TOKEN owner=vladimir@PATELLIANDREA.REMOTE, renewer=yarn, realUser=, issueDate=1485536569050, maxDate=1486141369050, sequenceNumber=3, masterKeyId=2)
17/01/27 12:02:49 INFO input.FileInputFormat: Total input paths to process : 10
17/01/27 12:02:50 INFO mapreduce.JobSubmitter: number of splits:10
17/01/27 12:02:51 INFO mapreduce.JobSubmitter: Submitting tokens for job: job_1485536159571_0002
17/01/27 12:02:51 INFO mapreduce.JobSubmitter: Kind: HDFS_DELEGATION_TOKEN, Service: 10.1.0.10:8020, Ident: (token for vladimir: HDFS_DELEGATION_TOKEN owner=vladimir@PATELLIANDREA.REMOTE, renewer=yarn, realUser=, issueDate=1485536569050, maxDate=1486141369050, sequenceNumber=3, masterKeyId=2)
17/01/27 12:02:51 INFO impl.YarnClientImpl: Submitted application application_1485536159571_0002
17/01/27 12:02:51 INFO mapreduce.Job: The url to track the job: http://ip-10-1-0-10.eu-central-1.compute.internal:8088/proxy/application_1485536159571_0002/
17/01/27 12:02:51 INFO mapreduce.Job: Running job: job_1485536159571_0002
17/01/27 12:03:26 INFO mapreduce.Job: Job job_1485536159571_0002 running in uber mode : false
17/01/27 12:03:26 INFO mapreduce.Job:  map 0% reduce 0%
17/01/27 12:03:33 INFO mapreduce.Job:  map 10% reduce 0%
17/01/27 12:03:34 INFO mapreduce.Job:  map 20% reduce 0%
17/01/27 12:03:35 INFO mapreduce.Job:  map 30% reduce 0%
17/01/27 12:03:38 INFO mapreduce.Job:  map 40% reduce 0%
17/01/27 12:03:39 INFO mapreduce.Job:  map 50% reduce 0%
17/01/27 12:03:40 INFO mapreduce.Job:  map 60% reduce 0%
17/01/27 12:03:41 INFO mapreduce.Job:  map 90% reduce 0%
17/01/27 12:03:47 INFO mapreduce.Job:  map 100% reduce 0%
17/01/27 12:03:49 INFO mapreduce.Job:  map 100% reduce 100%
17/01/27 12:03:52 INFO mapreduce.Job: Job job_1485536159571_0002 completed successfully
17/01/27 12:03:53 INFO mapreduce.Job: Counters: 50
        File System Counters
                FILE: Number of bytes read=93
                FILE: Number of bytes written=1368895
                FILE: Number of read operations=0
                FILE: Number of large read operations=0
                FILE: Number of write operations=0
                HDFS: Number of bytes read=3010
                HDFS: Number of bytes written=215
                HDFS: Number of read operations=43
                HDFS: Number of large read operations=0
                HDFS: Number of write operations=3
        Job Counters
                Launched map tasks=10
                Launched reduce tasks=1
                Data-local map tasks=8
                Rack-local map tasks=2
                Total time spent by all maps in occupied slots (ms)=74948
                Total time spent by all reduces in occupied slots (ms)=5293
                Total time spent by all map tasks (ms)=74948
                Total time spent by all reduce tasks (ms)=5293
                Total vcore-seconds taken by all map tasks=74948
                Total vcore-seconds taken by all reduce tasks=5293
                Total megabyte-seconds taken by all map tasks=76746752
                Total megabyte-seconds taken by all reduce tasks=5420032
        Map-Reduce Framework
                Map input records=10
                Map output records=20
                Map output bytes=180
                Map output materialized bytes=340
                Input split bytes=1830
                Combine input records=0
                Combine output records=0
                Reduce input groups=2
                Reduce shuffle bytes=340
                Reduce input records=20
                Reduce output records=0
                Spilled Records=40
                Shuffled Maps =10
                Failed Shuffles=0
                Merged Map outputs=10
                GC time elapsed (ms)=1762
                CPU time spent (ms)=7740
                Physical memory (bytes) snapshot=4693442560
                Virtual memory (bytes) snapshot=30645354496
                Total committed heap usage (bytes)=4645715968
        Shuffle Errors
                BAD_ID=0
                CONNECTION=0
                IO_ERROR=0
                WRONG_LENGTH=0
                WRONG_MAP=0
                WRONG_REDUCE=0
        File Input Format Counters
                Bytes Read=1180
        File Output Format Counters
                Bytes Written=97
Job Finished in 64.994 seconds
Estimated value of Pi is 3.14800000000000000000
```