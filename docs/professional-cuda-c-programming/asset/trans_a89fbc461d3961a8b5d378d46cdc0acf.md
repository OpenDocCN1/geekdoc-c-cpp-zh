
以下是 nvcc 编译器输出的消息：

```
ptxas info      : 0 bytes cem, 20 bytes cem[2]
ptxas info      : Compiling entry function '_Z8kernel_waveletPffii' for 'sm_20'
ptxas info      : Function properties for '_Z8kernel_waveletPffii'
ptxas info      : Use 6 registers, 8 bytes cem[0]
ptxas info      : Compiling entry function '_Z8kernel_2dfpSiii' for 'sm_20'
ptxas info      : Function properties for '_Z8kernel_2dfpSiii'
cem[16]         : Used 26 registers, 160 bytes cem, 60 bytes cem[0], 8 bytes
```

![](img/506ba3a4c9f4512233692f3f20de1f3a_435_0.png)

图 9-8

输出的最后一行表示内核 `kernel_2dfp` 每个线程使用了 26 个寄存器、共享内存以及一定量的常量内存（用于存储内核参数）。

![](img/506ba3a4c9f4512233692f3f20de1f3a_436_0.png)

# 跨 GPU 集群扩展应用程序

与架构同构的系统相比，GPU 加速集群因对计算密集型应用提供巨大的性能提升和功耗降低而闻名。在处理大型数据集时，你通常需要多个计算节点来高效处理问题。MPI（消息传递接口）是一种标准化且可移植的 API，用于通过消息在分布式进程之间进行通信。在大多数 MPI 实现中，直接从 C 或其他语言调用库函数。

MPI 与 CUDA 完全兼容。有两种类型的 MPI 实现支持在不同节点的 GPU 之间移动数据：传统型 MPI 和 CUDA 感知型 MPI。对于传统 MPI，在可以使用 MPI 将数据通信到另一个节点之前，必须先使用 CUDA API 将将主机内存的内容拷贝回主机内存。对于 CUDA 感知型 MPI，你可以直接将 GPU 内存传递给 MPI 函数，而无需通过主机内存对数据进行缓冲。

目前有多种商用和开源的 CUDA 感知型 MPI 实现，例如：

