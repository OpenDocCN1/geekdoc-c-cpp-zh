# Chapter 8. Special Topic: Graphics Coprocessor Programming Using CUDA

The K20 coprocessor's 13 streaming multiprocessors are comparable with the AVX host's 16 processors. The K20 begins to look very different from its Sandy Bridge host if we note that each multiprocessor has as many as 64K = 65,536 registers, each 32 bits wide. The AVX processor's register file of 256-bit YMM registers looks tiny in comparison.

A large register file is central to the K20 and other graphics coprocessors work. A large number of threads can be resident on the multiprocessor, and each thread gets its own subset of registers. Because the register file is split between threads, the streaming multiprocessor can switch between threads with zero overhead.

Each multiprocessor in the K20 can hold more than 2,048 threads. Therefore, each thread gets at least 64 registers.

When Intel brought the Xeon Phi to claim ground in supercomputing, the large number of registers of the K20 and other graphics coprocessor was a key parameter the Xeon Phi had 61 processor cores with four threads resident on each processor. The register file consisting of 32 512-bit ZMM registers is replicated for each thread. So the total number of registers on the Phi is equivalent to 125K 32-bit registers, which is approximately a sixth of the number of registers on the K20.

A thread on a graphics device like the K20 is different from a thread on an x86 machine or the Phi. To get a sense of how threads work in the K20, we give the rest of the output of the `cudaDeviceProp` program from section 7.1.

```
Number of threads per warp: 32
Maximum number of threads per block: 1024
Maximum of each dimension of block: 1024 x 1024 x 64
Maximum of each dimension of grid: --->
    ---> 2147483647 x 65535 x 65535
```

Warps, thread blocks, and grids of thread blocks are the basis of GPU programming.

On the graphics device, a thread never exists by itself. Threads are grouped into warps. On the K20 and most NVIDIA devices, a warp is 32 threads. The warp is fundamental to GPU programming. Instructions are executed by the entire warp and not by individual threads.

The threads in a warp must execute exactly the same instruction. If some threads in a warp diverge as a result of if-statements, for example, the threads that do not enter the if-block idle and wait while other threads are still in the if-block. Thread