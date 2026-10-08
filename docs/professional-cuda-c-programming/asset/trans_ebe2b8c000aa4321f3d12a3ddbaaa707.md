

```cpp
// 在默认流上记录停止事件
cudaEventRecord(stop);
```

```cpp
// 等待停止事件完成
cudaEventSynchronize(stop);
```

```cpp
// 计算两个事件之间的运行时间
float time;
cudaEventElapsedTime(&time, start, stop);
```

```cpp
// 清理两个事件
cudaEventDestroy(start);
cudaEventDestroy(stop);
```

start 和 stop 事件默认被放置在 NULL 流（默认流）中。在 NULL 流的开始处记录 start 事件的时间戳，在 NULL 流的结束处记录 stop 事件的时间戳。然后使用 `cudaEventElapsedTime` 获取两个事件之间的运行时间。

# 流同步 (Stream Synchronization)

由于非默认流中的所有操作相对于主机线程都是非阻塞的，你会遇到需要将主机端与在流中运行的操作进行同步的情况。

从主机的角度来看，CUDA 操作可以分为两大大类：

- 内存相关操作
- 内核启动 (Kernel launches)

内核启动相对于主机始终是异步的。许多内存操作本质上也是是异步的（例如 `cudaMemcpy`），但 CUDA 运行时也提供了执行内存操作的函数。

正如你所学的，流有两种类型：

- 异步流（非 NULL 流）
- 同步流（NULL/默认流）

非 NULL 流相对于主机是异步流；所有选择执行的操作都不会阻塞主机的执行。相反，隐式声明的 NULL 流相对于主机是同步流。大多数选择在 NULL 流上的操作会导致主机在所有先前的操作上阻塞，主要的异常是内核启动。

非 NULL 流可以进一步归类为以下类型：

- 阻塞流 (Blocking streams)
- 非阻塞流 (Non-blocking streams)

尽管非 NULL 流相对于主机是非阻塞的，但非 NULL 流内部的操作可能会被 NULL 流中的操作阻塞。如果一个非 NULL 流是阻塞流，那么 NULL 流可能会阻塞该非 NULL 流中的操作。如果一个非 NULL 流是非阻塞流，它将不会在 NULL 流的操作上发生阻塞。在接下来的章节中，你将学习如何处理阻塞流和非阻塞流。

# 阻塞与非阻塞流 (Blocking and Non-Blocking Streams)

使用 `cudaStreamCreate` 创建的流是阻塞流，这意味着这些流中的操作执行可以等待 NULL 流中较早的操作完成。NULL 流是一个隐式流，它与相同 CUDA 上下文中所有其他阻塞流同步。通常，当向 NULL 流发送操作时，CUDA 上下文会在启动该操作之前，等待之前发送到所有阻塞流的所有操作。此外，任何发送到阻塞流的操作也会等待 NULL 流中的待处理操作完成后才执行。

例如，以下代码在 `stream_1` 中启动 `kernel_1`，在 NULL 流中启动 `kernel_2`，然后在 `stream_2` 中启动 `kernel_3`：

```cpp
kernel_1<<1, 0, stream_1>>>;
kernel_2<<1, 1>>>;
kernel_3<<1, 0, stream_2>>>;
```

结果行为是：在 `kernel_1` 完成之前，`kernel_2` 不会在 GPU 上开始执行；在 `kernel_2` 完成之前，`kernel_3` 不开始。从内核的角度来看，每个内核启动仍然是异步且非阻塞的。

CUDA 运行时提供了一个函数，允许自定义非 NULL 流相对于 NULL 流的行为：

```cpp
cudaError_t cudaStreamCreateFlags(cudaStream_t* pstream, unsigned int flags);
```

`flags` 参数决定了所创建流的行为。`flags` 的有效值为：
cudaStreamDefault: 默认流创建标记（阻塞）
cudaStreamNonBlocking: 异步流创建标记（非阻塞）

指定 `cudaStreamNonBlocking` 会禁用非 NULL 流相对于 NULL 流的行为。如果上一个示例中的 `stream_1` 和 `stream_2` 是使用 `cudaStreamNonBlocking` 创建的，那么任何内核执行都不会将因为等待其他任何内核的完成而阻塞。

# 隐式同步 (Implicit Synchronization)

