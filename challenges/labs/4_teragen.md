## Teragen command
```
[donald@ip-10-1-0-7 ec2-user]$ time hadoop jar /opt/cloudera/parcels/CDH/jars/hadoop-examples.jar teragen -Dmapreduce.job.maps=6 -Ddfs.block.size=33554432 51200000 tgen512m
17/01/27 11:24:58 INFO client.RMProxy: Connecting to ResourceManager at ip-10-1-0-10.eu-central-1.compute.internal/10.1.0.10:8032
17/01/27 11:24:58 INFO terasort.TeraSort: Generating 51200000 using 6
17/01/27 11:24:58 INFO mapreduce.JobSubmitter: number of splits:6
17/01/27 11:24:58 INFO Configuration.deprecation: dfs.block.size is deprecated. Instead, use dfs.blocksize
17/01/27 11:24:58 INFO mapreduce.JobSubmitter: Submitting tokens for job: job_1485532936888_0002
17/01/27 11:24:59 INFO impl.YarnClientImpl: Submitted application application_1485532936888_0002
17/01/27 11:24:59 INFO mapreduce.Job: The url to track the job: http://ip-10-1-0-10.eu-central-1.compute.internal:8088/proxy/application_1485532936888_0002/
17/01/27 11:24:59 INFO mapreduce.Job: Running job: job_1485532936888_0002
17/01/27 11:25:05 INFO mapreduce.Job: Job job_1485532936888_0002 running in uber mode : false
17/01/27 11:25:05 INFO mapreduce.Job:  map 0% reduce 0%
17/01/27 11:25:19 INFO mapreduce.Job:  map 3% reduce 0%
17/01/27 11:25:20 INFO mapreduce.Job:  map 16% reduce 0%
17/01/27 11:25:22 INFO mapreduce.Job:  map 17% reduce 0%
17/01/27 11:25:23 INFO mapreduce.Job:  map 23% reduce 0%
17/01/27 11:25:25 INFO mapreduce.Job:  map 24% reduce 0%
17/01/27 11:25:26 INFO mapreduce.Job:  map 27% reduce 0%
17/01/27 11:25:28 INFO mapreduce.Job:  map 28% reduce 0%
17/01/27 11:25:29 INFO mapreduce.Job:  map 32% reduce 0%
17/01/27 11:25:31 INFO mapreduce.Job:  map 33% reduce 0%
17/01/27 11:25:32 INFO mapreduce.Job:  map 37% reduce 0%
17/01/27 11:25:34 INFO mapreduce.Job:  map 38% reduce 0%
17/01/27 11:25:35 INFO mapreduce.Job:  map 43% reduce 0%
17/01/27 11:25:38 INFO mapreduce.Job:  map 47% reduce 0%
17/01/27 11:25:40 INFO mapreduce.Job:  map 48% reduce 0%
17/01/27 11:25:41 INFO mapreduce.Job:  map 52% reduce 0%
17/01/27 11:25:44 INFO mapreduce.Job:  map 56% reduce 0%
17/01/27 11:25:47 INFO mapreduce.Job:  map 61% reduce 0%
17/01/27 11:25:49 INFO mapreduce.Job:  map 62% reduce 0%
17/01/27 11:25:50 INFO mapreduce.Job:  map 65% reduce 0%
17/01/27 11:25:52 INFO mapreduce.Job:  map 66% reduce 0%
17/01/27 11:25:53 INFO mapreduce.Job:  map 70% reduce 0%
17/01/27 11:25:55 INFO mapreduce.Job:  map 71% reduce 0%
17/01/27 11:25:56 INFO mapreduce.Job:  map 73% reduce 0%
17/01/27 11:25:59 INFO mapreduce.Job:  map 74% reduce 0%
17/01/27 11:26:02 INFO mapreduce.Job:  map 75% reduce 0%
17/01/27 11:26:08 INFO mapreduce.Job:  map 76% reduce 0%
17/01/27 11:26:11 INFO mapreduce.Job:  map 77% reduce 0%
17/01/27 11:26:14 INFO mapreduce.Job:  map 78% reduce 0%
17/01/27 11:26:16 INFO mapreduce.Job:  map 79% reduce 0%
17/01/27 11:26:17 INFO mapreduce.Job:  map 80% reduce 0%
17/01/27 11:26:20 INFO mapreduce.Job:  map 81% reduce 0%
17/01/27 11:26:23 INFO mapreduce.Job:  map 82% reduce 0%
17/01/27 11:26:26 INFO mapreduce.Job:  map 83% reduce 0%
17/01/27 11:26:29 INFO mapreduce.Job:  map 84% reduce 0%
17/01/27 11:26:31 INFO mapreduce.Job:  map 85% reduce 0%
17/01/27 11:26:32 INFO mapreduce.Job:  map 86% reduce 0%
17/01/27 11:26:35 INFO mapreduce.Job:  map 87% reduce 0%
17/01/27 11:26:38 INFO mapreduce.Job:  map 89% reduce 0%
17/01/27 11:26:41 INFO mapreduce.Job:  map 90% reduce 0%
17/01/27 11:26:44 INFO mapreduce.Job:  map 91% reduce 0%
17/01/27 11:26:46 INFO mapreduce.Job:  map 92% reduce 0%
17/01/27 11:26:47 INFO mapreduce.Job:  map 93% reduce 0%
17/01/27 11:26:50 INFO mapreduce.Job:  map 94% reduce 0%
17/01/27 11:26:53 INFO mapreduce.Job:  map 95% reduce 0%
17/01/27 11:26:55 INFO mapreduce.Job:  map 96% reduce 0%
17/01/27 11:26:58 INFO mapreduce.Job:  map 97% reduce 0%
17/01/27 11:26:59 INFO mapreduce.Job:  map 98% reduce 0%
17/01/27 11:27:02 INFO mapreduce.Job:  map 99% reduce 0%
17/01/27 11:27:05 INFO mapreduce.Job:  map 100% reduce 0%
17/01/27 11:27:08 INFO mapreduce.Job: Job job_1485532936888_0002 completed successfully
17/01/27 11:27:08 INFO mapreduce.Job: Counters: 31
        File System Counters
                FILE: Number of bytes read=0
                FILE: Number of bytes written=737430
                FILE: Number of read operations=0
                FILE: Number of large read operations=0
                FILE: Number of write operations=0
                HDFS: Number of bytes read=511
                HDFS: Number of bytes written=5120000000
                HDFS: Number of read operations=24
                HDFS: Number of large read operations=0
                HDFS: Number of write operations=12
        Job Counters
                Launched map tasks=6
                Other local map tasks=6
                Total time spent by all maps in occupied slots (ms)=709210
                Total time spent by all reduces in occupied slots (ms)=0
                Total time spent by all map tasks (ms)=709210
                Total vcore-seconds taken by all map tasks=709210
                Total megabyte-seconds taken by all map tasks=726231040
        Map-Reduce Framework
                Map input records=51200000
                Map output records=51200000
                Input split bytes=511
                Spilled Records=0
                Failed Shuffles=0
                Merged Map outputs=0
                GC time elapsed (ms)=1315
                CPU time spent (ms)=91070
                Physical memory (bytes) snapshot=2321997824
                Virtual memory (bytes) snapshot=16718929920
                Total committed heap usage (bytes)=2111307776
        org.apache.hadoop.examples.terasort.TeraGen$Counters
                CHECKSUM=109963291816450258
        File Input Format Counters
                Bytes Read=0
        File Output Format Counters
                Bytes Written=5120000000

real    2m12.536s
user    0m6.966s
sys     0m0.340s
```

