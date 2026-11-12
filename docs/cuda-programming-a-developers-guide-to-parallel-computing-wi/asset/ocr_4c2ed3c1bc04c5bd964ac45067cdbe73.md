![](bbox=[0.25, 0.11, 0.75, 0.34])

# **FIGURE 6.4**
Merging N lists simultaneously.

two lists are then further combined in the same manner to produce one final sorted list, {1,1,2,2,3,5,8,9}.

Thus, as each merge stage is completed, the amount of available parallelism halves. As an alternative approach where N is small, you can simply scan N sets of lists and immediately place the value in the correct output list, skipping any intermediate merge stages as shown in Figure 6.4. The issue is that the sort performed at the stage highlighted for elimination in Figure 6.4 is typically done with two threads. As anything below 32 threads means we’re using less than one warp, this is inefficient on a GPU.

The downside of this approach if that it means you would need to read the first element of the sorted list set from every set. With 64 K sets, this is 64 K reads, or 256 MB of data that has to be fetched from memory. Clearly, this is not a good solution when the number of lists is very large.

Thus, our approach is to try to achieve a much better solution to the merge problem by limiting the amount of recursion applied to the original problem and stopping at the number of threads in a warp, 32, instead of two elements per sorted set, as with a traditional merge sort. This reduces the number of sets in the previous example from 64 K sorted sets to just 4 K sets. It also increases the maximum amount of parallelism available from N/2 to N/32. In the 128 K element example we looked at previously, this would mean we would need 4 K processing elements. This would distribute 256 processing elements (warps) to every SM on a GTX980. As each Fermi SM can execute a maximum of 48 warps, multiple blocks will need to be iterated through, which allows for smaller problem sizes and speedups on future hardware. See Figure 6.5.

Shared memory is bank switched. We have 32 threads within a single warp. However, if any of those threads access the same bank, there will be a bank conflict. If any of the threads diverge in execution flow, you could be running at up to 1/32 of the speed in the worst case. Threads can use registers that are private to a thread. They can only communicate with one another using shared memory.

By arranging a dataset in rows of 32 elements in the shared memory, and accessing it in columns by thread, you can achieve bank conflict-free access to the memory (Figure 6.6).

For coalesced access to global memory, something we’ll cover in the next section, you’d need to fetch the data from global memory in rows of 32 elements. Then you can apply any sorting algorithm