issues one common instruction to be executed by all threads in a warp at a time. Ensuring blocks of threads are a multiple of 32 (a warp) prevents underpopulation of warps and therefore idle cores. The SIMT offers not only thread-level parallelism but also instruction-level parallelism, ensuring that instructions are pipelined to the cores in a constant stream by scheduling the next instruction to an active warp of threads. Threads are able to branch and diverge away from other threads, as each thread keeps track of its own instruction address and register state; however, divergent branching will cause all other threads in a warp to be idled (masked to null operations, no-ops) until the divergent branch is complete and threads are back on the same execution path. For this reason, a GPU is used most effectively when there are no divergent branches, that is, conditional statements, in a warp of threads and hence no idle cores waiting for threads to catch up.

# 2.2.3 Evolution of Nvidia Hardware through the Generations

The evolution of Nvidia GPU hardware can be tracked by compute capability (c.c.), which is a major and minor revision number linked to core architecture design. GPUs with the same major revision number are of the same hardware generation. Minor revision numbers reflect incremental improvements to the core architecture, that is, new features. For a complete explanation of the differences between compute capabilities, refer to the CUDA Programming Guide [1]. The architectural design of the latest generation Nvidia hardware (Kepler—compute capability 3.x) is shown in diagrammatic form in Figure 2.3. Each SM is equipped with registers, shared memory (SMEM), read-only and L1 instruction and data cache. All SMs have access to an L2 cache, which is responsible for reducing the latency of global memory accesses.

# 2.3 CUDA Programming Model

In the CUDA programming model, functions within the code are offloaded to the GPU as kernels. The workload of each kernel is decomposed into N independent workloads, which are then executed

# Kepler memory hierarchy

![](bbox=[0.16, 0.58, 0.88, 0.82])

Figure 2.3 Nvidia Kepler architecture memory model. Global memory and L2 cache can be accessed by all SMs. L1 cache and shared memory (SMEM) are accessible to threads running on the same SM. Picture adaptation courtesy of Nvidia