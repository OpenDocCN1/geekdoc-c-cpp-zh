# ## 2.1 Basic GPU Terminology

Before going into the details on GPU architecture and programming, it is important to first clarify some of the terminology used throughout this chapter. For a more thorough list of terminology, refer to the glossary at the beginning of this book.

+   - **Host** – the CPU that the GPU is coupled to.
+   - **Device** – the GPU coprocessor that is coupled to a CPU.
+   - **Cores** – the processing elements of a GPU (or CPU) that execute a sequence of instructions (thread), SM or streaming multiprocessor – responsible for running GPU kernels and comprises a subset of the total GPU cores, registers for each residing core, a shared memory, texture cache, constant cache, L1 cache, and warp schedulers. A GPU is organized into multiple streaming multiprocessors (SMs).
+   - **Thread** – a set of instructions to be executed sequentially by a GPU (or CPU) processing element (compute core).
+   - **Warp** – a set of 32 SIMD threads (as currently implemented in CUDA-enabled architecture) that execute the same instructions simultaneously in hardware. Instructions are issued to and scheduled for execution on an entire warp of threads at a time, which step through the instructions in lockstep.
+   - **Kernel** – a procedure that is executed on the SMs of a GPU, typically by thread counts in the region of tens of thousands in parallel. Instructions of a kernel are scheduled in groups of a warp in a single-instruction multiple-thread (SIMT) manner.

# ## 2.2 Architecture of GPUs

As illustrated in Figure 2.1, GPU architecture differs from CPU architecture in that in place of a few processing cores with sophisticated hardware, that is, multilevel caching technologies, prefetching, and branch prediction, there are thousands of simplistic compute cores that operate in lock step. This so-called SIMT model is reminiscent of traditional SIMD architectures in CPUs, but

![](bbox=[0.252, 0.566, 0.808, 0.846])

Figure 2.1 General overview of CPU-GPU hardware configuration. Picture adaptation courtesy of Nvidia Corporation