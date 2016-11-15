## Test HDFS performance
To run the `teragen`, the following command was run:
```
[patelliandrea@ip-172-20-0-4 ~]$ time hadoop jar /opt/cloudera/parcels/CDH-5.9.0-1.cdh5.9.0.p0.23/jars/hadoop-examples.jar teragen -Dmapred.map.tasks=4 -Ddfs.block.size=33554432 107374182 /user/patelliandrea/teragen_data_10g
16/11/15 06:01:49 INFO Configuration.deprecation: session.id is deprecated. Instead, use dfs.metrics.session-id
16/11/15 06:01:49 INFO jvm.JvmMetrics: Initializing JVM Metrics with processName=JobTracker, sessionId=
16/11/15 06:01:49 INFO terasort.TeraSort: Generating 107374182 using 1
16/11/15 06:01:49 INFO mapreduce.JobSubmitter: number of splits:1
16/11/15 06:01:49 INFO Configuration.deprecation: dfs.block.size is deprecated. Instead, use dfs.blocksize
16/11/15 06:01:49 INFO Configuration.deprecation: mapred.map.tasks is deprecated. Instead, use mapreduce.job.maps
16/11/15 06:01:49 INFO mapreduce.JobSubmitter: Submitting tokens for job: job_local751525010_0001
16/11/15 06:01:49 INFO mapreduce.Job: The url to track the job: http://localhost:8080/
16/11/15 06:01:49 INFO mapreduce.Job: Running job: job_local751525010_0001
16/11/15 06:01:49 INFO mapred.LocalJobRunner: OutputCommitter set in config null
16/11/15 06:01:49 INFO output.FileOutputCommitter: File Output Committer Algorithm version is 1
16/11/15 06:01:49 INFO mapred.LocalJobRunner: OutputCommitter is org.apache.hadoop.mapreduce.lib.output.FileOutputCommitter
16/11/15 06:01:49 INFO mapred.LocalJobRunner: Waiting for map tasks
16/11/15 06:01:49 INFO mapred.LocalJobRunner: Starting task: attempt_local751525010_0001_m_000000_0
16/11/15 06:01:49 INFO output.FileOutputCommitter: File Output Committer Algorithm version is 1
16/11/15 06:01:49 INFO mapred.Task:  Using ResourceCalculatorProcessTree : [ ]
16/11/15 06:01:49 INFO mapred.MapTask: Processing split: org.apache.hadoop.examples.terasort.TeraGen$RangeInputFormat$RangeInputSplit@3d709d53
16/11/15 06:01:50 INFO mapreduce.Job: Job job_local751525010_0001 running in uber mode : false
16/11/15 06:01:50 INFO mapreduce.Job:  map 0% reduce 0%
16/11/15 06:01:55 INFO mapred.LocalJobRunner: map > map
16/11/15 06:01:56 INFO mapreduce.Job:  map 5% reduce 0%
16/11/15 06:01:58 INFO mapred.LocalJobRunner: map > map
16/11/15 06:01:59 INFO mapreduce.Job:  map 8% reduce 0%
16/11/15 06:02:01 INFO mapred.LocalJobRunner: map > map
16/11/15 06:02:02 INFO mapreduce.Job:  map 10% reduce 0%
16/11/15 06:02:04 INFO mapred.LocalJobRunner: map > map
16/11/15 06:02:05 INFO mapreduce.Job:  map 13% reduce 0%
16/11/15 06:02:07 INFO mapred.LocalJobRunner: map > map
16/11/15 06:02:08 INFO mapreduce.Job:  map 16% reduce 0%
16/11/15 06:02:10 INFO mapred.LocalJobRunner: map > map
16/11/15 06:02:11 INFO mapreduce.Job:  map 18% reduce 0%
16/11/15 06:02:13 INFO mapred.LocalJobRunner: map > map
16/11/15 06:02:14 INFO mapreduce.Job:  map 20% reduce 0%
16/11/15 06:02:16 INFO mapred.LocalJobRunner: map > map
16/11/15 06:02:17 INFO mapreduce.Job:  map 21% reduce 0%
16/11/15 06:02:19 INFO mapred.LocalJobRunner: map > map
16/11/15 06:02:20 INFO mapreduce.Job:  map 23% reduce 0%
16/11/15 06:02:22 INFO mapred.LocalJobRunner: map > map
16/11/15 06:02:23 INFO mapreduce.Job:  map 25% reduce 0%
16/11/15 06:02:25 INFO mapred.LocalJobRunner: map > map
16/11/15 06:02:26 INFO mapreduce.Job:  map 28% reduce 0%
16/11/15 06:02:28 INFO mapred.LocalJobRunner: map > map
16/11/15 06:02:29 INFO mapreduce.Job:  map 31% reduce 0%
16/11/15 06:02:31 INFO mapred.LocalJobRunner: map > map
16/11/15 06:02:32 INFO mapreduce.Job:  map 33% reduce 0%
16/11/15 06:02:34 INFO mapred.LocalJobRunner: map > map
16/11/15 06:02:35 INFO mapreduce.Job:  map 34% reduce 0%
16/11/15 06:02:37 INFO mapred.LocalJobRunner: map > map
16/11/15 06:02:38 INFO mapreduce.Job:  map 36% reduce 0%
16/11/15 06:02:40 INFO mapred.LocalJobRunner: map > map
16/11/15 06:02:41 INFO mapreduce.Job:  map 38% reduce 0%
16/11/15 06:02:43 INFO mapred.LocalJobRunner: map > map
16/11/15 06:02:44 INFO mapreduce.Job:  map 40% reduce 0%
16/11/15 06:02:46 INFO mapred.LocalJobRunner: map > map
16/11/15 06:02:47 INFO mapreduce.Job:  map 43% reduce 0%
16/11/15 06:02:49 INFO mapred.LocalJobRunner: map > map
16/11/15 06:02:50 INFO mapreduce.Job:  map 45% reduce 0%
16/11/15 06:02:52 INFO mapred.LocalJobRunner: map > map
16/11/15 06:02:53 INFO mapreduce.Job:  map 47% reduce 0%
16/11/15 06:02:55 INFO mapred.LocalJobRunner: map > map
16/11/15 06:02:56 INFO mapreduce.Job:  map 49% reduce 0%
16/11/15 06:02:58 INFO mapred.LocalJobRunner: map > map
16/11/15 06:02:59 INFO mapreduce.Job:  map 51% reduce 0%
16/11/15 06:03:01 INFO mapred.LocalJobRunner: map > map
16/11/15 06:03:02 INFO mapreduce.Job:  map 52% reduce 0%
16/11/15 06:03:04 INFO mapred.LocalJobRunner: map > map
16/11/15 06:03:05 INFO mapreduce.Job:  map 54% reduce 0%
16/11/15 06:03:07 INFO mapred.LocalJobRunner: map > map
16/11/15 06:03:08 INFO mapreduce.Job:  map 57% reduce 0%
16/11/15 06:03:10 INFO mapred.LocalJobRunner: map > map
16/11/15 06:03:11 INFO mapreduce.Job:  map 59% reduce 0%
16/11/15 06:03:13 INFO mapred.LocalJobRunner: map > map
16/11/15 06:03:14 INFO mapreduce.Job:  map 60% reduce 0%
16/11/15 06:03:16 INFO mapred.LocalJobRunner: map > map
16/11/15 06:03:17 INFO mapreduce.Job:  map 62% reduce 0%
16/11/15 06:03:19 INFO mapred.LocalJobRunner: map > map
16/11/15 06:03:20 INFO mapreduce.Job:  map 64% reduce 0%
16/11/15 06:03:22 INFO mapred.LocalJobRunner: map > map
16/11/15 06:03:23 INFO mapreduce.Job:  map 66% reduce 0%
16/11/15 06:03:25 INFO mapred.LocalJobRunner: map > map
16/11/15 06:03:26 INFO mapreduce.Job:  map 68% reduce 0%
16/11/15 06:03:28 INFO mapred.LocalJobRunner: map > map
16/11/15 06:03:29 INFO mapreduce.Job:  map 70% reduce 0%
16/11/15 06:03:31 INFO mapred.LocalJobRunner: map > map
16/11/15 06:03:32 INFO mapreduce.Job:  map 72% reduce 0%
16/11/15 06:03:34 INFO mapred.LocalJobRunner: map > map
16/11/15 06:03:35 INFO mapreduce.Job:  map 74% reduce 0%
16/11/15 06:03:37 INFO mapred.LocalJobRunner: map > map
16/11/15 06:03:38 INFO mapreduce.Job:  map 76% reduce 0%
16/11/15 06:03:40 INFO mapred.LocalJobRunner: map > map
16/11/15 06:03:41 INFO mapreduce.Job:  map 77% reduce 0%
16/11/15 06:03:43 INFO mapred.LocalJobRunner: map > map
16/11/15 06:03:44 INFO mapreduce.Job:  map 79% reduce 0%
16/11/15 06:03:46 INFO mapred.LocalJobRunner: map > map
16/11/15 06:03:47 INFO mapreduce.Job:  map 81% reduce 0%
16/11/15 06:03:49 INFO mapred.LocalJobRunner: map > map
16/11/15 06:03:50 INFO mapreduce.Job:  map 84% reduce 0%
16/11/15 06:03:52 INFO mapred.LocalJobRunner: map > map
16/11/15 06:03:53 INFO mapreduce.Job:  map 86% reduce 0%
16/11/15 06:03:55 INFO mapred.LocalJobRunner: map > map
16/11/15 06:03:56 INFO mapreduce.Job:  map 87% reduce 0%
16/11/15 06:03:58 INFO mapred.LocalJobRunner: map > map
16/11/15 06:03:59 INFO mapreduce.Job:  map 89% reduce 0%
16/11/15 06:04:01 INFO mapred.LocalJobRunner: map > map
16/11/15 06:04:02 INFO mapreduce.Job:  map 90% reduce 0%
16/11/15 06:04:04 INFO mapred.LocalJobRunner: map > map
16/11/15 06:04:05 INFO mapreduce.Job:  map 93% reduce 0%
16/11/15 06:04:07 INFO mapred.LocalJobRunner: map > map
16/11/15 06:04:08 INFO mapreduce.Job:  map 95% reduce 0%
16/11/15 06:04:10 INFO mapred.LocalJobRunner: map > map
16/11/15 06:04:11 INFO mapreduce.Job:  map 97% reduce 0%
16/11/15 06:04:13 INFO mapred.LocalJobRunner: map > map
16/11/15 06:04:14 INFO mapreduce.Job:  map 99% reduce 0%
16/11/15 06:04:15 INFO mapred.LocalJobRunner: map > map
16/11/15 06:04:15 INFO mapred.Task: Task:attempt_local751525010_0001_m_000000_0 is done. And is in the process of committing
16/11/15 06:04:15 INFO mapred.LocalJobRunner: map > map
16/11/15 06:04:15 INFO mapred.Task: Task attempt_local751525010_0001_m_000000_0 is allowed to commit now
16/11/15 06:04:15 INFO output.FileOutputCommitter: Saved output of task 'attempt_local751525010_0001_m_000000_0' to hdfs://ip-172-20-0-4.eu-central-1.compute.internal:8020/user/patelliandrea/teragen_data_10g/_temporary/0/task_local751525010_0001_m_000000

16/11/15 06:04:15 INFO mapred.LocalJobRunner: map
16/11/15 06:04:15 INFO mapred.Task: Task 'attempt_local751525010_0001_m_000000_0' done.
16/11/15 06:04:15 INFO mapred.LocalJobRunner: Finishing task: attempt_local751525010_0001_m_000000_0
16/11/15 06:04:15 INFO mapred.LocalJobRunner: map task executor complete.
16/11/15 06:04:16 INFO mapreduce.Job:  map 100% reduce 0%
16/11/15 06:04:16 INFO mapreduce.Job: Job job_local751525010_0001 completed successfully
16/11/15 06:04:16 INFO mapreduce.Job: Counters: 21
        File System Counters
                FILE: Number of bytes read=276326
                FILE: Number of bytes written=576125
                FILE: Number of read operations=0
                FILE: Number of large read operations=0
                FILE: Number of write operations=0
                HDFS: Number of bytes read=0
                HDFS: Number of bytes written=10737418200
                HDFS: Number of read operations=4
                HDFS: Number of large read operations=0
                HDFS: Number of write operations=3
        Map-Reduce Framework
                Map input records=107374182
                Map output records=107374182
                Input split bytes=83
                Spilled Records=0
                Failed Shuffles=0
                Merged Map outputs=0
                GC time elapsed (ms)=996
                Total committed heap usage (bytes)=148373504
        org.apache.hadoop.examples.terasort.TeraGen$Counters
                CHECKSUM=230593859918397906
        File Input Format Counters
                Bytes Read=0
        File Output Format Counters
                Bytes Written=10737418200

real    2m29.751s
user    2m10.664s
sys     0m9.224s
```

