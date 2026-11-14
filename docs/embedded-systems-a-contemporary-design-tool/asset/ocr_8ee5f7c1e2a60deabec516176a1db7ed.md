![](bbox=[0.283, 0.083, 0.815, 0.273])

![](bbox=[0.283, 0.313, 0.815, 0.413])

Consider a memory in which the stored data words are a pattern of alternating 0’s and 1’s, such as is illustrated in Figure 4.14.

When the data is read from memory, the pattern on each data line will be a square wave. The highest frequency of that square wave is the memory bandwidth.

Latency. Latency is the amount of time required to access the first of a sequence of words. Latency measures the time necessary to compute the address of that sequence and then locate its first block of words in memory.

Block access time. Block access time gives a measure of the time to access an entire block from the start of a read. Block access time will include the time to find the 0th word of a block and then to transfer the remaining words.

Page. A page is a logical view placed on larger collections of words in memory. Pages are generally comprised of blocks; the size of a page can be given in words or in blocks.

# 4.9 A MEMORY INTERFACE IN DETAIL

If a single ROM or RAM chip is large enough and the address and data I/O are wide enough to satisfy system memory requirements, then the interface is rather straightforward. Often, however, one or the other of the requirements is not satisfied. Let's look at implementing a memory system in which neither of the requirements is met.

We will look first at an SRAM system and then at a DRAM design. A ROM implementation is identical to an SRAM design minus the write capability.