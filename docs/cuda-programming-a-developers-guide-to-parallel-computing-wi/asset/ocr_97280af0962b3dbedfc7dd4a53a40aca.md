# STRATEGY 7: SELF-TUNING APPLICATIONS

GPU optimization is not like CPU optimization. Many techniques overlap, while others have undesirable effects. I've tried to cover the major areas of optimization in the preceding sections. However, optimization is never an exact science, not when practiced by human programmers anyway. There are lots of factors that need to be considered when designing code for the GPU. Getting an optimal solution is not easy and it takes considerable time to become familiar with what works, try different solutions, and understand why one works when another doesn't.

Consider some of the major factors:

+   - Transfer to and from the host.
+   - Memory coalescing.
+   - Launch configuration.
+   - Theoretical and achieved occupancy.
+   - Cache utilization.
+   - Shared memory usage/conflicts.
+   - Branch divergence.
+   - Instruction-level parallelism.
+   - Device compute level.

For someone starting out with CUDA, there is a lot to think about and it will take time to become proficient with each of these areas. However, the most challenging aspect of this is that what works on one device many not work on another. Throughout this book we've used the whole range of available devices and a number of different host platforms where necessary to highlight differences.

In the same way as different CPUs provide different levels of performance and functionality, so do GPUs. The CPU world is largely stuck with an x86 architecture, which reflects design goals of a system designed to run serial programs. There have been many extensions to provide additional functionality, such as MMX, SSE, AVX, etc. The x86 instruction set is today translated within the hardware to micro-instructions, which can be really for any target hardware. Sandybridge is perhaps the best example of this, where the micro-instructions themselves are actually cached instead of the x86 assembly code instructions.

GPU hardware is also not fixed and has changed significantly since the first CUDA-enabled devices were released back in the GTX8800 times. CUDA compiles to PTX, a virtual assembly code, aimed at a parallel processor–like architecture. PTX can itself be compiled to many targets, including CPUs, as the cooperative thread array concept lends itself to implementation in most parallel hardware. However, as far as we're concerned, it's compiled to a specified compute level for various NVIDIA GPUs. Therefore, you need to be familiar with what a given compute level provides, that is you need to understand what hardware you are writing code. This has always been the basis of good optimization. Trends toward abstraction, layering, and hiding the architecture are all aimed at programmer productivity, but often at the expense of performance.

Not every programmer is interested in the intricate workings of the hardware. Even with the previous list of issues to consider you're unlikely to get an optimal solution the first time, the second time, or the Nth time without considerable thought and a lot of trial and error. Thus, one