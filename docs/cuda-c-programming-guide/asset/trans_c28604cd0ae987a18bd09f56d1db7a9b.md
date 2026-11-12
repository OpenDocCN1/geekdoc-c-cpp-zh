

cudaEventSynchronize() 和 cudaEventQuery() 在指定事件后未跟随任何设备工作的情况下；以及与主机完全同步的 cudaMemcpy() 和 cudaMemset() 的用法。

流之间创建的依赖关系将被跟踪，以通过同步流或事件来推断其他流的完成情况。依赖关系可以通过 cudaStreamWaitEvent() 创建，或在使用默认（NULL）流时隐式创建。

CPU 从流回调中访问托管数据是合法的，前提是没有其他可能正在访问托管数据的线程在 GPU 上处于活动状态。此外，未跟随任何设备工作的回调可用于同步：例如，从回调内部发出条件变量信号；否则，CPU 访问仅在回调期间有效。

有几点重要说明：

- GPU 处于活动状态时，CPU 始终可以访问非托管零拷贝数据。

- 当 GPU 正在运行任何内核时，即视为处于活动状态，即使该内核未使用托管数据。如果内核可能使用数据，则访问被禁止，除非设备属性 concurrentManagedAccess 为 1。

- 托管内存的并发跨 GPU 访问没有限制，除了适用于非托管内存的多 GPU 访问限制之外。

- 并发 GPU 内核访问托管数据没有限制。

请注意，最后一点允许 GPU 内核之间出现竞争，这与非托管 GPU 内存的当前情况相同。如前所述，从 GPU 的角度来看，托管内存的功能与非托管内存相同。以下代码示例说明了这些要点：

```
int main() {
cudaStream_t stream1, stream2;
cudaStreamCreate(&stream1);
cudaStreamCreate(&stream2);
int *managed;
cudaMallocManaged(&managed, 4, cudaMemAttachGlobal); // Non-managed, CPU-accessible memory
cudaMallocHost(&managed, 4);
cudaMallocManaged(&managed, 4);
// Point 1: CPU can access non-managed data.
kernel<<< 1, 1, 0, stream1 >>>(managed);
// non-managed data while GPU is busy,
// Point 2: CPU cannot access any managed data while GPU is busy,
// unless concurrentManagedAccess = 1
// Note we have not yet synchronized, so "kernel" is still active.
/* also managed = 2;
// Will issue segmentation fault
// Point 3: Concurrent GPU kernels can access the same data.
kernel<<< 1, 1, 0, stream2 >>>(managed);
// Point 4: Multi-GPU concurrent access is also permitted.
cudaStreamSynchronize();
kernel<<< 1, 1 >>>(managed);
return 0;
}
```

## K.2.2.3. 使用流管理数据可见性和并发 CPU + GPU 访问

此前假设对于 6.x 之前的 SM 架构：1) 任何活动内核都可以使用任何托管内存，2) 在内核活动时从 CPU 使用托管内存是无效的。这里我们介绍一种用于更精细控制托管内存的系统，旨在适用于所有支持托管内存的设备，包括 concurrentManagedAccess 等于 0 的旧架构。

CUDA 编程模型提供流，作为程序指示内核启动之间依赖性和独立性的机制。在同一流中启动的内核保证按顺序执行，而在不同流中启动的内核允许并发执行。流描述工作项之间的独立性，从而允许通过并发实现潜在的更高效率。

统一内存在流独立性模型的基础上，允许 CUDA 程序显式将托管分配与 CUDA 流关联。这样一来，程序员根据内核是否在指定流中启动来指示内核对数据的使用。这使得基于程序特定数据访问模式的并发机会成为可能。用于控制此行为的函数是：

```
cudaError_t cudaStreamAttachMemAsync(cudaStream_t stream,
 void *ptr,
 size_t length=0,
 unsigned int flags=0);
```

cudaStreamAttachMemAsync() 函数将从 ptr 开始的 length 字节内存分配给指定流。（目前，length 必须始终为 0 以指示应附加整个区域。）由于此关联，统一内存系统允许 CPU 访问此内存区域，只要流中的所有操作都已完成，无论其他流是否处于活动状态。实际上，这将活动 GPU 对托管内存区域的独占所有权限制为每流活动，而不是整个 GPU 活动。

最重要的是，如果分配未与特定流关联，则它对所有运行中的内核可见，无论其流如何。这是 cudaMallocManaged() 分配或 __managed__ 变量的默认可见性；因此，简单情况的规则是，在任何内核运行时 CPU 不得触摸数据。

通过将分配与特定流关联，程序保证只有在该流中启动的内核才会触摸该数据。统一内存系统不执行任何错误检查：程序员有责任确保遵守此保证。

除了允许更高的并发性之外，使用 cudaStreamAttachMemAsync() 可以（并且通常会）在统一内存系统中启用数据传输优化，这可能会影响延迟和其他开销。

## K.2.2.4. 流关联示例

将数据与流关联允许对 CPU + GPU 并发性进行精细控制，但在使用计算能力低于 6.x 的设备时，必须牢记哪些数据对哪些流可见。查看先前的同步示例：

```
__device__ __managed__ int x, y=2;
__global__ void kernel() {
    x = 10;
}

int main() {
    cudaStream_t stream1;
    cudaStreamCreate(&stream1);
    cudaStreamAttachMemAsync(stream1, &y, 0, cudaMemAttachHost);
    cudaDeviceSynchronize(); // Wait for Host attachment to occur.
    kernel<<< 1, 1, 0, stream1 >>>(); // Note: Launches into stream1.
    y = 20; // Success - kernel is running but "y"
    // has been associated with no stream.
    return 0;
}
```

这里我们显式将 **y** 与主机可访问性关联，从而使 CPU 随时都能访问。（与之前一样，请注意访问前没有 **cudaDeviceSynchronize()**。）GPU 运行 **kernel** 时对 **y** 的访问现在将产生未定义结果。

请注意，将变量与流关联不会更改任何其他变量的关联。例如，将 **x** 与 **stream1** 关联并不能确保仅由在 **stream1** 中启动的内核访问 **x**，因此此代码会导致错误：

```
__device__ __managed__ int x, y=2;
__global__ void kernel() {
    x = 10;
}

int main() {
    cudaStream_t stream1;
    cudaStreamCreate(&stream1);
    cudaStreamAttachMemAsync(stream1, &x); // Associate "x" with stream1.
    cudaDeviceSynchronize(); // Wait for "x" attachment to occur.
    kernel<<< 1, 1, 0, stream1 >>>(); // Note: Launches into stream1.
    y = 20; // ERROR: "y" is still associated globally with all streams by default
    return 0;
}
```

请注意，访问 **y** 会导致错误，因为尽管 **x** 已与流关联，但我们没有告诉系统谁可以看到 **y**。因此，系统保守地假设 **kernel** 可能会访问它，并阻止 CPU 这样做。

## K.2.2.5. 多线程主机程序中的流附加

**cudaStreamAttachMemAsync()** 的主要用途是使用 CPU 线程启用独立任务并行。通常在这样的程序中，CPU 线程为其生成的所有工作创建自己的流，因为使用 CUDA 的 NULL 流会导致线程之间的依赖关系。

托管数据对任何 GPU 流的默认全局可见性可能使在多线程程序中难以避免 CPU 线程之间的交互。因此，使用函数 **cudaStreamAttachMemAsync()** 将线程的托管分配与该线程自己的流关联，并且在线程生命周期内通常不会更改此关联。

