
For C-Shell:

```cpp
setenv CUDA_DEVICE_MAX_CONNECTIONS 32
```

This environment variable can also be set directly in the C host program:

```cpp
setenv("CUDA_DEVICE_MAX_CONNECTIONS", "32", 1);
```

Each CUDA stream is mapped to a single CUDA device connection. If the number of streams exceeds the hardware connections, multiple streams share the same hardware work queue, false dependencies might occur.

To check the behavior of CUDA streams on a platform that supports Hyper-Q but has insufficient hardware connections, modify the simpleHyperqDepth example to use CUDA streams:

```cpp
#define NSTREAM 8
```

and set the number of CUDA device connections to:

```cpp
// set up max connectionio
char* iname = "CUDA_DEVICE_MAX_CONNECTIONS";
setenv (iname, "4", 1);
```

Run the modified example on a Kepler GPU with nvvp:

```bash
$ nvvp ./simpleHyperqDepth
```

Figure 6-10 shows streams, but only four-way concurrency. Because there are only four device connections, two streams share each queue. Dispatching the kernels the deep-first approach causes false dependencies between the two streams assigned to the same work queue, similar to the results observed when using deep-first order on a Fermi GPU.

![](img/506ba3a4c9f4512233692f3f20de1f3a_312_0.png)

FIGURE 6-10

Next, check the behavior of the breadth-first approach using the same settings. As illustrated in Figure 6-11, all eight streams now run concurrently. Dispatching the kernels in breadth-first order resolve false dependencies.

![](img/506ba3a4c9f4512233692f3f20de1f3a_313_0.png)

FIGURE 6-11

## Concurrency-Limiting GPU Resources

Limited kernel resources can inhibit the amount of kernel concurrency possible in an application. In the previous examples, kernels were launched with only one thread to avoid any hardware restriction on concurrency. As a result, each kernel execution only requires a small amount of device resources.

```cpp
kernel1<<<1, 1, 0, streams[i]>>();
```

In real applications, kernels launched usually create more than one. Normally, hundreds or thousands of threads are created. With so many, the available hardware resources become the primary limiting factor for concurrency as they prevent launching eligible kernels. To observe this in, you can change the execution configuration in the simpleHyperBread to use more threads per block and more blocks per grid:

```cpp
dim3 block (128);
dim3 grid (32);
```

You should also increase the number of CUDA streams being used to: 16:

```cpp
#define NSTREAM 16
```

After recompiling, check the behavior of simpleHyperqBread on a Kepler device using nvvp:
`$ nvvp ./simpleHyperqBread`

As shown in Figure 6-12, only eight-way concurrency was achieved, even though the number of CUDA device connections is set to 32. Because the GPU is unable to allocate sufficient resources to execute all eligible kernels, concurrency is limited.

![](img/506ba3a4c9f4512233692f3f20de1f3a_314_0.png)

FIGURE 6-12

## Blocking Behavior of the Default Stream

To demonstrate how the default stream can block operations in non-null streams, modify the depth first dispatch loop in simpleHyperDepth.cu to invoke kernel_3 in the default stream:

```cpp
// dispatch job with depth first ordering
for (int i = 0; i < n_streams; i++) {
    kernel_1<<<grid, block, 0, streams[i]>>>();
    kernel_2<<<grid, block, 0, streams[i]>>>();
    kernel_3<<<grid, block>>>();
    kernel_4<<<grid, block, 0, streams[i]>>>();
}
```

Because the third kernel is launched in the default stream, any later operations on non-null streams will be blocked until the operations in the default stream complete. Figure 6-13 shows the timeline captured using nvvp for this code running on a Tesla K40. The timeline shows how each kernel_3 prevents any further execution in all other blocking streams.

![](img/506ba3a4c9f4512233692f3f20de1f3a_315_0.png)

FIGURE 6-13

## Creating Inter-Stream Dependencies

Ideally, there would be no unintended dependencies between streams (that is, false dependencies). However, in complex applications it can be used to introduce inter-stream dependencies that block operations in one stream until operations in another stream have completed. Events can be used to add inter-stream dependencies.

Suppose you want the work in one stream to only start after all other streams complete. You can use events to create a dependency between streams. First, create synchronization-only events with the flag cudaEventDisableTiming, as:

```cpp
cudaEvent_t *kernelEvent = (cudaEvent_t*)malloc(n_streams * sizeof(cudaEvent_t));
for (int i = 0; i < n_streams; i++) {
    cudaEventCreateFlags(&kernelEvent[i], cudaEventDisableTiming);
}
```

Next, create an event to track the completion of each stream using cudaRecord. Then, use cudaStreamWait to force the last stream (that is, streams [n_streams-1]) to wait for all other streams:

```cpp
// dispatch job with depth first
for (int i = 0; i < n_streams; i++) {
    kernel_1<<<grid, block, 0, streams[i]>>>();
    kernel_2<<<grid, block, 0, streams[i]>>>();
    kernel_3<<<grid, block, 0, streams[i]>>>();
    kernel_4<<<grid, block, 0, streams[i]>>>();
    cudaEventRecord(kernelEvent[i], streams[i]);
    cudaStreamWait(streams[n_streams-1], kernelEvent[i], 0);
}
```

You can download the full code for this example in the file simpleHyper.cu from Wrox.com. Figure 6-14 shows the nvvp timeline. Note that the fourth stream, streams [n_streams-1], only starts its work after all other streams complete.

![](img/506ba3a4c9f4512233692f3f20de1f3a_316_0.png)

```
-terminated=/usr/local/cuda-6.0/bin/mprof
CUDA DEVICE MAX_KERNELS=32
> Using device: Tesla K80 with num_streams 4
> Compute Capability 3.5 hardware with 15 multi-processors
> grid 1 block 1
Measured time for parallel execution = 0.157s
```

FIGURE 6-14

## OVERLAPPING KERN EXECUTION AND DATA TRANSFER

In the next section, you examined how to concurrently run multiple kernels in multiple streams. In this section, you will learn how to run kernels and data transfers concurrently. Overlapping kernels with data transfers exhibits different behavior and requires different considerations than concurrent kernel execution.

Fermi and Kepler GPUs have two copy engines: one for data transfer to the device, and one for data transfer from the device. Therefore, at most you can overlap two data transfers, but only if their directions differ and they are dispatched to different streams. Otherwise, data transfer will be serialized.
