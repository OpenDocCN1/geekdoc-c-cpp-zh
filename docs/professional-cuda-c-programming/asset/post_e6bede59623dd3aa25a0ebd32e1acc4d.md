
```
cudaMemcpyAsync(&gpuRef[offset],&d_C[offset],iBytes,
cudaMemcpyDeviceToHost, stream[i]);
}
```

Because these memory copies and kernel launches are asynchronous with respect to the host, the full workload is distributed among streams without any blocking. However, dependencies between input vectors, the kernel computation, and the output vector are maintained by placing data transfer computation on the same stream.

This example also uses a blocking implementation to calculate a baseline performance for comparison:

```
sumArrays<<<grid, block>>>(d_A, d_B, d_C, nElem);
```

You can download this example in the file SimpleMultiDepthDepth.cu from Wrox.com. After compiling, use nvvp to display the timeline of kernels and copies:

```bash
$ nvvp ./simpleMultiAddDepth
```

Figure 6-15 shows a typical timeline for Tesla K40. Eight hardware queues are used, and four CUDA streams are used to overlap kernel execution with data transfer. Streamed execution reaches nearly a 40 percent performance improvement over blocking execution on the default stream. Figure 6-15 shows the following three types of overlap:

- Kernels in different streams overlapping with each other
- Kernels overlapping with data transfers in other streams
- Data transfers in different streams and in different directions overlapping with each other

Figure 6-15 also shows the following two types of blocking behavior:

- A kernel blocked by preceding data transfers in the same stream
- Data transfers from the host to the device blocked by a transfer of the same direction

Though data transfers from the host to the device are executed in four different streams, the time show that they are executed sequentially because they are actually executed through the same copy engine.

Next, you can try experimenting with performance by reducing the number of hardware work queues to one and rerunning. Figure 6-16 shows the timeline generated on the Tesla K40 device. that there is no significant difference between Figure 6-16 (with one queue) and 6-15 with eight queues). Each stream only executes a single kernel, no false dependencies are added by reducing the number of work queues, nor are existing false dependencies (caused by the host-to-device copy) removed.

Decreasing the number of work queues in the K40 creates a similar difference to a Fermi GPU: one work queue and two copy queues. If you run the test on a Fermi GPU, you will find that dependencies do exist. This is a result of Kepler's work dispatch mechanisms, implemented in the Grid Management Unit (GPU). The GPU is responsible for managing and prioritizing work sent to the GPU. Analysis performed by the GPU helps reduce false dependencies.

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
```

Arrays match.

FIGURE 6-15

![](img/506ba3a4c9f4512233692f3f20de1f3a_319_1.png)

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
overlap with 4 streams : 0.6711104 ms (3.124928 GB/s)
speedup: 38.92%
```

Arrays match.

FIGURE 6-16

## GRID MANAGEMENT UNIT

Kepler introduces a new grid management and dispatch system, the Grid Management Unit (GMU). The GMU can pause the dispatch of new grids and queue suspended grids until they are ready, providing the flexibility to enable multiple runtimes such as Dynamic Parallelism. In Fermi devices, grids are passed to the CUDA scheduler from the stream queue. In Kepler devices, grids are passed to the GMU, and the GMU manages and prioritizes grids to be executed on the GPU. The GMU creates multiple hardware queues to reduce or eliminate false dependencies. Even when the GMU is restricted to a single hardware queue, streams can be kept as pipelines of work.

## Overlap Using Breadth-First Scheduling

Earlier examples demonstrated that Fermi GPUs delivered the best results while dispatching kernels using breadth-first approach. Now we examine the effect of breadth-first ordering in overlapping data transfers and compute. The following code segment dispatches both computation and communication among streams using breadth-first approach:

```cpp
// initiate asynchronous transfers to the device
for (int i = 0; i < NSTREAM; i++) {
    int offset = i * nElem;
    cudaMemcpyAsync(&d_A[offset], &h_A[offset], iBytes, cudaMemcpyHostToDevice, stream[i]);
    cudaMemcpyAsync(&d_B[offset], &h_B[offset], iBytes, cudaMemcpyHostToDevice, stream[i]);
}
```

