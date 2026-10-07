# Inverted Page Tables

An even more extreme space savings in the world of page tables is found with **inverted page tables**. Here, instead of having many page tables (one per process of the system), we keep a single page table that has an entry for each *physical* page of the system. The entry tells us which process is using this page, and which virtual page of that process maps to this physical page.

Finding the correct entry is now a matter of searching through data structure. A linear scan would be expensive, and thus a hash table is often built over the base structure to speed up lookups. The PowerPC is one example of such architecture [JM98].

More generally, inverted page tables illustrate what we've said from the beginning: page tables are just data structures. You do lots of crazy things with data structures, making them smaller or bigger, making them slower or faster. Multi-level and inverted page tables are just two of many things one could do.

# Swapping the Page Tables to Disk

Finally, we have assumed that page tables reside in kernel-owned physical memory. Even with many tricks to reduce the size of page tables, it is still possible, however they may be too big to fit into memory all at once. Thus, some systems place page tables in **kernel virtual memory**, allowing the system to *swap* some of these page tables to disk when memory pressure gets a little tight. We'll talk more about this in a future chapter (namely the case study of VAX/VMS), once we understand how to move pages in and out of memory in detail.

# Summary

We have seen how real page tables are built; not just as linear arrays but as more complex data structures. The trade-offs they present are in time and space — the bigger table, the faster the TLB miss, the choice of structure depends on the constraints of the given environment.

In a memory-constrained system (like other systems), small structures make sense; in a system with a reasonable amount of memory and workloads that use a large number of pages, a bigger table that speeds up TLB misses might be the right choice. With softwaremanaged TLBs, the entire space of data structures opens up to the delight of the operating system innovator (hint: that's you). What new can you come up with? What problems do they solve? Think of these questions as you fall asleep, and dream the big dreams that only operating-system developers can dream.