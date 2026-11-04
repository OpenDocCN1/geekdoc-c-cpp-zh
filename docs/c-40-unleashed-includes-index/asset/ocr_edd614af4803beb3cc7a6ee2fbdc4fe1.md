Other than in the world of native code, allocating memory on the heap is simple and efficient because of the illusion of infinite memory the heap creates. Heaps for use by native code typically maintain a free list to find memory to grant allocation requests, which requires search logic and use of some fitting algorithm. The difference in the case of allocation is illustrated in Figure 9.10.

![](bbox=[0.065, 0.196, 0.841, 0.638])

FIGURE 9.10  Heap memory allocation.

Notice how easy it is to allocate memory on the managed heap: Just see whether there’s enough space left, allocate, and move the high-water mark. Looks familiar, doesn’t it? Allocating memory on the managed heap is conceptually similar to stack-based allocation.

In the world of native code, more complexity is usually involved: To find available space, a free list needs to be searched. When a suitable spot is found (for example, by first-fit search), a pointer to the memory location is returned and the free list is patched up. In doing so, little regions of memory can appear that nearly no object can ever fit in. These allocate space nevertheless and are a waste of memory space. This is known as internal fragmentation, something the managed heap doesn’t suffer from.

Before we explain what happens when the heap is full in both the native and managed world, let’s first illustrate how deallocation happens in the native world. Managed code takes away this burden of manual memory management from the developer, but in native code it’s the only way to reclaim memory (see Figure 9.11).