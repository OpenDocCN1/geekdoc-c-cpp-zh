
![](img/133d518e3f69f4caaead32c569ae6c49_224_0.png)

Figure 17.6: Free Space With Two Chunks Allocated

bytes in after the three splits. But what happens when the calling program returns some memory via free()?

In this example, the application returns the middle chunk of allocated memory, by calling free(16500) (the value 16500 is arrived upon by adding the start of the memory region, 16384, to the 108 of the previous chunk and the 8 bytes of this chunk). This value is shown in the previous diagram by the pointer ptr.

The library immediately figures out the size of the free region, and then adds the free chunk back onto the free list. Assuming we insert at the head of the free list, the space now looks like this (Figure 17.6).

## Free-Space MANAGEMENT

[virtual address: 16KB]

| size: | 100 |
| next: | 16492 |
(now free)

| size: | 100 |
| next: | 16708 |
(now free)

| size: | 100 |
| next: | 16384 |
(now free)

| size: | 3764 |
| next: | 0 |
(the free 3764-byte chunk)

Figure 17.7: A Non-Coced Free List

Now we have a list that starts with a small free chunk (100 bytes, pointed to by the head of the list) and a large free chunk (3764 bytes). Our list has more than one element on it! And yes, the free space is fragmented, an unfortunate occurrence. One example: let's assume now that the last two in-use chunks are freed. Without coalescing, we end up with fragmentation (Figure 17.7). As you can see from the figure, we have a mess! Why? Simple, we forget to coalesce the list.

Now that we have the machinery under our belt, let's go over some strategies for managing free space. These approaches are mostly based on policies that you could think up; the ideal allocator is both fast and minimizes fragmentation. Unfortunately, the stream of allocation and free requests can be arbitrary (after all, they are determined by the programmer). Thus, we will not describe one last mechanism found within allocation libraries. Specifically, what should you do if the heap runs out of space? The simplest approach is to just fail. In some cases this is the only option, and returning NULL is an honorable approach, though you failed.

Most traditional allocators start with a small-sized heap and request memory from the OS when they run out. Typically, this make some kind of system call like `sbrk` to grow the heap. To service the `sbrk` request, the OS finds free pages, maps them into the address space, and returns the value of the end of the new heap; at that point, a larger heap is available, and the request can be serviced.

## 17.3 Basic Strategies

### Best Fit

The best fit strategy is quite simple: first, search through the free list and find chunks of free memory that are as big or bigger than the requested size, then return the smallest in that group; this is called best-fit chunk (it could be called smallest fit too). The intuition behind best fit is simple: by returning a block that is close to what the user asks, best fit tries to reduce wasted space. However, naive implementations pay a heavy penalty when performing exhaustive search.

### Worst Fit

The worst fit approach is the opposite of best fit; find the largest chunk and return the requested amount; keep the remaining (large) chunk on the free list. Worst fit tries to leave big chunks instead of small chunks that can arise from best-fit approach. Once again, it performs badly.

### First Fit

The first fit method simply finds the first block that is big enough and returns the requested amount to the user. As before, the remaining free space is kept for subsequent requests. First fit has the advantage of speed — no exhaustive search of all free spaces are necessary — but sometimes pollutes the beginning of the list with small objects. Thus, how the allocator manages the free list's order becomes an issue. One approach is to use address-based ordering; by keeping the list ordered by the address of the free space, coalescing becomes easier, and fragmentation tends to be reduced.

### Next Fit

Instead of always beginning the first-fit search at the beginning of the list, the next fit algorithm keeps an extra pointer to the location within the list where one was last. The idea is to spread the searches for free space throughout the list more uniformly, thus avoiding splintering of the beginning of the list. The performance of such an approach is quite similar to first fit, as exhaustive search is once again avoided.

### Examples

Here are a few examples of the above strategies. Envision a free list with three elements on it, of sizes 10, 30, and 20 (we'll ignore headers and other details here, just focusing on how strategies operate):

head -> 10 -> 30 -> 20 -> NULL

Assume an allocation request of size 15. A best-fit approach search the list and find that 20 was the best, as it is the smallest free space that can accommodate the request. The resulting list is:

head -> 10 -> 30 -> 5 -> NULL

As happens in this example, and often happens with best-fit approach, a small free chunk is now left over. A worst-fit approach is similar but instead finds the largest chunk, in this example 30. The resulting list is:

head -> 15 -> 20 -> NULL

## FREE-SPACE MANAGEMENT

The first-fit strategy, in this example, does the same thing as worst-fit, finding the first free block that can satisfy the request. The difference is in the search cost; both best-fit and worst-fit look through the entire list; first-fit only examines chunks until it finds one that fits, reducing search cost.

These examples just scratch the surface of allocation policies. More detailed analysis with real workloads and more complex allocator behaviors (e.g., coalescing) are required for a deeper understanding. Perhaps something for a homework section, do you say?

## 17.4 Other Approaches

Beyond the basic approaches described above, there have been a host of suggested techniques and algorithms to improve memory allocation in some way. We list a few of them here for your consideration (i.e., to make you about a little more than just best-fit allocation).

### Segregated Lists

One interesting approach that has been around for some time is the use of segregated lists. The basic idea is simple: if a particular application has (one for a few) popular-sized request that it makes, keep a separate list to manage objects of that size; all requests are forwarded to a more general memory allocator.

The benefits of such approach are obvious. by having a chunk of memory dedicated to one particular size of requests, fragmentation is much less of concern; moreover allocation and free requests can be served quite quickly when they are of the right size, as no complicated search of a list is required.

Just any good idea, this approach introduces new complications into a system as well. For example, how much memory should one allocate to the pool of memory that specialized requests of a given size, opposed to the general pool? One allocator, the slab allocator by user-engineer Jeff Bonwick (which was designed for the Solaris kernel), handles this in a rather nice way.

Specifically, when the kernel boots, it allocates a number of objects for kernel caches that are likely to be requested frequently (such as locks, file-system inodes, etc.); the object caches thus are segregated free of given size serve allocation and free requests quickly. When a cache is running low on free space, it requests slabs of memory from a more general allocator (the total amount requested being a multiple of the page size and the object in question). Conversely, when the reference counts of the objects within a given slab all go to zero, the general allocator can reclaim them from the specialized allocator, which is often done when the VM system needs more memory.
