
图 6-6 显示了应用程序的时间轴，与图 6-5 类似，但运行无法同时启动，因为 Fermi 设备上的流之间存在伪依赖，这是由共享工作队列引起的。流 `i+1` 什么时候能够与流 `i` 启动最后一个任务的同时启动其第一个任务？由于存在不同的流，它们之间没有依赖关系。当流 `i` 的最后一个任务启动时，CUDA 运行时调度工作队列中的下一个任务，即流 `i+1` 的第一个任务。由于每个流的第一个任务不依赖于任何早期的任务，并且有可用的 SM，它可以立即启动。流 `i+1` 的第二个任务被调度，它对第一个任务的依赖阻止了它再次执行任务执行直到被阻塞。

这种伪依赖是由内核从主机分发的顺序引起的。该应用程序使用了深度优先方法，在启动下一个流之前先启动一个流的全套操作。深度优先方法导致的工作队列中的任务顺序如图 6-7 所示。由于所有流都被复用到单个硬件工作队列中，先前的流会阻塞后续的流。

![](img/506ba3a4c9f4512233692f3f20de1f3a_309_0.png)

图 6-6

为了避免 Fermi GPU 上的依赖，你可以使用广度优先方法以广度优先的方式分发任务：

```
// 以广度优先的方式分发任务
for (int i = 0; i < n_streams; i++)
kernel_1<<<grid, block, 0, streams[i]>>>();
for (int i = 0; i < n_streams; i++)
kernel_2<<<grid, block, 0, streams[i]>>>();
for (int i = 0; i < n_streams; i++)
kernel_3<<<grid, block, 0, streams[i]>>>();
for (int i = 0; i < n_streams; i++)
kernel_4<<<grid, block, 0, streams[i]>>>();
```

主机分发顺序：深度优先

![](img/506ba3a4c9f4512233692f3f20de1f3a_309_1.png)

图 6-7

只有三个流的边缘是独立的。

使用广度优先排序确保了相邻的流是独立的。广度优先排序确保了工作队列中的相邻任务来自不同的流（如图 6-8 所示），因此内核之间没有依赖关系。

（注：由于提供的原文文本存在大量重复和逻辑混乱，上述译文已根据核心语义进行了去重处理，以符合高级文档工程师的标准。）

对于 C-Shell：

```cpp
setenv CUDA_DEVICE_MAX_CONNECTIONS 32
```

该环境变量也可以直接在 C 宿程序中设置：

```cpp
setenv("CUDA_DEVICE_MAX_CONNECTIONS", "32", 1);
```

每个 CUDA 流（`stream`）都映射到单个 CUDA 设备连接。如果流的数量超过了硬件连接数，多个流将共享同一个硬件工作队列，这可能会导致虚假依赖（`false dependencies`）。

为了在支持 Hyper-Q 但硬件连接不足的平台上检查 CUDA 流的行为，请修改 `simpleHyperqDepth` 示例以使用 CUDA 流：

```cpp
#define NSTREAM 8
```

并将 CUDA 设备连接数设置为：

```cpp
// set up max connectionio
char* iname = "CUDA_DEVICE_MAX_CONNECTIONS";
setenv (iname, "4", 1);
```

使用 `nvvp` 在 Kepler GPU 上运行修改后的示例：

```bash
$ nvvp ./simpleHyperqDepth
```

图 6-10 显示了流的执行，但只有四路并发。由于只有四个设备连接，每两个流共享一个队列。使用深度优先（`deep-first`）方法分发内核会导致分配到同一工作队列的两个流之间产生虚假依赖，这与在 Fermi GPU 上使用深度优先顺序观察到的结果相似。

![](img/506ba3a4c9f4512233692f3f20de1f3a_312_0.png)

图 6-10

接下来，使用相同设置检查广度优先（`breadth-first`）方法的行为。如图 6-11 所示，现在八个流都在并行运行。以广度优先顺序分发内核解决了虚假依赖。

![](img/506ba3a4c9f4512233692f3f20de1f3a_313_0.png)

图 6-11

## 限制并发的 GPU 资源

有限的内核资源会限制应用程序中可能的内核并发量。在之前的示例中，启动内核时仅使用一个线程以避免对并发的任何硬件限制。因此，每个内核的执行只需要少量的设备资源。

```cpp
kernel1<<<1, 1, 0, streams[i]>>();
```

在实际应用中，启动的内核通常会创建多个。通常情况下，会创建数百或数千个线程。有了这么多线程，可用的硬件资源成为限制并发的主要要因素，因为它们阻止了合格内核的启动。为了观察这一点，你可以更改 `simpleHyperBread` 中的执行配置，以便每个块使用更多的线程以及每个网格使用更多的块：

```cpp
dim3 block (128);
dim3 grid (32);
```

你还应该将使用的 CUDA 流数量增加到 16：

```cpp
#define NSTREAM 16
```

重新编译后，使用 `nvvp` 检查 Kepler 设备上 `simpleHyperqBread` 的行为：

