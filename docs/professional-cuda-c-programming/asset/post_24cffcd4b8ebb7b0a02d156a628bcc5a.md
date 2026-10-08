
the GPU parallel architecture, allowing you to reason about thread concurrency. In Chapter 2, you learned that the CUDA programming model exposes two primary abstractions: a memory hierarchy and a thread hierarchy that you control the massively parallel GPU. Accordingly, the CUDA execution model provides insights that are useful for writing efficient code in terms of both instruction throughput and memory accesses.

You will focus on instruction throughput in this chapter and learn more about efficient memory accesses in Chapters 4 and 5.

## GPU Architecture Overview

The GPU architecture is built around a scalable array of Streaming Multiprocessors (SM). GPU hardware parallelism is achieved through the replication of this architectural building block. Figure 3-1 illustrates the key components of a Fermi SM:

- CUDA Cores
- Shared Memory/L1 Cache
- Register File
- Load/Store Units
- Special Functions Units
- Warp Scheduler

Each SM in a GPU is designed to support concurrent execution of hundreds of threads, and there are generally multiple SMs per GPU, so it is possible to have thousands of threads executing concurrently a single GPU. When a kernel grid is launched, the thread blocks of kernel grid are distributed among available SMs for execution. Once scheduled on an SM, the threads of a thread block execute concurrently on the same SM and are scheduled based on the availability of SM resources. Instructions within a single thread are pipelined to leverage instruction-level parallelism, in addition to the thread-level parallelism you are already familiar with CUDA.

CUDA employs a Single Instruction Multiple Thread (SIMT) to manage and execute threads in groups of 32 warps. In each warp all threads execute the same instruction at the same time. Each thread has its own instruction counter and register state, and carries out the current instruction on its own data. Each SM partitions the thread blocks assigned to it into 32-thread warps that it schedules for execution on available hardware resources.

The SIMT architecture is similar to the SIMD (Single Instruction, Multiple Data) architecture. Both SIMD and SIMT implement parallelism by broadcasting the instruction to multiple execution units in a vector execute group. A key difference is that SIMD requires all elements in a vector to execute in a unified synchronous group, whereas SIMT allows multiple threads in a warp to execute independently. Even though all threads in a warp start at the same program address, it is possible for individual threads to have different behavior. SIMT enables you to write thread-level parallel code for independent, scalar threads, as well as data-parallel code for coordinated threads. The SIMT model includes three key features that SIMD does not:

- Each thread has its own instruction address counter.
- Each thread has its own register state.
- Each thread can have an independent execution path.

![](img/506ba3a4c9f4512233692f3f20de1f3a_96_0.png)

FIGURE 3-1

## A MAGIC NUMBER: 32

The 32 is a magic number in CUDA programming. It comes from hardware, and has a significant impact on the performance of software.

Conceptually, you can think of it as the granularity of work processed simultaneously in SIMD fashion by an SM. Optimizing your workloads to fit within the boundaries of a warp (group of 32 threads) will generally lead to more efficient utilization of GPU compute resources. You will learn much about this issue in subsequent chapters.

A thread block is scheduled on only one SM. Once a thread block is scheduled on an SM, it remains until execution completes. An SM can hold more than one thread block at the same time. Figure 3-2 illustrates the corresponding components from the logical view and hardware view of CUDA programming.

![](img/506ba3a4c9f4512233692f3f20de1f3a_97_0.png)

FIGURE 3-2

Shared memory and registers are precious resources in an SM. Shared memory is partitioned among threads resident on the SM and registers are partitioned among threads. In a thread block threads can cooperate and communicate with each other through these resources. While all threads in a thread block run in parallel, not all threads execute physically at the same time. As a result, different threads in a thread block may make progress at a different pace.

Sharing data among parallel threads may cause a race condition: Multiple threads accessing the same data with an undefined ordering, which results in unpredictable program behavior. CUDA provides a means to synchronize threads within a thread block to ensure that all threads reach points in execution before further progress. However, primitives are provided for inter-block synchronization.

While wraps within a thread block may be scheduled in order, the active warps are limited by SM resources. When a warp idle for any reason (for example, waiting for values to be read from device memory), the SM is free to schedule another warp from any thread block that is resident on the same SM. Switching between concurrent warps has no overhead because hardware resources are partitioned among all threads and blocks on an SM, so the state of the newly scheduled warp is already stored on the SM.

> SM: THE HEART OF THE GPU ARCHITECTURE
The Streaming Multiprocessor (SM) is the heart of the GPU architecture. Registers and shared memory are scarce resources in the SM. CUDA partitions these resources among all threads on an SM. Therefore, these limited resources impose a strict restriction on the number of active warps in an SM, which corresponds to the amount of parallelism in an SM. Knowing some basic facts about hardware components of an SM will help you organize and kernel execution to get the best performance.

In the next section, you will receive a brief tour of two versions of NVIDIA GPU architecture: the Fermi and Kepler architectures. Special attention will be given to their hardware resources. You will learn about their hardware features through examples and exercises, and this will help you gain insights into improving kernel performance.

## The Fermi Architecture

The Fermi architecture is the first complete GPU computing architecture to deliver the features required for the most demanding HPC applications. Fermi has been widely adopted for accelerating workloads.

Figure 3-3 illustrates a block diagram of the Fermi architecture focused on GPU computing with graphics-specific components omitted. Fermi features up to 512 accelerator cores, called CUDA cores each has a fully pipelined integer arithmetic logic unit (ALU) and a floating-point unit (FPU) that executes one integer or floating-point instruction per cycle. The CUDA cores are organized into 16 streaming multiprocessors (SM), with 32 CUDA cores each. Fermi has 34-bit GDDR5 memory interfaces supporting up to a total of 6 GB of global on-board memory, a key resource for many applications. A host interface connects the GPU to the CPU via the PCI bus. The GigaThread engine (shown in orange on the left side of the diagram) is a global scheduler that distributes blocks to the SM warp schedulers.

![](img/506ba3a4c9f4512233692f3f20de1f3a_99_0.png)

CUDA core Shared memory, register file, and L1 cache Scheduler and dispatch units

FIGURE 3-3

Fermi includes a coherent 768 KB L2 cache, shared by all 16 SMs. Each SM in Figure 3-3 is represented by a vertical rectangular strip containing:

- Execution units (CUDA cores)
- Scheduler and dispatcher units that schedule warps
- Shared memory, the register file, and L1 cache

Each multiprocessor has 16 load/store units (shown in Figure 3-1), allowing source and destination addresses to be calculated for 16 threads (a half-warp) per clock cycle. Special function units (SFUs) execute intrinsic instructions such as sine, cosine, square root, and interpolation. Each SFU can execute one intrinsic instruction per thread per clock cycle.

Each SM features two warp schedulers and two instruction dispatch units. When a thread block is assigned to an SM, all threads in a thread block are divided into warps. The warp schedulers select
