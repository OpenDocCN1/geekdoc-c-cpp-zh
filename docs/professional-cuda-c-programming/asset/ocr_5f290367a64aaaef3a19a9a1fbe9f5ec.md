# Checking Active Wraps with nvprof

First, you need to create a reference result as a baseline for performance. To do so, start by testing a set of basic block configurations, in particular, thread blocks of size (32,32), (32,16), (16,32), and (16,16). Recall that sumMatrix accepts the x-dimension of the thread block configuration as its first argument, and the y-dimension of the thread block configuration as its second argument. You can test various block configurations by invoking sumMatrix with the appropriate command line.

The following results are output on the Tesla M2070:

```
$ .sumMatrix 32 32
sumMatrixOGPUD2 << (512,512), (32,32) >>> elapsed 60 ms
$ .sumMatrix 16 32
sumMatrixOGPUD2 << (512,1024), (32,16) >>> elapsed 58 ms
$ .sumMatrix 32 16
sumMatrixOGPUD2 << (1024,512), (16,32) >>> elapsed 51 ms
$ .sumMatrix 16 16
sumMatrixOGPUD2 << (1024,1024), (16,16) >>> elapsed 46 ms
```

Comparing these results, the fastest performance is the first block configuration (32, 32). You may reason that the second configuration has more thread blocks than the first, therefore, exposes more parallelism. This can be confirmed using nvprof and the achieved occupancy metric. The achieved occupancy of a kernel is defined as the ratio of the active warps per cycle to the maximum number of warps supported on SM. The results are summarized below (Note: if you have a system with multiple GPUs, you can direct nvprof to collect information from specific devices by using the --metrics command option):

```
$ nvprof --metrics achieved_occupancy /sumMatrix 32 32
sumMatrixOGPUD2 << (512,512), (32,32) >>> achieved Occupancy 0.501071
$ nvprof --metrics achieved_occupancy /sumMatrix 16 32
sumMatrixOGPUD2 << (512,1024), (32,16) >>> achieved Occupancy 0.736900
$ nvprof --metrics achieved_occupancy /sumMatrix 32 16
sumMatrixOGPUD2 << (1024,512), (16,32) >>> achieved Occupancy 0.766037
$ nvprof --metrics achieved_occupancy /sumMatrix 16 16
sumMatrixOGPUD2 << (1024,1024), (16,16) >>> achieved Occupancy 0.810691
```

From the results you can observe two things:

+   Because the second case has more blocks than the first, it exposed more active warps to the device. This is likely the reason why the second case has higher achieved occupancy and better performance than the first case.

+   The fourth case has the highest achieved occupancy, but it is not the fastest; therefore, higher occupancy does not always equate to performance. There must be other factors that restrict performance.

# Checking Memory Operations with nvprof

There are three memory operations in the sumMatrix kernel (C[idx] = A[idx] + B[idx]): two memory loads and one memory store. The efficiency of these memory operations be checked