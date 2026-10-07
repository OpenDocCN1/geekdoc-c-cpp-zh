# Segmentation

So far we have been putting the entire address space of each process in memory. With the base and bounds registers, the OS can easily relocate processes to different parts of physical memory. However, you might have noticed something interesting about these address spaces of ours: there is a big chunk of “free” space in the middle, between the stack and the heap.

As you can imagine from Figure 16.1, although the space between the stack and heap is not being used by the process, it is still using physical memory; thus, the relocate the entire address space somewhere in physical memory; the simple approach of using a base and bounds register pair to visualize memory is wasteful. It also makes it quite hard to run a program when the entire address space doesn’t fit into memory; thus, base and bounds is not as flexible as we would like. And thus:

> The Crux: How to Support a Large Address Space How do we support a large address space with (potentially) a lot of free space between the stack and the heap? Note that in our examples, with tiny (pretend) address spaces, the waste doesn’t seem too bad. Imagine, a 32-bit address space (4 GB in size); a typical program will only use megabytes of memory, but still demand that the entire address be resident in memory.

# 16.1 Segmentation: Generalized Base / Bounds

To solve this problem, an idea was born, and it is called segmentation. It is quite an old idea, going as far back as the very early 1960's [H61, G62]. The idea is simple: instead of having just one base and bounds pair in our MMU, why not have a base and bounds per logical segment of the address space? A segment is a contiguous portion of the address space of a particular length, and in its canonical