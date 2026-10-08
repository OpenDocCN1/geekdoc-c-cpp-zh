Connecting these values to warp or thread counts depends on the application. Suppose each thread moves one float (4 bytes) from global memory to the SM for computation, you require 18,500 threads or 579 KB to hide all latency on Fermi GPUs:

```
74 KB ÷ 4 bytes/thread = 18,500 threads
```

```
18,500 + 32 threads/warp = 579 warps
```

The Fermi architecture has 16 SMs. Therefore, you require 579 warps + 16 SMs = 36 warps per SM to hide all latency. If each thread performed more than one 4-byte load, fewer threads would be required to hide the memory latency.

Much like instruction latency, you can increase the available parallelism by creating more independent memory operations within each thread/warp, or creating more concurrently active threads/warps.

Latency hiding depends on the number of active warps per SM, which is implicitly determined by the execution configuration and resource constraints (registers and shared memory used in a kernel). Choosing an optimal configuration is a matter of striking a balance between latency hiding and resource utility. You will examine this issue in detail in the next section.

# EXPOSING PARALLELISM

Because the GPU partitions resources among threads, switching between concurrent warps has very little overhead (on the order of one or two cycles) as the required state is already available on-chip. If there are sufficient active warps, you can keep the GPU busy in every pipeline stage every cycle. In this situation, the latency of one warp is hidden by the execution of other warps. Therefore, exposing sufficient parallelism to SMs is beneficial to performance.

A simple formula for calculating the required parallelism is to multiply the number of cores per SM by the latency of one arithmetic instruction on SM. For example, Fermi has 32 single-precision floating-point pipeline lanes and the latency of one arithmetic instruction is 20 cycles, so at minimum 32 x 20 = 640 threads per SM are required to keep your device busy. However, this is a lower bound.

# Occupancy

Instructions are executed sequentially within each CUDA core. When one warp stalls, the SM switches to executing other eligible warps. Ideally, you want to have enough warps to keep the cores of the device occupied. Occupancy is the ratio of active warps to maximum number of warps, per SM.

```
occupancy = \frac{active warps}{maximum warps}
```