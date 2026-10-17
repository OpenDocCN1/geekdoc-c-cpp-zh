
在这里，`blockId.x` 和 `blockId.y` 被解释为对角坐标。`block_x` 和 `block_y` 是它们对应的笛卡尔坐标。行优先转置核如下使用对角坐标：在核的开始，使用分配给线程块的笛卡尔坐标计算线程索引 `ix, iy`。下面的示例核使用对角坐标来实现合并读写：

```cpp
__global void transposeDiagonalRow(float *out, float *in, int nx, int ny) {
  unsigned int block_x = blockId.x;
  unsigned int block_y = (blockId.x+blockId.y)%gridDim.x;

  unsigned int ix = gridDim.x * block_x + threadIdx.x;
  unsigned int iy = blockDim.y * block_y + threadIdx.y;

  if (ix < nx && iy < ny) {
    out[ix*ny + iy] = in[iy*nx + ix];
  }
}
```

使用对角坐标的列优先版本如下：

```cpp
__global void transposeDiagonalCol(float *out, float *in, int nx, int ny) {
    unsigned int blk_y = blockIdx.x;
    unsigned int blk_x = (blockIdx.x+blockIdx.y)%gridDim.x;

    unsigned int ix = blockDim.x * blk_x + threadIdx.x;
    unsigned int iy = blockDim.y * blk_y + threadIdx.y;

    if (ix < nx && iy < ny) {
        out[iy*nx + ix] = in[ix*ny + iy];
    }
}
```

将以下代码加入核 `switch` 语句中处理这些核：

```cpp
case 6:
    kernel = &transposeDiagonalRow;
    kernelName = "DiagonalRow";
    break;

case 7:
    kernel = &transposeDiagonalCol;
    kernelName = "DiagonalCol";
    break;
```

启用 L1 缓存重新编译代码，并运行以下命令比较这两个新转置核的性能。结果总结在表 4-10。

```
$ ./transpose 6
$ ./transpose 7
```

# 表 4-10：核的有效带宽（启用 L1 缓存）

| 核 (KERNEL) | 带宽 | 峰值带宽比例 |
|---|---|---|
| DiagonalRow: 加载行/存储列 | 73.42 GB/s | 41.32% |
| DiagonalCol: 加载列/存储行 | 75.92 GB/s | 42.72% |

块大小：16x16；矩阵：2,048 x 2,048；有效带宽单位：GB/sec

通过使用对角坐标改变块执行顺序，行优先核的性能显著提高。然而，列优先核在笛卡尔坐标下的表现仍优于对角坐标。对角核的实现可以通过展开块进一步改进，但该实现没有笛卡尔核那样直观。

这种性能提升与 DRAM 的并行访问有关。连续的 256 字节设备内存被分配到连续的分区。当使用笛卡尔坐标将线程块映射到数据块时，全局内存访问可能均匀分布在 DRAM 分区之间，可能会发生分区冲突（partition camping）。在分区冲突中，内存请求会被队列，而其他分区保持空闲。由于对角坐标映射导致了线程块到其处理的数据块之间的非线性映射，步长访问可能进入同一个分区，从而提高了性能。

为了获得最佳性能，所有活跃分片的全局内存并发访问应该分布在分区之间。图 29 展示了使用笛卡尔坐标时的分区冲突。图中假设只有两个分区，这有助于可视化分区冲突。图 30 显示如何避免这种情况。

## 使用窄块暴露并行性

暴露更多并行性的简单方法是调整块大小。之前的章节已经证明了这种技术对提高性能的有效性。详尽块大小的示例总结在表 4-11 中。

# 表 4-11：核的有效带宽（禁用 L1）

| 核 (KERNEL) | 块大小 (BLOCK SIZE) | 带宽 (BANDWIDTH) |
| --- | --- | --- |
| NaiveCol | (32, 32) | 38.13 GB/s |
| NaiveCol | (32, 16) | 51.46 GB/s |
| NaiveCol | (32, 8) | 54.82 GB/s |
| NaiveCol | (16, 32) | 73.42 GB/s |
| NaiveCol | (16, 16) | 80.27 GB/s |
| NaiveCol | (16, 8) | 70.34 GB/s |
| NaiveCol | (8, 32) | 102.76 GB/s |
| NaiveCol | (8, 16) | 82.64 GB/s |
| NaiveCol | (8, 8) | 59.59 GB/s |