- MVAPICH2 2.0rc2 (http://mvapich.cse.ohio-state.edu/download/mvapich2/)
- MVAPICH2-GDR 2.0b (http://mvapich.cse.ohio-state.edu/download/mvapich2gdr/)
- OpenMPI 1.7 (http://www.open-mpi.org/software/ompi/v1.7/)
- CRAY MPI (MPT 5.6.2)
- IBM MPI Flat (8.3)

MVAPICH2 是一种开源 MPI 实现，旨在利用 Infiniband 网络特性，为基于 MPI 的应用程序提供高性能和可扩展性。它存在两个版本：MVAPICH2 是 CUDA 感知型 MPI 实现，而 MVAPICH2-GDR 是一个扩展，还支持通过 Infiniband 进行 GPUDirect RDMA（本章稍后将介绍更多关于 GPUDirect 的内容）。

MVAPICH2 是广泛用于 Infiniband 集群的开源 MPI 库，支持从一个 GPU 的设备内存到另一个 GPU 直接 MPI 通信。接下来的章节将使用 MVAPICH2 平台测试以下用：

- 使用 MVAPICH2 在 Infiniband 上进行 CPU 到 CPU 数据传输
- 使用传统 MPI 在 Infiniband 上进行 GPU 到 GPU 数据传输
- 使用 CUDA 感知型 MPI 在 Infiniband 上进行 GPU 到 GPU 数据传输
- 使用 MVAPICH2-GDR 和 GPUDirect RDMA 在 Infiniband 上进行 GPU 到 GPU 数据传输

# CPU 到 CPU 数据传输

为了建立比较基准，你可以使用 MVAPICH2 测试集群中两个 CPU 节点之间互连上数据传输的带宽和延迟。通常情况下，MPI 程序包含四个步骤：

1. 初始化 MPI 环境。
2. 使用阻塞或非阻塞 MPI 函数在不同节点的进程之间传递消息。
3. 跨节点同步。
4. 清理 MPI 环境。

# 实现节点间 MPI 通信

以下代码段展示了一个单 MPI 程序的骨架，该程序在所有节点同步并退出之前发送并接收单条消息。

```c
int main(int argc, char *argv[]) {
    // 初始化 MPI 环境
    int rank, nprocs;
    MPI_Comm_size(MPI_COMM_WORLD, &nprocs);
    MPI_Comm_rank(MPI_COMM_WORLD, &rank);

    // 使用 MPI 调用传输消息
    MPI_Send(sbuf, size, MPI_CHAR, 100, MPI_COMM_WORLD);
    MPI_Recv(rbuf, size, MPI_CHAR, 0, 100, MPI_COMM_WORLD, &reqstat);

    // 跨节点同步
    MPI_Barrier(MPI_COMM_WORLD);

    // 清理 MPI 环境
    MPI_Finalize();

    return EXIT_SUCCESS;
}
```

要测试两个节点之间的带宽和延迟，你首先需要分配 `myBUFSIZE` 数组作为接收缓冲区，如下：

```c
char *sbuf, *rbuf;
sbuf = (char *)malloc(myBUFSIZE);
rbuf = (char *)malloc(myBUFSIZE);
```

然后，可以使用非阻塞发送和接收执行两个节点之间的双向数据传输：

```c
// 如果是第一个进程
if(rank == 0) {
    // 重复执行
    for (int i = 0; i < nRepeat; i++) {
        // 异步从 other_proc 接收字节
        MPI_Irecv(rbuf, size, MPI_CHAR, other_proc, 10, MPI_COMM_WORLD, &reqstat);
        // 从 sbuf 异步发送字节到 other_proc
        MPI_Isend(sbuf, size, MPI_CHAR, other_proc, 100, MPI_COMM_WORLD, &reqstat);
    }
    // 等待发送
    MPI_Waitall(1, &send_request);
    // 等待接收
    MPI_Waitall(1, &reqstat);
} else if (rank == 1) {
  for (int i = 0; i < nRepeat; i++) {
    // 从 other_proc 异步接收字节到 rbuf
    MPI_Irecv(rbuf, size, MPI_CHAR, other_proc, 100, MPI_COMM_WORLD, &reqstat);
    // 从 sbuf 异步发送字节到 other_proc
    MPI_Isend(sbuf, size, MPI_CHAR, other_proc, 10, MPI_COMM_WORLD, &reqstat);
    }
    // 等待发送
    MPI_Waitall(1, &send_request);
    // 等待接收
    MPI_Waitall(1, &reqstat);
  }
}
```

为了获得准确的性能，发送和接收操作将重复 `nRepeat` 次，并报告结果的平均值。你可以下载 `simple2c.c` 并运行以下命令：

```bash
$ mpicc -std=c99 -O3 simple2c.c -o simple2c
```

如果有可用集群，可以在两个节点上运行 MPI 程序。指定两个节点的主名（例如 node01 和 node02，取决于你的集群配置），并运行命令：

```bash
$ mpirun -np 2 -host node01,node02 ./simple2c
```

示例输出如下：

| size | 耗时 | 性能 |
| :--- | :--- | :--- |
| 1 KB | 3.96 µs | 258.27 MB/sec |
| 4 KB | 3.75 µs | 1092.17 MB/sec |
| 16 KB | 8.77 µs | 1867.12 MB/sec |
| 64 KB | 20.18 µs | 3247.61 MB/sec |
| 256 KB | 49.48 µs | 5297.96 MB/sec |
| 1 MB | 169.99 µs | 6168.63 MB/sec |
| 4 MB | 662.81 µs | 6328.06 MB/sec |

`mpun_rsh` 是 MVAPICH2 提供的一个启动工具。你可以使用 `mpirun` 运行任务：

```bash
$ mpirun -np 2 -host node01,node02 ./simple2c
```

# CPU 亲和性

当多个进程或线程在多核上同时需要 CPU 时间时（例如在 MPI 程序中），操作系统负责将线程和进程分配到 CPU 核心。根据操作系统的决定，进程或线程可能会被暂停并移动到新核心。这种行为会导致数据局部性差，从而影响性能。如果进程被切换到新的 CPU 核心，该进程的没有任何数据存储在新核心的缓存中。该进程将必须从系统内存重新获取。因此，将进程或线程绑定到单个 CPU 核心（或一组相邻的 CPU 核心）有助于主机性能。

将进程或线程执行限制在某些 CPU 核心上称为 CPU 亲和性。有多种方法可以将进程和线程绑定到处理器。一旦设置了亲和性，操作系统调度程序必须遵守约束，进程仅在指定的处理器上运行。

CPU 亲和性直接影响 MPI 运行的性能。MVAPICH2 提供了一种使用 `MV2_ENABLE_AFFINITY` 环境变量在运行时设置 CPU 亲和性的方法。你可以在调用 MPI 进程时如下启用 CPU 亲和性：

```bash
$ mpirun -np 2 node01 node02 MV2_ENABLE_AFFINITY=1 /simple2c
```

你可以如下禁用 CPU 亲和性：

```bash
$ mpirun -np 2 node01 node02 MV2_ENABLE_AFFINITY=0 /simple2c
```

对于单线程或单进程应用，启用 CPU 亲和性通过防止操作系统移动进程或线程到处理器，可以提供相同或更好的性能。相反，多线程和多进程应用在禁用 CPU 亲和性时可能会获得性能提升。

# 使用传统 MPI 进行 GPU 到 GPU 数据传输

本节将研究使用传统 MPI 与 CUDA 交换独立节点 GPU 之间的数据。

考虑一个每个节点具有多个 GPU 的多节点集群计算。节点内 GPU 之间的数据交换可以使用上一章“点对点通信”描述的点对点访问或传输来实现。然而，不同节点 GPU 之间的数据交换需要节点间通信库，例如 MPI。为了简化 GPU 之间的数据交换并提高性能，你应该将 MPI 进程绑定到每个 GPU。

# MPI-CUDA 程序中的亲和性

就像将 MPI 进程绑定到 CPU 核心称为 CPU 亲和性一样，将 MPI 进程绑定到特定 GPU 称为 GPU 亲和性。将 MPI 进程绑定到 GPU 通常在通过 `MPI_Init` 初始化 MPI 环境之前完成。

为了在节点内均匀分布进程，你首先必须验证 MPI 库提供的环境变量，以确定进程在节点中的本地 ID。例如，MVAPICH2 保证环境变量 `MV2_COMM_WORLD_LOCAL_RANK` 为每个 MPI 进程设置，`MV2_COMM_WORLD_LOCAL_RANK` 是唯一标识相同节点内进程的整数。其他 MPI 实现提供类似的支持。此本地 ID 或秩可将 MPI 进程绑定到 CUDA 设备：

```c
int node_devices;
int local_rank = atoi(getenv("MV2_COMM_WORLD_LOCAL_RANK"));
```
