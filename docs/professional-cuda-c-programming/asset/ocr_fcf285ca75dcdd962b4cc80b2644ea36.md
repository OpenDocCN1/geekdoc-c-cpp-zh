using nvprof. First, check the memory read efficiency of the kernel using the gld_throughput metric to observe the differences for each execution configuration:

```
$ nvprof --metrics gld_throughput/sumMatrix 32 32
sumMatrixOnGPU<<< (512,512), (32,32)>>> Global Load Throughput 35.908GB/s
$ nvprof --metrics gld_throughput/sumMatrix 32 16
sumMatrixOnGPU<<< (512,512), (32,16)>>> Global Load Throughput 56.478GB/s
$ nvprof --metrics gld_throughput/sumMatrix 16 32
sumMatrixOnGPU<<< (1024,512), (16,32)>>> Global Load Throughput 81.195GB/s
$ nvprof --metrics gld_throughput/sumMatrix 16 16
sumMatrixOnGPU<<< (1024,1024), (16,16)>>> Global Load Throughput 94.708GB/s
```

While the fourth case has the highest load throughput, it is slower than the second case (which only demonstrates half the load throughput). From this, the reason will be clear when you learn how memory transactions work inside the GPU device in 4.

Next, check the load efficiency using the gld_efficiency_metric, which is the ratio of requested load throughput to required load throughput. It measures how the application's operations use device memory bandwidth. The results are summarized below:

```
$ nvprof --metrics gld_efficiency,/sumMatrix 32 32
sumMatrixOnGPU<<< (512,512), (32,32)>>> Global Memory Efficiency 100.00%
$ nvprof --metrics gld_efficiency/sumMatrix 32 16
sumMatrixOnGPU<<< (512,512), (32,16)>>> Global Memory Efficiency 100.00%
$ nvprof --metrics gld_efficiency/sumMatrix 16 32
sumMatrixOnGPU<<< (1024,512), (16,32)>>> Global Memory Efficiency 49.96%
$ nvprof --metrics gld_efficiency/sumMatrix 16 16
sumMatrixOnGPU<<< (1024,1024), (16,16)>>> Global Memory Efficiency 49.80%
```

From these results, you can explain why the higher load throughput and achieved occupancy of the last two cases did not yield improved performance. Even though the number of loads being performed (that is, throughput) is greater for the last cases, the effectiveness of those loads (that is, efficiency) is lower.

Note that the common feature for the last two cases is that their block size in the innermost dimension is always a multiple of the warp size. As stated earlier, for grid and block heuristics the innermost dimension should always be a multiple of the warp size. Chapter 4 will discuss half-warp threads impact performance.

# Exposing Parallelism

One conclusion you can draw from the previous section is that the innermost dimension of a block {block.x} should be a multiple of warp size. So drastically improved load efficiency. You might be curious:

+   - Is it possible to increase the load throughput by adjusting block.x?
- Is it possible to expose more parallelism?