矩阵大小：2,048 x 2,048；有效带宽单位：GB/sec：加载列和行的朴素实现核

到目前为止，最佳的块大小是 `(8, 32)`，尽管它像 `(16, 16)` 那样暴露了一些并行性。这种性能提升是由 `(8, 32)` 的“窄”块维度引起的，如图 31 所示。

“窄”块通过增加块内部维度存储的元素数量，改进了存储操作的有效性（如表 4-12 所示）。你可以通过 `nvprof` 测量加载和存储吞吐量来确认这一点。

# 表 4-12：核的有效带宽（启用 L1 缓存）

| 执行配置 (EXECUTION CONFIGURATION) | 加载吞吐量 (LOAD THROUGHPUT) | 存储吞吐量 (STORE THROUGHPUT) |
| --- | --- | --- |
| (16, 16) | 660.89 GB/s | 41.11 GB/s |
| (8, 32) | 406.43 GB/s | 50.80 GB/s |

![](img/506ba3a4c9f4512233692f3f20de1f3a_221_0.png)

![](img/506ba3a4c9f4512233692f3f20de1f3a_221_1.png)

图 4-31

接下来，尝试使用块大小 `(8, 32)` 执行以下命令，以比较不同内核实现之间的带宽。

```
$ ./transpose 0 8 32
$ ./transpose 1 8 32
$ ./transpose 0 8 32
$ ./transpose 3 8 32
$ ./transpose 4 8 32
```

示例结果总结在表 4-13 中。到目前为止，内核 `Unroll4Col` 表现出最佳性能，优于上界拷贝内核。能够达到峰值带宽 60% 到 80% 的有效带宽是一项相当成就。

## 表 4-13：内核的有效带宽（禁用 L1 缓存）

| 内核 | 带宽 | 与峰值带宽的比例 |
| --- | --- | --- |
| 理论峰值带宽 | 177.6 | |
| CopyRow: 使用行加载/存储 | 102.30 | 57.57% |
| NaiveRow: 加载行/存储列 | 95.33 | 53.65% |
| NaiveCol: 加载列/存储行 | 101.99 | 57.39% |
| Unroll4Row: 加载行/存储列 | 82.04 | 46.17% |
| Unroll4Col: 加载列/存储行 | 113.36 | 63.83% |

块大小：8 x 32；矩阵大小：2,048 x 2,048；有效带宽单位：GB/sec

## 使用统一内存进行矩阵加法

你在第 2 章中学习了如何在 GPU 上相加两个矩阵。为了简化独立主机和设备内存空间的管理，并使此 CUDA 程序更具读读且于维护，你可以对使用统一内存的矩阵加法主函数应用以下修订：

- 将主机和设备内存分配替换为托管内存分配，以消除冗余拷贝。
- 移除所有显式内存拷贝。

你可以从声明并分配三个数组开始：`A` 和 `B` 用于输入，`gpuRef` 用于输出：

```cpp
float *A, *gpuRef;
cudaMalloc(void **)&A, int nBytes);
cudaMalloc(void **)&B, int nBytes);
cudaMalloc(void **)&gpuRef, int nBytes);
```

然后，你应该使用管理内存的指针在主机上初始化两个输入矩阵：

```cpp
initialData(A, nxy);
initialData(B, nxy);
```

最后，使用托管内存指针调用矩阵加法：

```cpp
sumMatrixGPU<<grid, block>>>(A, B, gpuRef, nx, ny);
cudaDeviceSynchronize();
```

由于内核启动相对于主机是异步的，且使用托管内存时不再需要对 `cudaMemcpy` 进行阻塞调用，因此你需要在访问内核输出之前在主机端进行显式同步。与本书上一章中的非托管矩阵加法程序相比，得益于统一内存，代码在这里被简化了。