`$ nvvp ./simpleHyperqBread`

如图 6-12 所示，尽管 CUDA 设备连接数设置为 32，但仅实现了八路并发。由于 GPU 无法为执行所有合格的内核分配足够的资源，并发性受到了限制。

![](img/506ba3a4c9f4512233692f3f20de1f3a_314_0.png)

图 6-12

## 默认流的阻塞行为

为了演示默认流如何阻塞非空流的操作，请修改 `simpleHyperDepth.cu` 中的深度优先分发循环，在默认流中调用 `kernel_3`：

```cpp
// dispatch job with depth first ordering
for (int i = 0; i < n_streams; i++) {
    kernel_1<<<grid, block, 0, streams[i]>>();
    kernel_2<<<grid, block, 0, streams[i]>>();
}
kernel_3<<<grid, block>>>();
kernel_4<<<grid, block, 0, streams[i]>>();
}
```

由于第三个内核在默认流中启动，非空流上的后续操作将一直阻塞，直到默认流完成。图 6-13 显示了使用 `nvvp` 在 K40 上运行该代码的时间线。它显示了内核如何阻塞其他流。

![](img/506ba3a4c9f4512233692f3f20de1f3a_315_0.png)

图 6-13

## 创建流间依赖

理想情况下，流之间不应产生非预期依赖（即虚假依赖）。但在复杂的应用程序中，可以使用事件引入流间依赖，从而阻塞一个流的操作。

假设你希望某个流的工作在所有其他流完成后才开始。可以使用事件来创建流间依赖。首先，使用 `cudaEventTiming` 标志创建用于同步的事件：

```cpp
cudaEvent_t *kernelEvent = (cudaEvent_t*)malloc(n_streams * sizeof(cudaEvent_t));
for (int i = 0; i < n_streams; i++) {
    cudaEventCreateFlags(&kernelEvent[i], cudaEventTiming);
}
```

接下来，使用 `cudaRecord` 创建跟踪每个流完成情况的事件。然后使用 `cudaStreamWait` 强制最后一个流（`streams[n_streams-1]`）等待所有其他流：

```cpp
// dispatch job with depth first
for (int i = 0; i < n_streams; i++) {
    kernel_1<<<grid, block, 0, streams[i]>>();
    kernel_2<<<grid, block, 0, streams[i]>>();
    kernel_3<<<grid, block, 0, streams[i]>>();
    kernel_4<<<grid, block, 0, streams[i]>>();
    cudaEventRecord(kernelEvent[i], streams[i]);
    cudaStreamWait(streams[n_streams-1], kernelEvent[i], 0);
}
```

你可以从 Wrox.com 下载 `simpleHyper.cu` 下载此示例的完整代码。图 6-14 显示了 `nvvp` 时间线。注意，第四个流（`streams[n_streams-1]`）只有在所有其他流完成后才开始其工作。

![](img/506ba3a4c9f4512233692f3f20de1f3a_316_0.png)

```
-terminated=/usr/local/cuda-6.0/bin/mprof
CUDA DEVICE MAX_KERNELS=32
> Using device: Tesla K80 with num_streams 4
> Compute Capability 3.5 hardware with 15 multi-processors
> grid 1 block 1
Measured time for parallel execution = 0.157s
```

图 6-14

## 重叠内核执行与数据传输

在下一节中，你研究了如何在多个流中并发运行多个内核。在本节中，你将学习如何并发运行内核和数据传输。内核与数据传输的重叠的行为与并发内核执行不同，需要不同的考虑因素。

Fermi 和 Kepler GPU 有两个拷贝引擎：一个用于将数据传输到设备，另一个用于从设备传输数据。因此，你最多可以重叠两个数据传输，但前提是它们的方向不同且被分发到不同的流中。否则，数据传输将串行化。

```
cudaMemcpyAsync(&gpuRef[offset],&d_C[offset],iBytes,
cudaMemcpyDeviceToHost, stream[i]);
}
```

由于这些内存拷贝和内核启动相对于主机是异步的，因此整个工作负载分布在各个流（`streams`）中，没有任何阻塞。然而，输入向量、内核计算和输出向量之间的依赖关系通过将数据传输计算放在同一个流中来维护。

此示例还使用了一个阻塞实现来计算基准性能以便对比：

```
sumArrays<<<grid, block>>>(d_A, d_B, d_C, nElem);
```

你可以从 Wrox.com 的文件 `SimpleMultiDepthDepth.cu` 中下载此示例。编译后，使用 `nvvp` 显示内核和拷贝的时间线：

```bash
$ nvvp ./simpleMultiAddDepth
```

图 6-15 显示了 Tesla K40 的典型时间线。它使用了 8 个硬件队列，并使用 4 个 CUDA 流来重叠内核执行与数据传输。流式执行相比于默认流上的阻塞执行，性能提升了接近 40%。图 6-15 显示了以下三种类型的重叠：

