304

Chapter 5. Threads and Shared Memory

complete sorting the entire array. The easy way to do a merge is to leave it all to the master thread. A more sophisticated way is to merge pairwise while assigning the pairs to different threads. Time and compare the two sorting routines, with two different ways of doing a merge, with a single threaded sort.

If the merge is implemented pairwise, it could be important to ensure that the number of threads in the parallel regions remains the same, even if some threads remain inactive. Explain why that could be the case.

**Exercise 5.1.4.** An array, or equivalently a pointer to its first entry, is a shared variable. Array entries are modified independently by different threads using the same pointer. Is OpenMP flush essential to make changes made by one thread visible to the other threads?

**Exercise 5.1.5.** Write an OpenMP program to find the minimum entry of an array using the **parallel** for construct with an appropriate reduction clause.

# 5.2 Optimizing OpenMP programs

In OpenMP, program memory is often naturally split between threads. In an example such as matrix transpose, for instance, blocks of the matrix are mainly handled by certain threads. When multiple threads occupy processor cores across multiple packages, there is much to be gained by allocating memory for each thread in a memory channel that is close to it.

The way to do this is explained in section 5.2.1. In first one may see that memory is allocated during a call to malloc() or its equivalent. In fact, during malloc(), the memory that gets allocated is typically virtual and not physical. It is only during first access, and the resulting page fault, that a page of virtual memory is mapped to a page of physical memory. Therefore, the allocation of page frames in near memory depends on the initialization protocol. Briefly, each page in virtual memory must first be accessed by the thread most likely to use it.

It is certainly possible that a page of virtual memory is heavily used by a certain thread in a certain phase of the program and by another thread in another phase of the program. In such situations, the best option is to try to map the threads that use the same pages of memory to nearby cores. This technique is also explained in section 5.2.1.