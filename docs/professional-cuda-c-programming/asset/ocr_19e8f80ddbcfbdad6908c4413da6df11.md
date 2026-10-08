becomes essential for parallelization. CUDA maximizes your ability to fully utilize the parallel power of GPUs.

Depending on the original code, you might need to refactor your program to expose inherent parallelism in order to improve application performance. Parallel data decomposition is an unavoidable step during this phase. There are basically different approaches to partitioning data among massive threads: block partitioning and cyclic partitioning. In block partitioning, elements are chunked together and distributed to threads. The performance of a kernel can be sensitive to block size. In cyclic partitioning, every thread processes one element at a time before jumping ahead by as many elements as there are threads. The basic considerations for data partitioning relate to architecture features and the nature of the algorithm being implemented.

# Optimization

After you have organized your code to run in parallel, then you move to the next stage: optimizing the implementation to improve performance. Roughly speaking, CUDA-based optimizations can be applied at the following two levels:

+   - Grid-level
- Kernel-level

During grid-level optimization, focus is on overall GPU utilization and efficiency. Techniques to optimize grid-level performance include running multiple kernels simultaneously and overlapping kernel execution with data transfers using CUDA streams and events.

There are three major factors that can limit performance for a kernel:

+   - Memory bandwidth
- Compute resources
- Instruction and memory latency

During kernel-level optimization, you focus on the efficient use of GPU memory bandwidth and compute resources and the reduction or hiding of instruction and memory latency.

CUDA provides the following useful and powerful tools to help you identify performance opportunities at the grid-level and kernel level:

+   - Nsight Eclipse Edition (nsight)
- NVIDIA Visual Profiler (nvvp)
- NVIDIA Command-line Profiler (nvprof)

These profiling tools are effective at guiding you during the optimization processes and offer suggestions for the best course of action to improve performance. nvprof and nvvp have already been used in many exercises and examples throughout this book.