```cpp
// launch a kernel in each stream
for (int i = 0; i < NSTREAM; i++) {
    int offset = i * nElem;
    sumArrays<<<grid, block, 0, stream[i]>>>(&d_A[offset], d_B[offset], d_C[offset]);
}
```

```cpp
// queue asynchronous transfers from the device
for (int i = 0; i < NSTREAM; i++) {
    int offset = i * nElem;
    cudaMemcpyAsync(&h_C[offset], &d_C[offset], iBytes, cudaMemcpyDeviceToHost, stream[i]);
}
```

You can download the full example simpleMultiAddDepth.cu from wrox. Figure 6-17 shows the timeline generated on the K40 device using one queue. There is no significant difference between Figure 6-16 (with one queue) and 6-15 with eight queues. Each stream only executes a single kernel, no false dependencies are added by reducing the number of work queues, nor are existing false dependencies (caused by the host-to-device copy) removed. If you run the same test on a Fermi device, you will see that overall performance of breadth-first approach is worse than depth-first approach. Therefore, for Kepler devices you not need to worry about order. On Fermi devices you need to be more aware of these issues and evaluate scheduling options.

![](img/506ba3a4c9f4512233692f3f20de1f3a_321_0.png)

FIGURE 6-17

## OVERLAP GPU AND CPU EXECUTION

It is relatively straightforward to achieve GPU and CPU overlap because all kernel launches are asynchronous by default. As a result, simply launching a kernel and immediately doing work in the host automatically overlaps GPU and CPU. The example in this section consists of two main parts:

- A kernel is dispatched to the default stream.
- Host computation is executed while waiting on the GPU.

The following kernel implementing a vector-scalar addition will be:

```cpp
global void kernel(float *g_data, float value) {
    int idx = blockIdx.x * blockDim.x + threadIdx.x;
    g_data[idx] = g_data[idx] + value;
}
```

In this example, cudaAsync performs two operations and a kernel launch is issued. A stop event is recorded to map the completion of all CUDA operations.

```cpp
cudaMemcpyAsync(d_a, h_a, bytes, cudaMemcpyHostToDevice);
kernel<<<grid, block>>>(d_a, value);
cudaMemcpyAsync(h_a, d_a, bytes, cudaMemcpyDeviceToHost);
cudaEventRecord(stop);
```

All of these operations are asynchronous to the host, and they are all bound to the default stream. As soon as cudaMemcpyAsync is issued, control is immediately returned to the host. One can then do any computation that does not depend on the output of the kernel. In the following code segment the host iterates, incrementing a counter. On each iteration, the host queries the stop event. Once the event is satisfied, the host continues.

```cpp
unsigned long int counter = 0;
while (cudaEventQuery(stop) == cudaErrorNotReady) {
    counter++;
}
```

You can download the example asyncAPI from wrox.com. The following is a typical output from nvprof collected on a Tesla K40 device. While waiting for GPU operations, the host performed 14,606 iterations.

```text
# nvprof ==2213=NVPROF is profiling process 2283, command: ./asyncAPI
> ./asyncAPI running on CPU device [Tesla K40]
CPU executed 14606 iterations while waiting for GPU to finish
==2213= Profiling application: ./asyncAPI
==2213= Profiling result:
```

| Time | Calls | Avg | Min | Max | Name |
|---|---|---|---|---|---|
| 48.89% | 1 | 10.61ms | 10.61ms | 10.61ms | [cuda Memcpy HtoD] |
| 46.04% | 1 | 10.04ms | 10.04ms | 10.04ms | [cuda Memcpy DtoH] |
| 3.25% | 1 | 709.82us | 709.82us | 709.82us | Kernel(float*, float) |
| 1.82% | 1 | 396.13us | 396.13us | 396.13us | [CUDA event] |

## STREAM CALLBACKS

A stream callback is another type of operation that can be queued to a CUDA stream. Once all of the operations in a stream preceding have completed, a host-side function callback is called by the CUDA runtime. This function is provided by the application. This allows arbitrary host-side logic to be inserted into CUDA streams. Stream callbacks are particularly powerful because they are the first example of GPU operations working on the host system, the opposite of every CUDA concept described in this point in the book.
