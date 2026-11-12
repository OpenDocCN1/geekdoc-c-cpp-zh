in all cores. Thus, all processor cores see the same view of memory at any point in time. This is one of the key factors that limits the number of cores in a processor. Communication becomes increasingly more expensive in terms of time as the processor core count increases. The worst case in a cache-coherent system is where each core writes adjacent memory locations as each write forces a global update to every core's cache.

A non cache-coherent system by comparison does not automatically update the other core's caches. It relies on the programmer to write the output of each processor core to separate areas/addresses. This supports the view of a program where a single core is responsible for a single or small set of outputs. CPUs follow the cache-coherent approach whereas the GPU does not and thus is able to scale to a far larger number of cores (SMs) per device.

Let's assume for simplicity that we implement a kernel as four blocks. Thus, we have four kernels on the GPU and four processes or threads on the CPU. The CPU may support mechanisms such as hyperthreading to enable processing of additional threads/processes due to a stall event, a cache miss, for example. Thus, we could increase this number to eight and we might see an increase in performance. However, at some point, sometimes even at less than the number of cores, the CPU hits a point where there are just too many threads.

At this point the memory bandwidth becomes flooded and cache utilization drops off, resulting in less performance, not more.

On the GPU side, four blocks is nowhere near enough to satisfy four SMs. Each SM can actually schedule up to eight blocks (16 on Kepler). Thus, we'd need 8 x 4 = 32 blocks to load the four SMs correctly. As we have four independent operations, we can launch four simultaneous kernels on Fermi hardware via the streams feature (see Chapter 8 on using multiple GPUs). Consequently, we can launch 16 blocks in total and work on the four arrays in parallel. As with the CPU, however, it would be more efficient to work on one array at a time as this would likely result in better cache utilization. Thus, on the GPU we need to ensure we always have enough blocks (typically a minimum of 8 to 16 times the number of SMs on the GPU device).

# FLYNN'S TAXONOMY

We mentioned the term SIMD earlier. This classification comes from Flynn's taxonomy, a classification of different computer architectures. The various types are as follows:

+   - SIMD—single instruction, multiple data
+   - MIMD—multiple instructions, multiple data
+   - SISD—single instruction, single data
+   - MISD—multiple instructions, single data

The standard serial programming most people will be familiar with follows the SISD model. That is, there is a single instruction stream working on a single data item at any one point in time. This equates to a single-core CPU able to perform one task at a time. Of course it's quite possible to provide the illusion of being able to perform more than a single task by simply switching between tasks very quickly, so-called time-slicing.

MIMD systems are what we see today in dual- or quad-core desktop machines. They have a work pool of threads/processes that the OS will allocate to one of N CPU cores. Each thread/process has an