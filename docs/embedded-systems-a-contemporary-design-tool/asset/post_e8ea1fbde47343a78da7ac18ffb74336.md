
![](img/679b8d2d47f1bf86e17aca48f596f5cc_252_0.png)

removed from the system. If the design is using memory mapped I/O, then all of physical memory will not be available for data or code.

virtual memory overlays

## 4.14 MEMORY SUBSYSTEM ARCHITECTURE

We have looked at several different kinds of memory, how one can design and build an interface to them, and how one might allocate subsets of the physical memory address space to meet the different requirements of the application. We now bring a number of those pieces together in a memory system. The block-labeled memory in the diagram for a von Neumann machine actually comprises a number of memory components of different kinds, sizes, and speeds arranged in a hierarchical manner and designed to cooperate with each other. Such a hierarchy is given in Figure 4.32.

secondary cache
main, primary

The commonly used hierarchical metrics for relating the different kinds of memories are speed and storage capacity. At the top are the slowest, largest, and least expensive memories. These are known as secondary memory and are shown in the diagram by the block on the left. At the bottom are the smallest, fastest memories called cache memory; these are typically higher speed SRAMs. These devices also tend to be the most expensive. In the middle of the hierarchy is main or primary memory. These are either lower speed SRAM devices or, more commonly, DRAM memories. CPU registers are sometimes included in the ranking as higher speed memory than cache.

The motivation for building a memory system as a hierarchical collection of different kinds of memories is that we would prefer an application program to execute as quickly as possible. Accessing memory takes time; each access contributes to the time required to execute an instruction that can have a significant negative impact on real-time performance in an embedded application.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_253_0.png)

Figure 4.32 Typical Memory Hierarchy Utilizing a Variety of Memory Types

We will not consider secondary storage; the typical embedded applications will not use this. The discussion here will focus on main memory and cache, the last two blocks on the right. These can be implemented using (variations on) the designs presented in the previous sections.

## 4.15 BASIC CONCEPTS OF CACHING

*icache, dcache* Cache is a small, fast memory that temporarily holds copies of block data and program instructions from the main memory. The increased speed of cache memory over that of main memory components offers the prospect for programs to execute much more rapidly if the instructions and data can be held in cache. Many of today’s higher performance microprocessors, implemented around the Harvard architecture, will internally support both an *icache* (instruction cache) and a *dcache* (data cache). We will now examine the concept of caching in greater detail. We will look first at the ideas behind caching, what cache is, why it works, and some of the potential difficulties encountered in embedded applications. We will then examine several alternative caching schemes and, later, the effect of caching on performance in Chapter 14.

### 4.15.1 Locality of Reference

Time is a critical constraint in many embedded applications. Time burdens arising from memory accesses and memory access speeds can have a significant impact on meeting those constraints. Thus, in executing a design, among the many goals two are to reduce the number of memory accesses and make each access as short (in time) as possible. Ideally, one would like to make all memory as fast as technology allows. There is an associated cost, however. High-speed memories are expensive and complex to design; support circuitry can be rather expensive as well. As the speed demands and the requirements for additional support circuitry increase, a growing stress will be placed on the system’s power supplies. Let’s look at an alternate approach.

Almost all embedded software today is written using a procedural paradigm and is often written in the C language. Many years ago IBM analyzed how such programs are designed and executed and discovered an interesting phenomenon. Execution generally occurs either sequentially or in small loops with a small number of instructions. Such behavior means that the overall forward progress through a program is proceeding at a much lower rate than the access times of the fastest memory. Put another way, with respect to the entire program, actual execution takes place within a small window that moves forward through the program. This is shown in Figure 4.33.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_254_0.png)

Formally, such a phenomenon is called sequential locality of reference. Because the program is executing only a few instructions within a small window, if those few instructions can be kept in fast memory, the program will appear to be executing out of that memory. Through such a scheme, we can gain the benefits of higher speed at a reduced cost. An important point to remember is that the approach works if the area within the program in which the application is currently executing is in the local window. The method can easily be defeated with large loops or repeated branches outside of the window. Two other types of locality of reference, spatial and temporal, are also defined. Spatial locality suggests that a future access of a resource, a memory address in this case, is going to be physically near one previously accessed. Temporal locality suggests that a future access of a resource, again, a memory address, is going to be temporally near one recently accessed. Using locality of reference knowledge can significantly improve memory access time performance.

A major caveat for real-time applications that utilize a caching scheme is that demand for the movement of blocks of instructions or data from or to main memory to or from cache is driven by the execution path taken through the program. Such a path is often governed by results of computations, external events, and/or any of a variety of other factors. Which path of a branch is taken, for example, may determine whether or not the application has to bring in data/instructions from cache.

Although it is important to keep in mind that any such schemes can have significant negative impact on real-time systems, it is also important to remember that, when properly used, they can have a significant positive impact on system performance. It is evident, then, that using caching schemes is sometimes appropriate. If caching must be used, it is essential to understand the problem and the caching algorithm completely, to determine an upper bound on context switching, and to leave plenty of time margin in the application.

### 4.15.2 Cache System Architecture

When using a caching scheme, the goal is to operate out of cache memory – typically SRAM – to the greatest extent possible. When program execution needs an instruction or data that is not in the cache, it must be brought in from main memory – typically DRAM.

The block diagram for the architecture appears as shown in Figure 4.34.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_255_0.png)

Figure 4.34 Cache System Architecture

## 4.16 DESIGNING A CACHE SYSTEM

Caching requires a certain amount of higher speed memory. The size of that memory determines how much information can be stored locally. In larger modern processors, several levels of cache internal to the processor can be enabled or disabled. The cache under discussion here is external to the CPU.

### 4.16.1 A High-Level Description

The application program begins executing and encounters a need for a piece of data or an instruction. To locate that item, first the cache is checked. If the item is found, there is a cache hit. The data or instruction is retrieved and used. If the item is not found, there has been a cache miss and the item must be obtained from somewhere else. For the current discussion that location will be main memory.

The block containing the data or instruction is brought into the cache from main memory. If there is room left in the cache, the block is stored; otherwise room must be made. That task is accomplished by overwriting or removing an existing block. On one hand, if the contents of the block have been modified, the changes must be saved. On the other hand, if there have been no modifications to any data in the old block, that block can simply be discarded and the new block written in its place.

Several questions arise immediately.

- How do we know when something is not in the cache?
- Where do we go to find something if it is not in the cache?
- What if it's not there?
- How do we know if there is room left in the cache?
- How do we know if information in the cache was modified?
- How do we select the block to replace?
