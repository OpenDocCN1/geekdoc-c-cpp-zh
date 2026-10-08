
使用 `nvprof`。首先，使用 `gld_throughput` 指检查内核的内存读取效率，以观察不同执行配置之间的差异：

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

虽然第四种情况具有最高的吞吐量，但它比第二种情况要慢（后者仅展示了一半的吞吐量）。从这一点来看，当你第 4 章学习 GPU 设备内部内存事务的工作原理时，原因就会变得明了。

接下来，使用 `gld_efficiency` 指检查加载效率，它是请求加载吞吐量与所需加载吞吐量的比值。它衡量了应用程序操作使用设备内存带宽的情况。结果总结如下：

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

通过这些结果，你可以解释为什么最后两种情况较高的加载吞吐量和实现的占用率并没有带来性能的提升。尽管最后几种情况执行的加载次数（即吞吐量）更多，但这些加载的有效性（即效率）较低。

注意，最后两种情况的共同特征是，它们在最内层维度的块大小始终线程（warp）大小的倍数。如之前所述，对于网格和块启发式算法，最内层维度应该是线程大小的倍数。第 4 章将讨论半线程线程（half-warp threads）如何影响性能。

# 暴露并行性

你可以从上一个节得出的结论是，块的最内层维度 `{block.x}` 应该是线程大小的倍数。这样加载效率就得到了大幅提升。你可能会好奇：

- 是否可以通过调整 `block.x` 来增加加载吞吐量？
- 是否可以暴露更多的并行性？

既然已经建立了性能基准，可以通过对更广泛的线程配置测试 `sumMatrix` 来回答这些问题：

```
$ ./sumMatrix 64 2
sumMatrixOnGPU2D <<(256,8192), (64,2) >>> elapsed 0.033567 sec
$ ./sumMatrix 64 4
sumMatrixOnGPU2D <<(256,4096), (64,4) >>> elapsed 0.034908 sec
$ ./sumMatrix 64 8
sumMatrixOnGPU2D <<(256,2048), (64,8) >>> elapsed 0.036651 sec
$ ./sumMatrix 128 2
sumMatrixOnGPU2D <<(128,8192), (128,2) >>> elapsed 0.032688 sec
$ ./sumMatrix 128 4
sumMatrixOnGPU2D <<(128,4096), (128,4) >>> elapsed 0.034786 sec
$ ./sumMatrix 128 8
sumMatrixOnGPU2D <<(128,2048), (128,8) >>> elapsed 0.046157 sec
$ ./sumMatrix 256 2
sumMatrixOnGPU2D <<(64,8192), (256,2) >>> elapsed 0.032793 sec
$ ./sumMatrix 256 4
sumMatrixOnGPU2D <<(64,4096), (256,4) >>> elapsed 0.038092 sec
$ ./sumMatrix 256 8
sumMatrixOnGPU2D <<(64,2048), (256,8) >>> elapsed 0.000173 sec
Error: sumMatrix.cu:163, code:9, invalid configuration argument
```

以下是从这些结果中得到的一些观察和结论：

- 最后一次块大小为 (256,8) 的执行是无效的。块中的总线程超过了 1,024，这是该 GPU 的硬件限制。
- 使用块维度为 (128,2) 的第四种情况获得了最佳结果。
- 虽然块维度为 (64,2) 的第一种情况启动了最多的线程块，但它并不是快的连接。
- 因为块配置为 (64,4) 的第二种情况与块数量相同，这两种情况在设备上暴露了相同的并行性。由于此情况的表现逊于 (128,2)，你可以得出线程块的最内层结构对性能起着关键作用。这重复了上一个节的结论。
- 剩余所有情况的线程块都少于最佳情况。此外，更多的并行性是性能优化的重要因素。

你可能会猜线程块最少的报告实现的占用率较低，而线程块最多的示例报告实现的占用率较高。可以通过 `nvprof` 测量 `achieved_occupancy` 指标来验证这一理论：

```
$ nvprof --occupancy ./sumMatrix 64 2
sumMatrixOnGPU2D <<(256,8192), (64,2)>>> Global Occupancy 0.55456
$ nvprof --occupancy ./sumMatrix 64 4
sumMatrixOnGPU2D <<(256,4096), (64,4)>>> Global Occupancy 0.79862
$ nvprof --occupancy ./sumMatrix 64 8
sumMatrixOnGPU2D <<(256,2048), (64,8)>>> Global Occupancy 0.75353
$ nvprof --occupancy ./sumMatrix 128 2
sumMatrixOnGPU2D <<(128,8192), (128,2)>>> Global Occupancy 0.80259
$ nvprof --occupancy ./sumMatrix 128 4
sumMatrixOnGPU2D <<(128,4096), (128,4)>>> Global Occupancy 0.74636
$ nvprof --occupancy ./sumMatrix 128 8
sumMatrixOnGPU2D <<(128,2048), (128,8)>>> Global Occupancy 0.57349
$ nvprof --occupancy ./sumMatrix 256 2
sumMatrixOnGPU2D <<(64,8192), (256,2)>>> Global Occupancy 0.76090
$ nvprof --occupancy ./sumMatrix 256 4
sumMatrixOnGPU2D <<(64,4096), (256,4)>>> Global Occupancy 0.59517
```
