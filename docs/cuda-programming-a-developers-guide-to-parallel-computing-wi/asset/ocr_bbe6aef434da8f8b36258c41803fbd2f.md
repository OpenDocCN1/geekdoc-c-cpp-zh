Some of the main changes in compute 2.x hardware are as follows:

+   - Introduction of 16 K to 48 K of L1 cache memory on each SP.
+   - Introduction of a shared L2 cache for all SMs.
+   - Support in Tesla-based devices for ECC (Error Correcting Code)-based memory checking and error correction.
+   - Support in Tesla-based devices for dual-copy engines.
+   - Extension in size of the shared memory from 16 K per SM up to 48 K per SM.
+   - For optimum coalescing of data, it must be 128-byte aligned.
+   - The number of shared memory banks increased from 16 to 32.

Let's look at the implications of some of these changes in detail. First, let's pick up on the introduction of the L1 cache and what this means. An L1 (level one) cache is a cache present on a device and is the fastest cache type available. Compute 1.x hardware has no cache, except for the texture and constant memory caches. The introduction of a cache makes it much easier for many programmers to write programs that work well on GPU hardware. It also allows for applications that do not follow a known memory pattern at compile time. However, to exploit the cache, the application either needs to have a sequential memory pattern or have at least some data reuse.

The L2 cache is up to 768 K in size on Fermi and, importantly, is a unified cache, meaning it is shared and provides a consistent view for all the SMs. This allows for much faster interblock communication through global atomic operations. Compared to having to go out to the global memory on the GPU, using the shared cache is an order of magnitude faster.

Support for ECC memory is a must for data centers. ECC memory provides for automatic error detection and correction. Electrical devices emit small amounts of radiation. When in close proximity to other devices, this radiation can change the contents of memory cells in the other device. Although the probability of this happening is tiny, as you increase the exposure of the equipment by densely packing it into data centers, the probability of something going wrong rises to an unacceptable level. ECC, therefore, detects and corrects single-bit upset conditions that you may find in large data centers. This reduces the amount of available RAM and negatively impacts memory bandwidth. Because this is a major drawback on graphics cards, ECC is only available on Tesla products.

Dual-copy engines allow you to extend the dual-buffer example we looked at earlier to use multiple streams. Streams are a concept we’ll look at in detail later, but basically, they allow for N independent kernels to be executed in a pipeline fashion as shown in Figure 3.8.

![](bbox=[0.11, 0.74, 0.88, 0.86])

# FIGURE 3.8 Stream pipelining.