
# COMPLETE VIRTUAL MEMORY SYSTEMS

0x00000000, 0xC000FFF to 0x0000FFF, and so forth. This direct mapping has two implications. The first is that it is simple to translate back and between kernel logical addresses and physical addresses; as a result, these addresses are often treated as if they are physical. The second is that if a chunk of memory is contiguous in kernel logical space, it is also contiguous in physical memory. This makes memory allocated in this part of the kernel's address space for operations which need contiguous physical memory to work correctly, with I/O transfers to and from devices via direct memory access (DMA) which we'll learn about in the third part of this book.

The other type of memory address is a kernel virtual. When getting memory of this type, kernel code calls a different allocator, `valloc`, which returns a pointer to a virtually contiguous region of the desired memory. Unlike kernel logical memory, kernel virtual is usually noncontiguous; kernel virtual pages may map to noncontiguous physical pages (and is thus not suitable for DMA). However, such memory is easier to allocate and thus for larger buffers finding a contiguous chunk of physical memory would be challenging.

In 32-bit Linux, one other reason for the existence of kernel virtual addresses is that they enable the kernel to address more than (roughly) 1 GB of memory. Years ago, machines had less memory than this, and access to 1 GB was not an issue. However, technology progressed, and there was a need to enable the kernel to use larger amounts of memory. Kernel virtual addresses, and their disconnection from a strict-to-one mapping to physical memory, make this possible. However, with the 64-bit Linux, the need is less urgent, because the kernel is not confined to only the last 1 GB of the virtual address space.

# Page Table Structure

Because we are focused on Linux for our discussion will center on the type of page-table structure provided by x86, it determines what Linux can and cannot. As mentioned before, x86 provides a hardware-multi-level page table structure, with one page table per process; the OS sets up mappings in its memory, a privileged register at the start of the page directory handles the rest. The OS gets involved, as expected, at process creation, deletion, and upon context switches, making sure in each case the correct page is being used by the hardware MMU to translate addresses.

Probably the biggest change in recent years is the move from 32-bit to 64-bit x86, as mentioned above. As in the VAX/VMS system, 32-bit address spaces have been around for a long time, and as technology changed, they were finally starting to become a real limit for programs. Virtual memory makes it easy to program systems, but with modern systems containing many GB of memory, 32 bits were no longer enough to reach each of them. Thus, the next leap became necessary.

Moving to a 64-bit address affects page table structure in x86 in the expected manner. Because x86 uses a multi-level page table, current 64-bit systems use a four-level table. The full 64-bit nature of the virtual address space is not in use, however, rather only the lower 48 bits. Thus, a virtual address can be viewed as follows:

| 63 | 47 | 31 | 15 | 0 |
|---|---|---|---|---|
| Unused | P1 | P2 | P3 | P4 | Offset |

As you can see in the picture, the top 16 bits of a virtual address are unused (and thus no role in translation), the bottom 12 bits (due to the 4-KB page size) are used as the offset (and hence used directly, and not translated), leaving the middle 36 bits of virtual address to take part in the translation. The P1 portion of the address is used to index into the topmost page directory, and the translation proceeds from there, one level at a time, until the actual page of the page table is indexed by P4, yielding the desired page table entry.

As systems grow ever larger, more parts of this voluminous address space will become enabled, leading to five-level and eventually six-level page-table tree structures. Imagine that: a simple page table requiring six levels of translation, to figure out where memory a certain piece of data resides.

# Large Page Support

Intel x86 allows the use of multiple page sizes, not just the standard 4-KB page. Specifically, designs support 2-MB and 1-GB pages in hardware. Thus, over time, Linux has evolved to allow applications to utilize huge pages (as they are called in the world of Linux).

Using huge pages, as hinted earlier, leads to numerous benefits. As seen in VAX/VMS, designs reduces the number of mappings that are needed in the page table; the larger the pages, the fewer mappings. However, page-table entries are not the driving force behind huge pages; rather, it is better TLB behavior and related performance gains.

When a process uses a large amount of memory, it fills the TLB with translations. If these translations are for 4-KB pages, only a small amount of total memory can be accessed without inducing TLB misses. Research shows that for modern "big memory" workloads running on machines with many CPUs, memory is a noticeable performance cost; research shows that some applications spend 10% of their cycles TLB misses [B+13].

Huge pages allow a process to access a large tract of memory without inducing TLB misses, by using fewer slots in the TLB, and thus is the main advantage.
