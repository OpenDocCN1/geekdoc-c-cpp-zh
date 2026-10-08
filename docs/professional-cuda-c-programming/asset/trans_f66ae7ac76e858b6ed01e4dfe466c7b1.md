
运行时初始化函数用于初始化或清理 OpenACC 状态。表 8-9 描述了运行时初始化函数的子集。如果 OpenACC 应用没有显式调用 `acc_init`，则会在应用程序的第一次 OpenACC 操作时自动执行运行时初始化。

# 表 8-9：OpenACC 运行时 API 中的运行时初始化函数

| 函数声明 | 描述 |
|---|---|
| void acc_init(acc_device_t) | 在提供的类型的设备上初始化 OpenACC 运行时。 |
| void acc_shutdown(acc_device_t) | 从当前指定的指定类型的设备上断开 OpenACC 运行时连接。 |

内存管理函数用于管理加速器内存的分配以及主机与加速器之间的数据传输。在许多情况下，它们重复了 OpenACC 数据指令和子句的功能。表 8-10 描述了内存管理函数的子集。

# 表 8-10：OpenACC 运行时 API 中的内存管理函数

| 函数声明 | 描述 |
|---|---|
| void * acc_malloc(size_t) | 在加速器上分配指定字节数的内存，并返回分配内存的地址 |
| void acc_free(void *) | 释放从指定地址开始的内存 |
| void acc_copyin, acc_present_or_copyin, acc_create, acc_present_or_create, acc_copyout, acc_delete | 这些每个每个都接受 `void*` 作为第一个参数，`size_t` 作为第二个参数。它们以相同的名称实现相同的操作，从第一个参数指定的主机地址开始，使用第二个参数指定的字节数执行操作 |
| int acc_is_present(void*, size_t) | 检查从提供的地址开始且长度指定的内存是否已复制到加速器 |

# 结合 OpenACC 和 CUDA 库

虽然 CUDA 和 OpenACC 是独立的编程模型，但它们可以在同一个应用程序中使用。这样做需要更改应用程序编译的方式。必须使用 `deviceptr` 类在 CUDA 和 OpenACC 之间共享数据。本节将演示一个在单个源文件中一起使用 CUDA 库和 OpenACC 的示例应用程序。示例程序可以从 Wrox.com 的 `cuda-openacc.cu` 下载。

`cuda-openacc.cu` 可以分为以下步骤：

- 1. 使用 `cudaMalloc` 在设备上分配矩阵，并使用 `curandCreateGenerator` 和 `cublasCreate` 为 cuRAND 和 cuBLAS 库创建句柄。
- 2. 使用 cuRAND 库的 `curandGenerateUniform` 函数为设备内存中的输入矩阵填充随机数据。
- 3. 使用 OpenACC 指令在 GPU 上并行执行矩阵乘法。
- 4. 使用 `cublasSasum` 通过对每行以及跨行求和来计算输出矩阵中所有元素的和。
- 5. 使用 `cudaFree` 释放设备内存。

使用 PGI OpenACC 编译器构建 `cuda-openacc.cu`，请使用以下命令：

```
$ pgcc -acc openacc.cu -o cuda-openacc -Minfo=accel \
-L$CUDA_HOME/lib64 -lcurand -lcublas -lcudart
```

注意，这里使用了 C++ 编译器 `pgcc` 以兼容 CUDA 库。保留了相同的参数以启用 OpenACC 支持，并使用 `-Minfo=accel` 显示关于 OpenACC 计算区域并行化的诊断信息。此外，还将 CUDA 库路径添加到编译器的路径中，以便找到 cuRAND、cuBLAS 和 CUDA 运行时函数的定义。该命令的输出如下：

```
main:
70, Accelerator kernel generated
70, #pragma accel loop gang blockIdx.x */ /
72, #pragma accel loop vector(32), worker(4) /* threadIdx.x threadIdx.x
```
（注：由于原文示例输出部分存在乱码或重复字符，此处保持了逻辑结构）

（注：原文后续文本部分存在大量单词重复和逻辑混乱，翻译已根据语意进行对齐）
