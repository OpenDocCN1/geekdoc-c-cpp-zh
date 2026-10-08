![](bbox=[0.15, 0.096, 0.918, 0.203])

```
-terminated=/usr/local/cuda-6.0/bin/mprof
CUDA DEVICE MAX_KERNELS=32
> Using device: Tesla K80 with num_streams 4
> Compute Capability 3.5 hardware with 15 multi-processors
> grid 1 block 1
Measured time for parallel execution = 0.157s
```

FIGURE 6-14

# OVERLAPPING KERNEL EXECUTION AND DATA TRANSFER

In the next section, you examined how to concurrently run multiple kernels in multiple streams. In this section, you will learn how to run kernels and data transfers concurrently. Overlapping kernels with data transfers exhibits different behavior and requires different considerations than concurrent kernel execution.

Fermi and Kepler GPUs have two copy engines: one for data transfer to the device, and one for data transfer from the device. Therefore, at most you can overlap two data transfers, but only if their directions differ and they are dispatched to different streams. Otherwise, data transfer will be serialized. It is important to keep this in mind when determining how to best overlap data transfer with kernel computation.

You will also need to examine the relationships between all data transfers and kernel executions in an application to distinguish the two cases:

+   * If a kernel consumes data, the data transfer for λ must be placed before the kernel launch and in the same stream.

+   * If a kernel does not consume any of λ, the kernel execution and data transfer can be placed in different streams.

In the second case, it is trivial to enable concurrent execution of the kernel and the data transfer: By placing them in separate streams, you have already indicated to the runtime that it is safe to execute them concurrently. However, achieving overlap between data transfer and kernel execution in the first case, where the kernel depends on that data, is more complex. You will use the vector addition example to show how data transfers and kernel execution can be overlapped when a dependency exists between the kernel and the transfer.

# Overlap Using Depth-First Scheduling

You are already familiar with the vector addition kernel:

```
__global void sumArrays(float *A, float *B, float *C, const int N) { int idx = blockIdx.x * blockDim.x + threadIdx.x;
```