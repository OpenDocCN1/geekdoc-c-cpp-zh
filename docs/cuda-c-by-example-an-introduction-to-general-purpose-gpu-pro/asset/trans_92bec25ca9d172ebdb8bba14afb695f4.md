

```cpp
// allocate page-locked memory, used to stream
HANDLE_ERROR( cudaHostAlloc( (void**)&host_a,
    FULL_DATA_SIZE * sizeof(int),
    cudaHostAllocDefault ) );
HANDLE_ERROR( cudaHostAlloc( (void**)&host_b,
    FULL_DATA_SIZE * sizeof(int),
    cudaHostAllocDefault ) );
HANDLE_ERROR( cudaHostAlloc( (void**)&host_c,
    FULL_DATA_SIZE * sizeof(int),
    cudaHostAllocDefault ) );
for (int i=0; i<FULL_DATA_SIZE; i++) {
    host_a[i] = rand();
    host_b[i] = rand();
}
```

我们已在 GPU 和主机上分配了输入和输出缓冲区。请注意，我们决定通过使用 cudaHostAlloc() 进行分配来在主机上使用固定内存。使用固定内存有非常充分的理由，而这绝非仅仅因为它能让拷贝更快。我们稍后会详细说明，但我们将使用一种新的 cudaMemcpy() 函数，而这个新函数要求主机内存必须是页锁定的。在分配输入缓冲区后，我们使用 C 库函数 rand() 向主机分配区域填充随机整数。

在创建流和定时事件、分配设备和主机缓冲区后，我们已准备好执行一些计算！通常，我们通过将两个输入缓冲区拷贝到 GPU、启动内核，然后将输出缓冲区拷贝回主机来快速完成这一阶段。我们将再次遵循这一模式，但这次会做一些小的改动。

首先，我们将选择不将输入缓冲区完整地拷贝到 GPU。相反，我们将把输入拆分成较小的块，并对每个块执行三步流程。也就是说，我们将取输入缓冲区的一部分，将其拷贝到 GPU，在该部分缓冲区上执行内核，然后将输出缓冲区的相应部分拷贝回主机。想象一下，我们需要这样做是因为 GPU 的内存远小于主机，因此计算需要分块进行，因为整个缓冲区无法一次性放入 GPU。执行这种“分块化”计算序列的代码如下：

```cpp
// now loop over full data, in bite-sized chunks
for (int i=0; i<FULL_DATA_SIZE; i+=N) {
    // copy the locked memory to the device, async
    HANDLE_ERROR( cudaMemcpyAsync( dev_a, host_a+i,
                                   N * sizeof(int),
                                   cudaMemcpyHostToDevice,
                                   stream ) );
    HANDLE_ERROR( cudaMemcpyAsync( dev_b, host_b+i,
                                   N * sizeof(int),
                                   cudaMemcpyHostToDevice,
                                   stream ) );

    kernel<<<N/256, 256, 0, stream>>>( dev_a, dev_b, dev_c );

    // copy the data from device to locked memory
    HANDLE_ERROR( cudaMemcpyAsync( host_c+i, dev_c,
                                   N * sizeof(int),
                                   cudaMemcpyDeviceToHost,
                                   stream ) );
}
```

但在前面的摘录中，你还会注意到另外两个与常规不同的意外变化。首先，我们不再使用熟悉的 cudaMemcpy()，而是使用一个新的例程 cudaMemcpyAsync() 来将数据拷贝到 GPU 和从 GPU 拷贝数据。这两个函数之间的差异微妙但显著。原始的 cudaMemcpy() 表现得像 C 库函数 memcpy()。具体来说，这个函数是同步执行的，这意味着当函数返回时，拷贝已完成，输出缓冲区现在包含了本应拷贝进去的内容。

*同步* 函数的对立面是 *异步* 函数，这启发了 `cudaMemcpyAsync()` 这一名称。对 `cudaMemcpyAsync()` 的调用只是将一个 *请求* 放入由参数 `stream` 指定的流中，以执行内存拷贝。当调用返回时，不能保证拷贝甚至已经开始，更不用说已经完成了。我们拥有的保证是，拷贝肯定会在同一流中放入的下一个操作之前执行。要求传递给 `cudaMemcpyAsync()` 的任何主机内存指针都必须由 `cudaHostAlloc()` 分配。也就是说，你只允许向页锁定内存或从页锁定内存安排异步拷贝。

