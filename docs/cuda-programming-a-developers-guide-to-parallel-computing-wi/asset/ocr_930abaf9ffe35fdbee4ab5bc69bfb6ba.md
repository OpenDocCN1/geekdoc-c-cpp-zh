Processors such as the Intel 17 are 64-bit processors, meaning they can process up to 64 bits at a time (8 bytes). The SSE SIMD instruction set extends this to 128 bits. With SIMD instructions on such a processor, we eliminate all redundant instruction memory fetches, and generate one sixteenth of the memory read and write cycles compared with fetching and writing 1 byte at a time. AVX extends this to 256 bits, making it even more effective.

For a high-definition (HD) video image of 1920 × 1080 resolution, the data size is 2,073,600 bytes, or around 2 MB per color plane. Thus, we generate around 260,000 SIMD cycles for a single conventional processor using SSE/MMX. By SIMD cycle, we mean one read, compute, and write cycle. The actual number of processor clocks may be considerably different than this, depending on the particular processor architecture.

The Connection Machine used 64 K processors. Thus, the 2 MB frame would have resulted in about 32 SIMD cycles for each processor. Clearly, this type of approach is vastly superior to the modern processor SIMD approach. However, there is of course a caveat. Synchronization and communication between processors becomes the major issue when moving from a rather coarse-threaded approach of today's CPUs to a hugely parallel approach used by such machines.

# CELL PROCESSOR

Another interesting development in supercomputers stemmed from IBM's invention of the Cell processor (Figure 1.4). This worked on the idea of having a regular processor act as a supervisory

![](bbox=[0.18, 0.5, 0.84, 0.87])

FIGURE 1.4 IBM cell processor die layout (8 SPE version).