你可以从 `Wrox.com` 下载完整的 `sumMatrixGPU.cu` 代码。你还会找到对应的 `sumMatrixManual.cu`，它使用相同的矩阵加法内核但没有使用托管内存，而是对设备执行显式内存拷贝。两个版本都使用预热内核来避免内核启动开销并获得更准确的时间结果。使用 CUDA 6.0 和 Kepler 或更高版本的 GPU，编译两个版本，分别命名为 `managed` 和 `manual`。

```
$ nvcc -arch=sm_30 sumMatrixGPU.cu -o managed
$ nvcc -arch=sm_30 sumMatrixManual.cu -o manual
```

如果你在使用多个 GPU 进行测试，则托管应用需要额外的步骤。由于托管内存分配对系统中的所有设备都是可见的，你希望限制应用程序可见的设备，以便内存只分配在一个设备上。要做到这一点，请使用 `CUDA_VISIBLE_DEVICES` 环境变量向 CUDA 暴露单个 GPU：

```
$ export CUDA_VISIBLE_DEVICES=0
```

首先，运行托管程序。

```
$ /managed 14
```

在 Kepler K40 上测量的结果如下：

```
$ /managed
Starting using Device 0: Tesla K40m
Matrix size: nx 16384 ny 16384
initialization:
    5.930170 sec
sumMatrix on host:
    0.504063 sec
sumMatrix on gpu:
    0.020253 sec <<<(512,512), (32,32)>>>
```

接下来，运行不使用托管内存的手动程序：

```
$ /manual 14
```

在 Kepler K40 上测量的结果如下：

```
$ /manual
Starting using Device 0: Tesla K40m
Matrix size: nx 16384 ny 16384
initialization:
    1.835069 sec
sumMatrix on host:
    0.474370 sec
sumMatrix on gpu:
    0.020226 sec <<<(512,512), (32,32)>>>
```

这些结果显示，使用托管内存的内核性能几乎与主机和设备之间的显式拷贝一样快，而且编程工作量少得多。

使用 `nvprof` 跟踪两个程序：

```
$ nvprof --profile-api-trace runtime /managed
$ nvprof --profile-api-trace runtime /manual
```

Kepler K40 上的结果总结在表 4-14 中。性能最大的差异在于 CPU 初始化时间——使用托管内存花费的时间长得多。虽然矩阵最初分配在 GPU 上，但它在用初始值初始化时首先在 CPU 上被引用。这要求底层系统在初始化之前将矩阵内容从设备传输到主机，而这种传输在手动版本中并未执行。

当执行主机矩阵矩阵函数时，整个矩阵已经驻留于主机和设备上。接下来，预热内核导致矩阵迁移回设备，以便启动实际的加法内核，此时数据已经在 GPU 上。如果不执行预热内核，使用托管内存运行速度会慢得多。

## 表 4-14：使用托管内存的性能对比

| 运行时函数 | 使用托管内存 | 不使用托管内存 |
|---|---|---|
| 矩阵内核 | 1.6114 | 1.6024 |
| CUDA 内核启动 | 49.259 | 70.717 |
| CUDA 拷贝 HToD | | 37.987 |
| CUDA 拷贝 DToH | | 20.252 |

## 使用统一内存的矩阵加法

| 运行时函数 | 使用托管内存 | 不使用托管内存 |
|---|---|---|
| CPU 数据初始化 | 5930.17 | 1835.07 |
| CPU 矩阵加法 | 504.63 | 474.37 |
| CPU 内核计时 | 25.203 | 20.226 |

矩阵大小：4096 x 4096；单位：毫秒

`nvvp` 和 `nvprof` 都支持检查内存。分析工具允许统一流量。此功能默认关闭。向 `nvprof` 传递以下标志可以启用统一内存指标：

```
$ nvprof --unified-memory-profiling per-device
```

注意，设备到主机传输还会报告 CPU 分页错误。当主机应用程序请求物理内存中不存在的内存地址时，会发生分页错误。当 CPU 需要访问托管内存时，分页错误触发设备到主机的传输。错误数量是相对于数据大小的。尝试使用 256x256 元素的小矩阵运行程序：