The next step is to run `terasort` and measure performance of the cluster:
```
[patelliandrea@ip-172-20-0-4 ~]$ time hadoop jar /opt/cloudera/parcels/CDH-5.9.0-1.cdh5.9.0.p0.23/jars/hadoop-examples.jar terasort /user/patelliandrea/teragen_data_10g /user/patelliandrea/terasort_data_10g

[...]

16/11/15 07:37:02 INFO mapreduce.Job: Job job_local102906111_0001 completed successfully
16/11/15 07:37:02 INFO mapreduce.Job: Counters: 35
        File System Counters
                FILE: Number of bytes read=33558241465
                FILE: Number of bytes written=1825731321238
                FILE: Number of read operations=0
                FILE: Number of large read operations=0
                FILE: Number of write operations=0
                HDFS: Number of bytes read=1737303104900
                HDFS: Number of bytes written=10737418200
                HDFS: Number of read operations=111388
                HDFS: Number of large read operations=0
                HDFS: Number of write operations=644
        Map-Reduce Framework
                Map input records=107374182
                Map output records=107374182
                Map output bytes=10952166564
                Map output materialized bytes=11166916848
                Input split bytes=54080
                Combine input records=0
                Combine output records=0
                Reduce input groups=107374182
                Reduce shuffle bytes=11166916848
                Reduce input records=107374182
                Reduce output records=107374182
                Spilled Records=319438189
                Shuffled Maps =320
                Failed Shuffles=0
                Merged Map outputs=320
                GC time elapsed (ms)=48988
                Total committed heap usage (bytes)=85594210304
        Shuffle Errors
                BAD_ID=0
                CONNECTION=0
                IO_ERROR=0
                WRONG_LENGTH=0
                WRONG_MAP=0
                WRONG_REDUCE=0
        File Input Format Counters
                Bytes Read=10737418200
        File Output Format Counters
                Bytes Written=10737418200
16/11/15 07:37:02 INFO terasort.TeraSort: done

real    12m40.867s
user    12m23.064s
sys     1m25.913s
```