## Time output
```
real    2m12.536s
user    0m6.966s
sys     0m0.340s
```

## `/user/donald/tgen512m` 
[donald@ip-10-1-0-7 ec2-user]$ hdfs dfs -ls /user/donald/tgen512m
Found 7 items
-rw-r--r--   3 donald donald          0 2017-01-27 11:27 /user/donald/tgen512m/_SUCCESS
-rw-r--r--   3 donald donald  853333400 2017-01-27 11:27 /user/donald/tgen512m/part-m-00000
-rw-r--r--   3 donald donald  853333300 2017-01-27 11:27 /user/donald/tgen512m/part-m-00001
-rw-r--r--   3 donald donald  853333300 2017-01-27 11:27 /user/donald/tgen512m/part-m-00002
-rw-r--r--   3 donald donald  853333400 2017-01-27 11:27 /user/donald/tgen512m/part-m-00003
-rw-r--r--   3 donald donald  853333300 2017-01-27 11:27 /user/donald/tgen512m/part-m-00004
-rw-r--r--   3 donald donald  853333300 2017-01-27 11:27 /user/donald/tgen512m/part-m-00005
```

## Blocks associated with the directory
```
[donald@ip-10-1-0-7 ec2-user]$ hadoop fsck /user/donald/tgen512m
DEPRECATED: Use of this script to execute hdfs command is deprecated.
Instead use the hdfs command for it.

Connecting to namenode via http://ip-10-1-0-10.eu-central-1.compute.internal:50070
FSCK started by donald (auth:SIMPLE) from /10.1.0.7 for path /user/donald/tgen512m at Fri Jan 27 11:30:53 EST 2017
.......Status: HEALTHY
 Total size:    5120000000 B
 Total dirs:    1
 Total files:   7
 Total symlinks:                0
 Total blocks (validated):      156 (avg. block size 32820512 B)
 Minimally replicated blocks:   156 (100.0 %)
 Over-replicated blocks:        0 (0.0 %)
 Under-replicated blocks:       0 (0.0 %)
 Mis-replicated blocks:         0 (0.0 %)
 Default replication factor:    3
 Average block replication:     3.0
 Corrupt blocks:                0
 Missing replicas:              0 (0.0 %)
 Number of data-nodes:          3
 Number of racks:               1
FSCK ended at Fri Jan 27 11:30:53 EST 2017 in 5 milliseconds


The filesystem under path '/user/donald/tgen512m' is HEALTHY
```