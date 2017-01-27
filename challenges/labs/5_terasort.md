```
[ec2-user@ip-10-1-0-7 ~]$ kinit donald
Password for donald@PATELLIANDREA.REMOTE:

[ec2-user@ip-10-1-0-7 ~]$ time hadoop jar /opt/cloudera/parcels/CDH/jars/hadoop-examples.jar terasort tgen512m tsort512m
17/01/27 12:01:11 INFO terasort.TeraSort: starting
17/01/27 12:01:12 INFO hdfs.DFSClient: Created token for donald: HDFS_DELEGATION_TOKEN owner=donald@PATELLIANDREA.REMOTE, renewer=yarn, realUser=, issueDate=1485536472856, maxDate=1486141272856, sequenceNumber=2, masterKeyId=2 on 10.1.0.10:8020
17/01/27 12:01:12 INFO security.TokenCache: Got dt for hdfs://ip-10-1-0-10.eu-central-1.compute.internal:8020; Kind: HDFS_DELEGATION_TOKEN, Service: 10.1.0.10:8020, Ident: (token for donald: HDFS_DELEGATION_TOKEN owner=donald@PATELLIANDREA.REMOTE, renewer=yarn, realUser=, issueDate=1485536472856, maxDate=1486141272856, sequenceNumber=2, masterKeyId=2)
17/01/27 12:01:13 INFO input.FileInputFormat: Total input paths to process : 6
Spent 327ms computing base-splits.
Spent 5ms computing TeraScheduler splits.
Computing input splits took 333ms
Sampling 10 splits of 156
Making 8 from 100000 sampled records
Computing parititions took 628ms
Spent 963ms computing partitions.
17/01/27 12:01:13 INFO client.RMProxy: Connecting to ResourceManager at ip-10-1-0-10.eu-central-1.compute.internal/10.1.0.10:8032
17/01/27 12:01:14 INFO mapreduce.JobSubmitter: number of splits:156
17/01/27 12:01:14 INFO mapreduce.JobSubmitter: Submitting tokens for job: job_1485536159571_0001
17/01/27 12:01:14 INFO mapreduce.JobSubmitter: Kind: HDFS_DELEGATION_TOKEN, Service: 10.1.0.10:8020, Ident: (token for donald: HDFS_DELEGATION_TOKEN owner=donald@PATELLIANDREA.REMOTE, renewer=yarn, realUser=, issueDate=1485536472856, maxDate=1486141272856, sequenceNumber=2, masterKeyId=2)
17/01/27 12:01:15 INFO impl.YarnClientImpl: Submitted application application_1485536159571_0001
17/01/27 12:01:15 INFO mapreduce.Job: The url to track the job: http://ip-10-1-0-10.eu-central-1.compute.internal:8088/proxy/application_1485536159571_0001/
17/01/27 12:01:15 INFO mapreduce.Job: Running job: job_1485536159571_0001
17/01/27 12:01:24 INFO mapreduce.Job: Job job_1485536159571_0001 running in uber mode : false
17/01/27 12:01:24 INFO mapreduce.Job:  map 0% reduce 0%
17/01/27 12:01:34 INFO mapreduce.Job:  map 1% reduce 0%
17/01/27 12:01:35 INFO mapreduce.Job:  map 2% reduce 0%
17/01/27 12:01:42 INFO mapreduce.Job:  map 6% reduce 0%
17/01/27 12:01:43 INFO mapreduce.Job:  map 10% reduce 0%
17/01/27 12:01:44 INFO mapreduce.Job:  map 12% reduce 0%
17/01/27 12:01:52 INFO mapreduce.Job:  map 13% reduce 0%
17/01/27 12:01:53 INFO mapreduce.Job:  map 16% reduce 0%
17/01/27 12:01:54 INFO mapreduce.Job:  map 21% reduce 0%
17/01/27 12:01:58 INFO mapreduce.Job:  map 22% reduce 0%
17/01/27 12:02:02 INFO mapreduce.Job:  map 23% reduce 0%
17/01/27 12:02:04 INFO mapreduce.Job:  map 25% reduce 0%
17/01/27 12:02:05 INFO mapreduce.Job:  map 26% reduce 0%
17/01/27 12:02:06 INFO mapreduce.Job:  map 29% reduce 0%
17/01/27 12:02:07 INFO mapreduce.Job:  map 31% reduce 0%
17/01/27 12:02:09 INFO mapreduce.Job:  map 32% reduce 0%
17/01/27 12:02:10 INFO mapreduce.Job:  map 33% reduce 0%
17/01/27 12:02:14 INFO mapreduce.Job:  map 35% reduce 0%
17/01/27 12:02:16 INFO mapreduce.Job:  map 37% reduce 0%
17/01/27 12:02:17 INFO mapreduce.Job:  map 40% reduce 0%
17/01/27 12:02:18 INFO mapreduce.Job:  map 42% reduce 0%
17/01/27 12:02:21 INFO mapreduce.Job:  map 43% reduce 0%
17/01/27 12:02:23 INFO mapreduce.Job:  map 44% reduce 0%
17/01/27 12:02:25 INFO mapreduce.Job:  map 45% reduce 0%
17/01/27 12:02:26 INFO mapreduce.Job:  map 46% reduce 0%
17/01/27 12:02:27 INFO mapreduce.Job:  map 48% reduce 0%
17/01/27 12:02:28 INFO mapreduce.Job:  map 49% reduce 0%
17/01/27 12:02:29 INFO mapreduce.Job:  map 52% reduce 0%
17/01/27 12:02:30 INFO mapreduce.Job:  map 53% reduce 0%
17/01/27 12:02:33 INFO mapreduce.Job:  map 54% reduce 0%
17/01/27 12:02:34 INFO mapreduce.Job:  map 55% reduce 0%
17/01/27 12:02:35 INFO mapreduce.Job:  map 56% reduce 0%
17/01/27 12:02:37 INFO mapreduce.Job:  map 58% reduce 0%
17/01/27 12:02:38 INFO mapreduce.Job:  map 59% reduce 0%
17/01/27 12:02:39 INFO mapreduce.Job:  map 60% reduce 0%
17/01/27 12:02:40 INFO mapreduce.Job:  map 62% reduce 0%
17/01/27 12:02:41 INFO mapreduce.Job:  map 63% reduce 0%
17/01/27 12:02:44 INFO mapreduce.Job:  map 65% reduce 0%
17/01/27 12:02:45 INFO mapreduce.Job:  map 66% reduce 0%
17/01/27 12:02:47 INFO mapreduce.Job:  map 67% reduce 0%
17/01/27 12:02:49 INFO mapreduce.Job:  map 69% reduce 0%
17/01/27 12:02:51 INFO mapreduce.Job:  map 70% reduce 0%
17/01/27 12:02:52 INFO mapreduce.Job:  map 71% reduce 0%
17/01/27 12:02:53 INFO mapreduce.Job:  map 73% reduce 0%
17/01/27 12:02:54 INFO mapreduce.Job:  map 74% reduce 0%
17/01/27 12:02:56 INFO mapreduce.Job:  map 76% reduce 0%
17/01/27 12:02:58 INFO mapreduce.Job:  map 77% reduce 0%
17/01/27 12:02:59 INFO mapreduce.Job:  map 79% reduce 0%
17/01/27 12:03:01 INFO mapreduce.Job:  map 80% reduce 0%
17/01/27 12:03:02 INFO mapreduce.Job:  map 81% reduce 0%
17/01/27 12:03:03 INFO mapreduce.Job:  map 82% reduce 0%
17/01/27 12:03:04 INFO mapreduce.Job:  map 84% reduce 0%
17/01/27 12:03:05 INFO mapreduce.Job:  map 85% reduce 0%
17/01/27 12:03:06 INFO mapreduce.Job:  map 86% reduce 0%
17/01/27 12:03:07 INFO mapreduce.Job:  map 87% reduce 0%
17/01/27 12:03:09 INFO mapreduce.Job:  map 89% reduce 0%
17/01/27 12:03:10 INFO mapreduce.Job:  map 90% reduce 0%
17/01/27 12:03:12 INFO mapreduce.Job:  map 91% reduce 0%
17/01/27 12:03:14 INFO mapreduce.Job:  map 92% reduce 0%
17/01/27 12:03:16 INFO mapreduce.Job:  map 92% reduce 7%
17/01/27 12:03:18 INFO mapreduce.Job:  map 92% reduce 16%
17/01/27 12:03:19 INFO mapreduce.Job:  map 92% reduce 24%
17/01/27 12:03:21 INFO mapreduce.Job:  map 94% reduce 25%
17/01/27 12:03:22 INFO mapreduce.Job:  map 96% reduce 26%
17/01/27 12:03:23 INFO mapreduce.Job:  map 97% reduce 27%
17/01/27 12:03:24 INFO mapreduce.Job:  map 97% reduce 28%
17/01/27 12:03:27 INFO mapreduce.Job:  map 99% reduce 28%
17/01/27 12:03:28 INFO mapreduce.Job:  map 99% reduce 29%
17/01/27 12:03:29 INFO mapreduce.Job:  map 100% reduce 29%
17/01/27 12:03:30 INFO mapreduce.Job:  map 100% reduce 30%
17/01/27 12:03:31 INFO mapreduce.Job:  map 100% reduce 36%
17/01/27 12:03:32 INFO mapreduce.Job:  map 100% reduce 38%
17/01/27 12:03:33 INFO mapreduce.Job:  map 100% reduce 46%
17/01/27 12:03:34 INFO mapreduce.Job:  map 100% reduce 54%
17/01/27 12:03:35 INFO mapreduce.Job:  map 100% reduce 55%
17/01/27 12:03:36 INFO mapreduce.Job:  map 100% reduce 62%
17/01/27 12:03:37 INFO mapreduce.Job:  map 100% reduce 64%
17/01/27 12:03:38 INFO mapreduce.Job:  map 100% reduce 65%
17/01/27 12:03:39 INFO mapreduce.Job:  map 100% reduce 68%
17/01/27 12:03:40 INFO mapreduce.Job:  map 100% reduce 70%
17/01/27 12:03:41 INFO mapreduce.Job:  map 100% reduce 71%
17/01/27 12:03:42 INFO mapreduce.Job:  map 100% reduce 76%
17/01/27 12:03:43 INFO mapreduce.Job:  map 100% reduce 81%
17/01/27 12:03:44 INFO mapreduce.Job:  map 100% reduce 82%
17/01/27 12:03:45 INFO mapreduce.Job:  map 100% reduce 87%
17/01/27 12:03:46 INFO mapreduce.Job:  map 100% reduce 88%
17/01/27 12:03:47 INFO mapreduce.Job:  map 100% reduce 90%
17/01/27 12:03:48 INFO mapreduce.Job:  map 100% reduce 94%
17/01/27 12:03:49 INFO mapreduce.Job:  map 100% reduce 95%
17/01/27 12:03:51 INFO mapreduce.Job:  map 100% reduce 98%
17/01/27 12:03:53 INFO mapreduce.Job:  map 100% reduce 100%
17/01/27 12:03:54 INFO mapreduce.Job: Job job_1485536159571_0001 completed successfully
17/01/27 12:03:54 INFO mapreduce.Job: Counters: 50
        File System Counters
                FILE: Number of bytes read=2269099382
                FILE: Number of bytes written=4513148747
                FILE: Number of read operations=0
                FILE: Number of large read operations=0
                FILE: Number of write operations=0
                HDFS: Number of bytes read=5120023868
                HDFS: Number of bytes written=5120000000
                HDFS: Number of read operations=492
                HDFS: Number of large read operations=0
                HDFS: Number of write operations=16
        Job Counters
                Launched map tasks=156
                Launched reduce tasks=8
                Data-local map tasks=116
                Rack-local map tasks=40
                Total time spent by all maps in occupied slots (ms)=1446897
                Total time spent by all reduces in occupied slots (ms)=329573
                Total time spent by all map tasks (ms)=1446897
                Total time spent by all reduce tasks (ms)=329573
                Total vcore-seconds taken by all map tasks=1446897
                Total vcore-seconds taken by all reduce tasks=329573
                Total megabyte-seconds taken by all map tasks=1481622528
                Total megabyte-seconds taken by all reduce tasks=337482752
        Map-Reduce Framework
                Map input records=51200000
                Map output records=51200000
                Map output bytes=5222400000
                Map output materialized bytes=2223517695
                Input split bytes=23868
                Combine input records=0
                Combine output records=0
                Reduce input groups=51200000
                Reduce shuffle bytes=2223517695
                Reduce input records=51200000
                Reduce output records=51200000
                Spilled Records=102400000
                Shuffled Maps =1248
                Failed Shuffles=0
                Merged Map outputs=1248
                GC time elapsed (ms)=38869
                CPU time spent (ms)=806100
                Physical memory (bytes) snapshot=83094863872
                Virtual memory (bytes) snapshot=456975261696
                Total committed heap usage (bytes)=84636336128
        Shuffle Errors
                BAD_ID=0
                CONNECTION=0
                IO_ERROR=0
                WRONG_LENGTH=0
                WRONG_MAP=0
                WRONG_REDUCE=0
        File Input Format Counters
                Bytes Read=5120000000
        File Output Format Counters
                Bytes Written=5120000000
17/01/27 12:03:54 INFO terasort.TeraSort: done

real    2m44.191s
user    0m10.051s
sys     0m0.382s
```