We can validate the output of the job as well, using `teravalidate`:
```
[patelliandrea@ip-172-20-0-4 ~]$ time hadoop jar /opt/cloudera/parcels/CDH-5.9.0-1.cdh5.9.0.p0.23/jars/hadoop-examples.jar teravalidate /user/patelliandrea/terasort_data_10g /user/patelliandrea/teravalidate_data_10g

[...]

16/11/15 07:40:58 INFO mapreduce.Job:  map 100% reduce 100%
16/11/15 07:40:58 INFO mapreduce.Job: Job job_local926422043_0001 completed successfully
16/11/15 07:40:58 INFO mapreduce.Job: Counters: 35
        File System Counters
                FILE: Number of bytes read=553146
                FILE: Number of bytes written=1155445
                FILE: Number of read operations=0
                FILE: Number of large read operations=0
                FILE: Number of write operations=0
                HDFS: Number of bytes read=21474836400
                HDFS: Number of bytes written=25
                HDFS: Number of read operations=13
                HDFS: Number of large read operations=0
                HDFS: Number of write operations=4
        Map-Reduce Framework
                Map input records=107374182
                Map output records=3
                Map output bytes=83
                Map output materialized bytes=95
                Input split bytes=170
                Combine input records=0
                Combine output records=0
                Reduce input groups=3
                Reduce shuffle bytes=95
                Reduce input records=3
                Reduce output records=1
                Spilled Records=6
                Shuffled Maps =1
                Failed Shuffles=0
                Merged Map outputs=1
                GC time elapsed (ms)=617
                Total committed heap usage (bytes)=533725184
        Shuffle Errors
                BAD_ID=0
                CONNECTION=0
                IO_ERROR=0
                WRONG_LENGTH=0
                WRONG_MAP=0
                WRONG_REDUCE=0
        File Input Format Counters
                Bytes Read=10737418200
        File Output Format Counters
                Bytes Written=25

real    1m30.929s
user    1m15.198s
sys     0m8.849s
```