请注意，带角括号的内核启动也接受一个可选的 stream 参数。这个内核启动是异步的，就像之前的两个向 GPU 拷贝内存的操作以及之后从 GPU 拷贝回的内存操作一样。从技术上讲，我们可以结束循环的一次迭代，而实际上尚未启动任何内存拷贝或内核执行。如前所述，我们能保证的只是，流中放入的第一个拷贝会在第二个拷贝之前执行。此外，第二个拷贝会在内核启动之前完成，内核会在第三个拷贝启动之前完成。所以，正如我们在本章前面提到的，流就像是 GPU 要执行的工作的有序队列。

当 `for` 循环终止时，GPU 可能仍有大量工作排队等待完成。如果我们想保证 GPU 已完成其计算和内存拷贝，就需要将其与主机同步。也就是说，我们基本上希望主机等待，直到 GPU 完成后再继续。我们通过调用 `cudaStreamSynchronize()` 并指定要等待的流来实现这一点：

```cpp
// copy result chunk from locked to full buffer
HANDLE_ERROR( cudaStreamSynchronize( stream ) );
```

在将流与主机同步后，计算和拷贝已完成，我们可以停止计时器、收集性能数据，并释放输入和输出缓冲区。

```cpp
HANDLE_ERROR( cudaEventRecord( stop, 0 ) );

HANDLE_ERROR( cudaEventSynchronize( stop ) );
HANDLE_ERROR( cudaEventElapsedTime( &elapsedTime,
start, stop ) );
printf( "Time taken:  %3.1f ms\n", elapsedTime );

// cleanup the streams and memory
HANDLE_ERROR( cudaFreeHost( host_a ) );
HANDLE_ERROR( cudaFreeHost( host_b ) );
HANDLE_ERROR( cudaFreeHost( host_c ) );
HANDLE_ERROR( cudaFree( dev_a ) );
HANDLE_ERROR( cudaFree( dev_b ) );
HANDLE_ERROR( cudaFree( dev_c ) );
```

最后，在退出应用程序之前，我们销毁用于排队 GPU 操作的流。

```cpp
HANDLE_ERROR( cudaStreamDestroy( stream ) );
return 0;
}
```

老实说，这个例子很少展示流的强大之处。当然，即使使用单个流，如果我们有希望在 GPU 忙于处理流中塞入的工作时在主机上完成一些工作，也能帮助加速应用程序。但假设主机上没什么可做的，我们仍然可以通过使用流来加速应用程序，在下一节中我们将看看如何实现这一点。

## 10.5 使用多个 CUDA 流

让我们改编自第 10.3 节：使用单个 CUDA 流 的单流示例，使其在两个不同的流中执行工作。在前一个示例开始时，我们检查了设备确实支持重叠，并将计算分成了块。这个改进版应用程序背后的想法很简单，依赖于两点：“分块”计算和内存拷贝与内核执行的重叠。我们力求在流 0 执行其内核的同时，让流 1 将其输入缓冲区拷贝到 GPU。然后，在流 0 将其结果拷贝回主机时，流 1 将执行其内核。接着，在流 0 开始在下一块数据上执行其内核时，流 1 将其结果拷贝回主机。假设我们的内存拷贝和内核执行所需时间大致相同，我们的应用程序执行时间线可能如图 10.1 所示。该图假设 GPU 可以同时执行内存拷贝和内核执行，因此空框表示一个流正在等待执行无法与另一个流的操作重叠的操作的时间。还要注意，本章其余图表中对 cudaMemcpyAsync() 的调用被缩写，简单表示为“memcpy”。

| 流 0 | 流 1 |
| :--- | :--- |
| memcpy A 到 GPU | |
| memcpy B 到 GPU | |
| 内核 | memcpy A 到 GPU |
| | memcpy B 到 GPU |
| | 内核 |
| memcpy C 从 GPU | memcpy C 从 GPU |
| | |
| memcpy A 到 GPU | |
| memcpy B 到 GPU | |
| 内核 | memcpy A 到 GPU |
| | memcpy B 到 GPU |
| | 内核 |
| memcpy C 从 GPU | memcpy C 从 GPU |

图 10.1 使用两个独立流的预期应用程序执行时间线

