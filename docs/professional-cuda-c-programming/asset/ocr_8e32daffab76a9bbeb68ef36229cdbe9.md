```
$ nvprof --metrics achieved_occupancy /sumMatrix 128 8
sumMatrixOnGPUDD<<(128,2048), (128,8)>> Achieved Occupancy 0.573449
$ nvprof --metrics achieved_occupancy /sumMatrix 256 2
sumMatrixOnGPUDD<<(64,8192), (256,2)>> Achieved Occupancy 0.760901
$ nvprof --metrics achieved_occupancy /sumMatrix 256 4
sumMatrixOnGPUDD<<(64,4096), (256,4)>> Achieved Occupancy 0.595197
```

You might be surprised that the first case (64, 2) has the lowest achieved occupancy among all cases, yet it has the most thread blocks. This case is encountering hardware limits on the maximum number of thread blocks.

The fourth (128, 2) and seventh (256, 2) cases, the two highest performing configurations, nearly identical achieved occupancy. It might be interesting to observe how performance is affected if you expose more inter-block parallelism by setting block.y to 1. This reduces the size of each thread block, causing more thread blocks to be loaded to process the same amount of data. Data produces the following results:

```
$ /sumMatrix 128 1
sumMatrixOnGPUDD<<(128,16384), (128,1)>> elapsed 0.032062 sec
$ /sumMatrix 256 1
sumMatrixOnGPUDD<<(64,16384), (256,1)>> elapsed 0.030959 sec
```

These configurations produce the best performance so far. In particular, a block configuration of (256, 1) outperforms (128, 1). You can check achieved occupancy, load throughput, and load efficiency with the following commands:

```
$ nvprof --metrics achieved_occupancy /sumMatrix 256 1
$ nvprof --metrics gid_throughput /sumMatrix 256 1
$ nvprof --metrics gid_efficiency /sumMatrix 256 1
```

The following results are reported:

| Achieved Occupancy | 0.808622 |
| Global Load Throughput | 69.762GB/s |
| Global Memory Load Efficiency | 100.00% |

Note that the best execution configuration you found has neither the highest achieved occupancy nor the lowest load throughput recorded. From these tests, you can conclude that no single metric is directly equivalent to improved performance. You need to look for a good balance of related metrics to reach the best overall performance.

![](bbox=[0.195, 0.735, 0.855, 0.93])