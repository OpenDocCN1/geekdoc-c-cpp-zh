![](bbox=[0.155, 0.115, 0.855, 0.375])

FIGURE 9.19 Zero-copy graph (time in ms versus transfer size).

You can of course achieve this using streams and asynchronous memory copies, as demonstrated in Chapter 8. Zero copy simply presents an alternative, and somewhat simpler, interface you can work with.

However, there are some caveats. Beware of exactly how many times the data is being fetched from memory. Re-reading data from global memory will usually exclude the use of zero-copy memory.

If we modify the program to read the value from host memory twice instead of once, then the performance drops by half on the 9800 GT and GTX260 platforms, the compute 1.x devices. This is because each and every fetch from global memory on these platforms is not cached. Thus, the number of PCI-E transactions issued is doubled, as we double the amount of times the GPU accesses the zero-copy memory area.

On Fermi the situation is somewhat different. It has an L1 and L2 cache and it’s highly likely the data fetched earlier in the kernel will still be in the cache when the latter access hits the same memory address. To be sure, you have to explicitly copy the data you plan to reuse to the shared memory. So in Fermi, depending on the data pattern, you typically do not see the device issuing multiple PCI-E transactions, as many of these hit the internal caches and therefore never create a global memory transaction.

Thus, zero-copy memory presents a relatively easy way to speed up your existing serial code without having to explicitly learn the stream API, providing you are careful about data reuse and have a reasonable amount of work to do with each data item.

However, be aware that the bandwidth of the PCI-E bus is nowhere near the bandwidth available on a CPU. The latest Sandybridge i7 processor (Socket 2011) achieves some 37 GB/s of memory bandwidth, from a theoretical peak of 51 GB/s. We’re achieving 5–6 GB/s from a theoretical peak of 8 GB/s on the PCI-E 2.0 bus. You must have enough work in your application to justify the cost of moving the data over the PCI-E bus. Consider that the CPU can be a better alternative in situations where very little work is being done per element.