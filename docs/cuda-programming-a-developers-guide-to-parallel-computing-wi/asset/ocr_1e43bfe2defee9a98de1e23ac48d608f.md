typically 16 to 64 GB on the host, this may be problematic. However, this can be solved by using multiple GPU cards, with many high-end motherboards able to take up to four PCI-E cards, thus providing up to 24 GB per node of GPU memory.

Recursion is also problematic on GPUs, as it's only supported on compute 2.x GPUs, and then only for __device__ functions and not __global__ functions. The upcoming dynamic parallelism feature found in the Kepler K20 design will help in many respects with recursive algorithms.

Many CPU algorithms make use of recursion. Often it's convenient to break down a problem into a smaller problem that is then broken down further and so on until it becomes a trivial problem. Binary search is a classic example of this. Binary search splits a sorted list of numbers in half and simply asks the question of whether the data we're looking for exists in the left or right set. It then repeats the split until either the item is found or the problem becomes just two items and is thus trivial to solve.

However, any recursive algorithm can also be represented as an iterative algorithm. The binary search problem just mentioned is shown as an iterative solution within the sample sort example (see Chapter 6). Quick sort is also a common example of an algorithm that is typically implemented recursively. The algorithm picks a pivot point and then sorts all items less than the pivot point to the left and less than or equal to the pivot point to the right. You now have 2 independent datasets that can be sorted by two independent threads. This then becomes 4 threads on the next iteration, then 8, then 16, and so on.

The GPU kernel invocation requires a fixed number of threads. It cannot currently exploit dynamic parallelism, although this will change with the Kepler K20 release. Dynamic parallelism is where the amount of parallelism in the problem changes over time. In the quick sort problem it grows by a factor of two at every level. In path finding-type problems, discovery of a new node may introduce 30,000 or more additional paths into a problem.

How do you replicate such algorithms on a GPU? There are a number of approaches. The easiest is when the parallelism scales in some known manner, as with quick sort. You can then simply invoke one kernel per level or one kernel per N levels of the algorithm back-to-back in a single stream. As one level finishes, it writes its state to global memory and the next kernel execution picks up on the next level. As the kernels are already pushed into a stream ready to execute, there is no CPU intervention needed to launch the next stream. See Figure 7.1.

Where the parallelism grows by some indeterminate amount per iteration, you can also store the state in global memory. You have to then communicate back to the host the number of the amount of

![](bbox=[0.28, 0.68, 0.72, 0.85])

# FIGURE 7.1 Kernel invocations for a recursive algorithm.