结果如下。注意错误数量大幅减少。

| | 计数 | 平均值 | 最大值 |
|---|---|---|---|
| 主机到设备（字节） | 2 | 524288.00 | 0 | 1048576 |
| 设备到主机（字节） | 9 | 505628.44 | 0 | 1572864 |
| CPU 分页错误 | 9 | 123.44 | 0 | 384 |

你还可以使用 `nvv` 可视化地检查内存行为。如下所示对托管内存实现运行 `nvv`：

```
$ nvv /managed
```

在““Executables”选项卡中，在“Arguments”字段中输入 14 以测试大矩阵，并勾选“启用统一内存分析”框，如图 4-32 所示。

图 4-33 描述了托管内存的时间线。你可以从图中看到主机分页错误与数据数据迁移密切相关。统一内存优化

通过将数据迁移到 GPU 来提高性能。底层系统维持主机与设备之间的一致性，并尝试将数据放置在可以访问效率最高的地方。

![](img/506ba3a4c9f4512233692f3f20de1f3a_225_0.png)

图 4-32

![](img/506ba3a4c9f4512233692f3f20de1f3a_225_1.png)

图 4-33

图 4-34 展示了不使用统一内存（Unified Memory）的程序时间线。对比这两幅图，你可以发现显式管理数据移动只产生一次从设备到主机的传输，而统一内存导致了两次。

![](img/506ba3a4c9f4512233692f3f20de1f3a_226_0.png)

图 4-34

随 CUDA 6.0 发布的统一内存版本旨在提高程序员的生产力。底层系统更强调一致性和正确性而非性能。虽然这里的结果表明在 CUDA 应用中手动优化数据移动比统一内存具有性能优势，但你可以确定NVIDIA 计划在未来的硬件和软件发布中增强统一内存的性能和可编程性。

## 总结

CUDA 编程模型的显著特征之一是它直接向程序员暴露 GPU 内存层次结构。对数据移动和放置提供更多控制，可以实现更激进的优化和更高的峰值性能。

全局内存（Global memory）是最大、延迟最高且最常用的内存。对全局内存的请求可以通过 32 字节或 128 字节的事务处理。记住这些特性和粒度对于调优应用程序中的全局内存使用很重要。

通过本章的示例，你学习了提高带宽利用的两个准则：

- 最大化进行中的并发内存访问次数。
- 最大化全局内存与 SM 片内内存之间总线传输字节利用率。

为了保持足够的内存操作在进行中，你可以使用展开（unrolling）技术为每个线程创建更多独立的内存请求，或者调整网格（grid）和块（block）执行配置以向 SM 暴露并行性。

为了避免设备内存与片内内存之间不必要的移动，你的目标应该追求并实现理想的访问模式：对齐且合并（aligned and coalesced）的内存访问。

对齐内存访问相对容易，但有时合并访问可能具有挑战性。某些算法本质上可能使合并访问变得不可实现或极度困难。

在改进合并访问时，你的关注是 warp 内部的内存访问模式。另一方面，在移除分区映射（partition mapping）时，你的关注是所有活动 warp 的模式。对角块协调（Diagonal block coordination）是调整块执行顺序以避免分区冲突（partition camping）的一种方法。

统一内存通过消除指针和消除在主机与设备之间显式传输数据的需要，极大地简化了 CUDA 编程。CUDA 6.0 中统一内存的实现透明地维护了一致性，将其优先级高于性能。未来的硬件和软件增强将提高统一内存的性能。

下一章将涵盖本章简要介绍的话题：常量内存和共享内存。

## 第 4 章练习

- 1. 参考文件 `globalVariable.cu`。声明一个大小为五个元素的静态全局 `float` 数组。用相同值 3.14 初始化全局数组。修改内核，让每个线程更改具有与线程索引相同的数组元素值。让该值乘以五个线程的线程索引。
- 2. 参考文件 `globalVariable.cu`。将以下符号拷贝函数：

```
cudaMemcpyToSymbol()
cudaMemcpyFromSymbol()
```