CUDA 包含了两种类型的设备-主机同步：显式和隐式。你已经看到了许多执行显式同步的函数，`cudaDeviceSynchronize`、`cudaStreamSynchronize` 和 `cudaEventSynchronize`。这些函数由主机显式调用，以同步设备上的任务执行与主机线程。你手动在应用程序的逻辑点处插入显式同步调用。

你已经看到过隐式同步的示例。例如，`cudaMemcpy` 隐式地同步设备和主机，因为主机应用程序会阻塞直到

```cpp
cudaError_t cudaEventSynchronize(cudaEvent_t event);
cudaError_t cudaEventQuery(cudaEvent_t event);
```

此外，`cudaStreamWait` 提供了一种使用 CUDA 事件引入流间依赖关系的灵活方法：

```cpp
cudaError_t cudaStreamWait(cudaStream_t stream, cudaEvent_t event);
```

`cudaStreamWait` 导致指定的流在执行调用 `cudaStreamWait` 之后队列的任何操作之前，等待指定的事件。该事件可能与同一流关联，也可能与不同的流关联。在后者，此函数执行跨流同步，如图 6-4 所示。在这里，由流 2 发出的等待确保了在流 1 中创建的事件在继续之前得到满足。

![](img/506ba3a4c9f4512233692f3f20de1f3a_305_0.png)

图 6-4

# 可配置事件 (Configurable Events)

CUDA 运行时提供了一种自定义事件行为和属性的方法：

```cpp
cudaError_t cudaEventCreateWithFlags(cudaEvent_t* event, unsigned int flags);
```

有效的标记包括：

- cudaEventDefault
- cudaEventBlockingSync
- cudaEventDisableTiming
- cudaEventInterprocess

标记 `cudaEventBlockingSync` 指定与此事件的同步将阻塞调用。`cudaEventSynchronize` 的默认行为是在事件上进行自旋（spin），使用 CPU 周期不断检查事件状态。设置了 `cudaEventBlockingSync` 后，线程将放弃核心直到事件被满足。虽然这可以通过在可以执行其他用工作时进入睡眠来减少浪费的 CPU 周期或进程切换，但也可能导致事件被满足与调用线程被激活之间产生更长的延迟。

传递 `cudaEventDisableTiming` 表明创建的事件仅用于同步，不需要记录计时数据。移除获取时间戳的开销可以提高 `cudaStreamWaitEvent` 和 `cudaEventQuery` 用的性能。

标记 `cudaEventInterprocess` 表明创建的事件可以用作进程间事件。

# 并发内核执行 (CONCURRENT KERNEL EXECUTION)

现在已经解释了流、事件和同步的概念及 API，是时候使用几个示例进行实验了。第一个示例了如何使用多个流并行运行多个内核。这个简单的示例将演示关于并发内核执行的一些关键问题：

- 使用深度优先或广度优先方法调度
- 调整硬件队列
- 在 Kepler 和 Fermi 设备上避免伪依赖
- 添加非默认流的阻塞行为
- 添加流之间的依赖关系
- 检查资源使用如何影响并发

# 非 NULL 流中的并发内核 (Concurrent Kernels in Non-NULL Streams)

在本节中，你将使用 NVIDIA Visual Profiler nvvp 来可视化内核执行。此示例中的内核包含虚拟计算以模拟设备上的工作。这确保了内核在 GPU 上停留一段时间，以便在 Visual Profiler 中可见。注意，此示例使用了相同的内核 `kernel_1`、`kernel_2` 等：

```cpp
global void kernel_1() {
    double sum = 0.0;
    for (int i = 0; i < N; i++) {
        sum = sum + tan(0.1);
    }
}
```

这样做是为了更容易在 nvvp 中可视化不同内核的执行。
必须首先一组非 NULL 流。这些流的每个内核启动应该在 GPU 上并发运行，只要没有由于硬件资源限制导致的伪依赖。

```cpp
cudaStream_t *streams = (cudaStream_t*)malloc(n_streams * sizeof(cudaStream_t));
for (int i = 0; i < n_streams; i++) {
    cudaStreamCreate(&streams[i]);
}
```

可以使用循环遍历流，在这些流中调度内核：

```cpp
dim3 block(1);
dim3 grid(1);
for (int i = 0; i < n_streams; i++) {
    kernel_1<<<grid, block, 0, streams[i]>>>();
    kernel_2<<<grid, block, 0, streams[i]>>>()();
}
```

