When preempted, a partition is swapped to disk or (in the case of most embedded systems) to slower memory or RAM, or the code portion address is saved. As is common in virtual memory schemes, using fixed-size partitions can lead to memory fragmentation. Fragmentation can happen in several ways. Consider a system using fixed-size partitions of 2 K. Let three jobs be brought into memory:

+   J1-1.5 K
+   J2-0.5 K
+   J3-2.1 K

Let these jobs be allocated to successive partitions in memory. We see that four partitions are required. Now, let J2 to finish and be swapped out. What does this mean? We immediately see the following problems:

+   J2. Leaving has left a hole that can only be filled by job <= 2K. The task consumes a 2 K partition leaving three-fourths of it unused.
+   J3. Requires two partitions, one of size 2 K and one of size 0.1 K; this is very wasteful of memory. If these three jobs consume the last of the memory, a new job of size 1 K cannot enter, although it will fit.

# 4.20.3.2 Variable Number

Programs with a variable number of tasks are treated in a similar manner to segments in a traditional virtual memory scheme. Memory allocation for a variable number of tasks is similar to a paged virtual memory scheme. Allocation is determined by the process's requirements when it is loaded into memory. Such an approach works well when the number of tasks is unknown or variable. Wasted memory arising from a misfit into a partition size is virtually eliminated. Holes remain but can be eliminated by using compaction schemes. Compaction moves pieces of used memory into contiguous locations. It is important to keep in mind that any such schemes can have significant negative impact on real-time systems. If they must be used, then one needs to understand them and the application context completely. One should also determine an upper bound on context switching and leave plenty of margin in the application.

# 4.21 TESTING MEMORIES

Let's now look at the problem of testing memories. As we learned in earlier studies, a wide variety of different kinds of memories can be incorporated into a design. On the one hand, the amount of memory (ROM or RAM) that can economically be included in a contemporary system seems to grow daily. On the other hand, trying to test that memory as a part of production test has become more costly and complex. Exhaustive testing of all possible combinations of data values is not a practical approach. Moreover, it is logical to assume that in production, the object of a memory test is not to confirm the individual memory chips themselves, but rather to ensure that the installation and interconnection of the devices are defect free.

To address the memory test problem, as with any other problem, we begin by decomposing it into the basic pieces. The high-level diagrams for a RAM or ROM memory system are redrawn in Figure 4.44. Looking first from an external point of view, we see that both types are similar, the major difference being the R/W line and bidirectional data flow for the RAM. Each memory block shown may comprise a number of memory chips interconnected via the address, data, and control buses.