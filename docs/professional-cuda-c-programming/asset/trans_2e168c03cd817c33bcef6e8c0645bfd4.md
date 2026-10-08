

![](img/506ba3a4c9f4512233692f3f20de1f3a_374_0.png)

![](img/506ba3a4c9f4512233692f3f20de1f3a_374_1.png)

![](img/506ba3a4c9f4512233692f3f20de1f3a_374_2.png)

![](img/506ba3a4c9f4512233692f3f20de1f3a_374_3.png)

![](img/506ba3a4c9f4512233692f3f20de1f3a_374_4.png)

图 8-9

## 使用 cuFFT API

cuFFT 用于指代两个独立的库：核心高性能 cuFFT 库和可移植库 cuFFTW。cuFFT 库是 CUDA 上的 FFT 实现，并提供它自己的 API。而 cuFFTW 设计时与标准的 FFTW（西方最快速傅里叶变换）主机库具有相同的 API。类似于 cuBLAS 与 BLAS 库共享 API 的方式，cuFFT 的设计目的是最大程度地提高使用 FFTW 的现有代码的可移植性。FFT 库中的大量函数在 cuFFTW 中都得到了相同的支持。cuFFT 假设所有输入都通过句柄（handles）传递，并管理所有的分配（`cudaMalloc`）和传输（`cudaMempy`）。尽管可能会导致性能并非最优，但它极大加速了移植过程。有关 cuFFTW 和 cuFFT 支持的操作完整列表，请参阅 cuFFT 用户指南。

cuFFT 库的配置是通过 FFT 计划（plans）完成的，这是 cuFFT 用来指代其句柄的术语。一个计划定义了要执行的单次变换操作。cuFFT 使用计划来推导出执行请求变换所需的内部内存分配、传输和内核启动。可以使用不同的计划创建方式来生成复杂度和维度不断增加的计划：

```c
cuffResult cuftPlan1d(cuffHandle *plan, int nx, cufftType type, int batch);
cuffResult cuftPlan2d(cuffHandle *plan, int nx, int ny, cufftType type);
cuffResult cuftPlan3d(cuffHandle *plan, int nx, int ny, int nz, cufftType type);
```

cuFFT 还支持多种输入和输出类型，包括：

- 复数到复数（Complex-to-complex）
- 实数到复数（Real-to-complex）
- 复数到实数（Complex-to-real）

对于许多现实应用，最有用的类型是实数到复数，它允许你将来自真实系统的实值测量值输入 cuFFT。

一旦配置了 cuFFT 计划，就可以使用 `cufftExec*` 函数调用（例如 `cufftExec2c`）。通常情况下，函数调用的输入包括计划、输入存储的位置、输出的位置，以及这是正向 FFT（从时域到频域）还是逆向 FFT（从频域到时域）。

## 演示 cuFFT

本节介绍一个使用 cuFFT API 执行复数到复数 1D FFT 的简单示例。你可以从 Wrox.com 下载 `cufft.cu` 示例代码，或者按照下面的代码段进行操作：

```c
// 设置 cuFFT 计划
cuffPlan1d(&plan, N, CUFFT_C2C, 1);

// 分配设备内存
cudaMalloc(void **)&complexSamples, sizeof(cuffComplex) * N);

// 将输入传输到设备内存
cudaMemcpy(dComplexSamples, complexSamples, sizeof(cuffComplex) * N, cudaMemcpyHostToDevice);

// 执行复数到复数的 1D FFT
cufftExec2c(plan, dComplexSamples, dComplexSamples, CUFFT_FORWARD);

// 将结果检索到主机内存
cudaMemcpy(complexFreq, dComplexSamples, sizeof(cuffComplex) * N, cudaMemcpyDeviceToHost);
```

cuFFT 应用的工作流取决于变换的复杂度。在最基础层面，工作流包括：

1. 创建并配置 cuFFT 计划。
2. 使用 `cudaMalloc` 分配设备内存以存储来自 cuFFT 的输入和输出频率。注意，该内存必须类型化以支持你正在执行的变换类型（例如复数到复数、实数到复数、复数到实数）。你可以使用同一块设备内存作为输入和输出进行原地变换。
3. 使用 `cudaMempy` 用输入信号样本填充设备内存。
4. 使用 `cufftExec*` 函数执行计划。
5. 使用 `cudaMempy` 从设备内存中检索结果。
6. 使用 `cudaFree` 和 `cufftDestroy` 释放 CUDA 和 cuFFT 资源。

该示例可以使用以下命令构建：

```bash
$ nvcc -lcusufft cufft.cu -o cufft
```

`cufft.cu` 提供的示例从 `cos(x)` 函数生成输入样本序列，将其转换为复数，将复数表示传输到 GPU，并在复制结果之前执行一个复数到复数的 1D 计划。注意，同一个内存地址 `dComplexSamples` 同时被传递给 `cufftExec2C` 输入和输出范围，这是一个原地 FFT 操作。也可以预分配一个单独的输出缓冲区来存储输出。

## cuFFT 总结

本节简要描述了 cuFFT 库加速许多使用 FFT 应用的能力。在下一节中，我们将查看一个生成随机数的 CUDA 库，它有两个 API：一个用于从主机创建随机数，另一个直接在设备上创建随机数。

## cuRAND 库

随机数生成是许多科学、加密和金融应用的关键部分。随机数生成器（RNG）是一个不接受参数的函数 $f$，但在每次调用时返回值序列中的下一个值。你可以将其想象为一个遍历填充了随机值的数组的指针，如图 8-10 所示。

| 3 | 6 | 8 | 3 | 10 | 88 | 4 |

图 8-10

cuRAND 提供了一个基于 CUDA 的库，用于快速生成准随机和伪随机数。

## 选择伪随机数或准随机数

要理解的最重要的概念是不存在真正的随机性。因为计算机是确定性的，它们只能产生伪随机数。伪随机数生成器（PRNG）使用一种算法，其中每个值在范围内的任何位置出现的概率相等。对于从整数 PRNG 中检索值，返回值为 1 的概率与返回值为 2 或 3 的概率相同，一直到 `INT_MAX`。这对于 PRNG 的每一个值都是如此。这意味着仅仅因为上一次检索到的值是 2，并不意味着下一个值的概率会更低。换句话说，伪随机序列的每次采样都是独立的统计事件，并且不会影响未来采样观测到的值。

这对于准随机生成器（QRNG）来说是不成立的。QRNG 试图均匀地填充类型范围；如果上一次使用的值是 2，那么下次值为 2 的概率实际上降低了。QRNG 序列的采样在统计上是不独立的。

## cuRAND 库概览

cuRAND 库可用于从伪随机和准随机序列中采样。它在本文讨论的 CUDA 库中是独特的，因为它既有主机 API 也有设备 API。这意味着它可以直接从主机代码和内核代码中调用。cuRAND 库暴露的许多概念在两个 API 之间共享，但在使用设备 API 时会增加一些选项。