- 不同流中的内核相互重叠

- 内核与其他流中的数据传输重叠

- 不同流中且不同方向的数据传输相互重叠

图 6-15 还显示了以下两种类型的阻塞行为：

- 内核被同一流中先前的数据传输阻塞

- 从主机到设备的数据传输被相同方向的传输所阻塞

尽管从主机到设备的数据传输是在四个不同的流中执行的，但从时间显示它们是顺序执行的，因为它们实际上是通过同一个拷贝引擎执行的。

接下来，你可以尝试通过将硬件工作队列的数量减少到 1 个并重新运行来实验对性能的影响。图 6-16 显示了在 Tesla K40 设备上生成的时间线。发现图 6-16（1 个队列）与 8 个队列的图 6-15 之间没有显著差异。每个流只执行一个内核，减少工作队列的数量不会增加虚假依赖，也不会消除现有的（由主机到设备的拷贝引起的）虚假依赖。

在 K40 中减少工作队列的数量会产生与 Fermi GPU 相似的差异：一个工作队列和两个拷贝队列。如果你在 Fermi GPU 上运行测试，你会发现依赖确实存在。这是 Kepler 在 GPU 管理单元（Grid Management Unit）中实现的的工作调度机制的结果。GPU 负责管理和对发送到 GPU 的工作进行排序。GPU 执行的分析有助于减少虚假依赖。

![](img/506ba3a4c9f4512233692f3f20de1f3a_319_0.png)

```text
<terminated>~/usr/local/cuda-6.0/bin/nvprof
> Using Device: 0 Tesla K40c
> Compute Capability 3.5 hardware with 15 multi-processors
> CUDA DEVICE MAX CONNECTIONS = 1
> with streams: 4
> vector size = 262144
> grid (2048, 1) block (128, 1)

Measured timings (throughput):
Memcpy device to host : 0.838792 ms (2.706757 GB/s)
Memcpy device to host : 0.185920 ms (5.639931 GB/s)
Kernel : 0.522958 ms (3.996818 GB/s)
Total : 1.182784 ms (1.901869 GB/s)

Actual results from overlapped data transfers:
overlap with 4 streams : 0.6664512 ms (3.155928 GB/s)
speedup: 39.74%

Arrays match.

FIGURE 6-15

![](img/506ba3a4c9f4512233692f3f20de1f3a_319_1)

```text

<terminated>~/usr/local/cuda-6.0/bin/nvprof

> Using Device: 0 Tesla K40c

> Compute Capability 3.5 hardware with 15 multi-processors

> CUDA DEVICE MAX CONNECTIONS = 1

> with streams: 4

> vector size = 262144

> grid (2048, 1) block (128, 1)

Measured timings (throughput):

Memcpy device to host : 0.838792 ms (2.706757 GB/s)

Memcpy device to host : 0.185920 ms (5.639931 GB/s)

Kernel : 0.522584 ms (3.996744 GB/s)

Total : 1.098816 ms (1.908556 GB/s)

Actual results from overlapped data transfers:

overlap with 4 streams : 0.671104 ms (3.124928 GB/s)

speedup: 38.92%

Arrays match.

FIGURE 6-16```
Kepler 引入了一种新的网格管理和调度系统——网格管理单元（GMU）。GMU 可以暂停新网格的调度，直到它们就绪，为启用动态并行（Dynamic Parallelism）等运行时提供了灵活性。在 Fermi 设备中，网格从流队列传递给 CUDA 调度器。在 Kepler 设备中，网格传递给 GMU，由 GMU 管理并优先处理在 GPU 上执行的网格。GMU 创建多个硬件队列以减少或消除虚假依赖。即使 GMU 被限制为单个队列，流也可以保持工作流水线。

## 使用宽度优先调度重叠

早期的示例表明，Fermi GPU 使用宽度优先方法分发内核时效果最佳。现在我们检查宽度优先排序在重叠数据传输和计算中的影响。以下代码使用宽度优先方法在流之间分发计算和通信：

```cpp
// 启动到设备的异步传输
for (int i = 0; i < NSTREAM; i++) {
    int offset = i * nElem;
    cudaMemcpyAsync(&d_A[offset], &h_A[offset], iBytes, cudaMemcpyHostToDevice, stream[i]);
    cudaMemcpyAsync(&d_B[offset], &h_B[offset], iBytes, cudaMemcpyHostToDevice, stream[i]);
}
```

```cpp
// 在每个流中启动内核
for (int i = 0; i < NSTREAM; i++) {
    int offset = i * nElem;
    sumArrays<<<grid, block, 0, stream[i]>>>(&d_A[offset], d_B[offset], d_C[offset]);
}
```

```cpp
// 从设备启动异步传输
for (int i = 0; i < NSTREAM; i++) {
    int offset = i * nElem;
    cudaMemcpyAsync(&h_C[offset], &d_C[offset], iBytes, cudaMemcpyDeviceToHost, stream[i]);
}
```
