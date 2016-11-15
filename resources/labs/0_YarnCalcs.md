## YarnCalcs
Inserted values:
```
Worker vcores		20
Worker splindles	12
Worker RAM			128
Workload factor		1
Worker nodes		10
```

The workload factor represents the maximum number of map and reduce jobs to run in a node. So with a workload factor of 1, only 1 map and only 1 reduce task will be executed per-node, while with a workload factor of 2, a maximum of 2 maps and 2 reduce tasks will be executed per-node as well as if set to 4 (maximum of 4 map and reduce tasks per-node).

Setting the workload factor to 2 or 4 brings to the same result of maximum mapreduce tasks that will be executed on the cluster (15) since the allocated vcores for yarn is set to 15.