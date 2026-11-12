
```
// Make sure all threads have taken their turn.
__syncthreads();
}

// If this thread was the one with the minimum
if (min_val[0] == data)
{
    // Check for equal values
    // Lowest tid wins and does the write
    atomicMin(&min_tid, tid);
}

// Make sure all threads have taken their turn.
__syncthreads();

// If this thread has the lowest tid
if (tid == min_tid)
{
    // Increment the list pointer for this thread
    list_indexes[tid]++;
}

// Store the winning value
dest_array[i] = data;

// If the current list has not already been
// emptied then read from it, else ignore it
if ((list_indexes[tid] < num_elements_per_list))
    data = src_array[tid + (list_indexes[tid] * num_lists)];
else
    data = 0xFFFFFFFF;
}

// Wait for min_tid thread
__syncthreads();
}
```

One of the main problems of the simple 1-to-N reduction is it becomes increasingly slower as the value of N increases. We can see from previous tests that the ideal value of N is around 16 elements. The kernel works by creating a partial reduction of N values and then a final reduction of those N values into a single value. In this way it’s similar to the reduction example, but skips most of the iterations.

Notice that min_val has been extended from a single value into an array of shared values. This is necessary so each independent thread can minimize the values over its dataset. Each min value is 32 bits wide so it exists in a separate shared memory bank, meaning there are no bank conflicts provided the maximum number of first-level reductions results in 32 or less elements.

The value of REDUCTION_SIZE has been set to eight, which means the program will do a min over groups of eight values prior to a final min. With the maximum of 256 elements, we get exactly 32

![](img/e0b192dbaf05f61ad420bee512a8c4e4_161_0.png)

FIGURE 6.14
Hybrid parallel reduction.

**Table 6.12 Hybrid Atomic and Parallel Reductions Results (ms)**

| Device/Threads | 1 | 2 | 4 | 8 | 16 | 32 | 64 | 128 | 256 |
|---|---|---|---|---|---|---|---|---|---|
| GTX470 | 29.41 | 17.62 | 11.24 | 8.98 | 7.2 | 6.49 | 6.46 | 7.01 | 8.57 |
| GTX260 | 56.85 | 33.54 | 20.83 | 15.29 | 11.87 | 10.5 | 10.36 | 11.34 | 14.65 |
| GTX460 | 24.12 | 14.54 | 9.36 | 7.64 | 6.22 | 5.67 | 5.68 | 6.27 | 7.81 |

![](img/e0b192dbaf05f61ad420bee512a8c4e4_161_1.png)

FIGURE 6.15
Hybrid atomic and parallel reduction graph.

separate banks being used to do the reduction. In the 256 elements we have a 256:32:1 reduction. With a 128-element list we have a 128:16:1 reduction, etc.

The other major change is now only the thread that writes out the winning element reads a new value into data, a register-based value that is per thread. Previously, all threads re-read in the value from their respective lists. As only one thread won each round, only one list pointer changed. Thus, as N increased, this became increasingly inefficient. However, this doesn't help as much as you might at first imagine.

So how does this version perform? Notice in Table 6.12 that the minimum time, 5.86 ms from the atomicMin example, has fallen to 5.67 ms. This is not spectacular, but what is interesting to note is the shape of the graph (Figure 6.15). No longer is the graph such an inclined U shape. Both the 32- and 64-thread versions beat the simple atomicMin based on 16 threads. We're starting to smooth out the upward incline introduced by the merge step as shown in table 6.12 and figure 6.15.

## Shared memory on different GPUs

Not all GPUs are created equal. With the move to compute 2.x devices, the amount of shared memory became configurable. By default, compute 2.x (Fermi) devices are configured to provide 48K of shared memory instead of the 16 K of shared memory on compute 1.x devices.

The amount of shared memory can change between hardware releases. To write programs that scale in performance with new GPU releases, you have to write portable code. To support this, CUDA allows you to query the device for the amount of shared memory available with the following code:

```
struct cudaDeviceProp device_prop;
CUDA_CALL(cudaGetDeviceProperties(&device_prop, device_num));
printf("\nShared Memory: %u", device_prop.sharedMemPerBlock);
```

Having more shared memory available allows us to select one of two strategies. We can either extend the amount of shared memory used from 16 K to 48 K or we can simply schedule more blocks into a single SM. The best choice will really depend on the application at hand. With our sorting example, 48 K of shared memory would allow the number of lists per SM to be reduced by a factor of three. As we saw earlier, the number of lists to merge has a significant impact on the overall execution time.

## Shared memory summary

So far we have looked only at sorting within a single SM, in fact within a single block. Moving from a single-block version to a multiple-block version introduces another set of merges. Each block will produce an independent sorted list. These lists then have to be merged, but this time in global memory. The list size moves outside which can be held in shared memory. The same then becomes true when using multiple GPUs—you generate N or more sorted lists where N equals the number of GPUs in the system.

We've looked primarily at interthread cooperation with shared memory in this section. The merging example was selected to demonstrate this in a manner that was not too complex and easy to follow. Parallel sorting has a large body of research behind it. More complex algorithms may well be more efficient, in terms of the memory usage and/or SM utilization. The point here was to use

a practical example that could be easily followed and process lots of data that did not simply reduce to a single value.

We'll continue to look at sorting later and look at how interlock communication and coordination can be achieved in addition to thread-level communication.

## Questions on shared memory

- 1. Looking at the radix_sort algorithm, how might the use of shared memory be reduced? Why would this be useful?
- 2. Are all the synchronization points necessary? In each instance a synchronization primitive is used. Discuss why. Are there conditions where they are not necessary?
- 3. What would be the effect of using C++ templates in terms of execution time?
- 4. How would you further optimize this sorting algorithm?

## Answers for shared memory

- 1. There are a number of solutions. One is to use only the memory allocated to the sort. This can be done using an MSB radix sort and swapping the 1s with elements at the end of the list. The 0 list counts forward and the 1 list counts backward. When they meet, the next digit is sorted until the LSB is sorted. Reducing the memory usage is useful because it allows larger lists in the shared memory, reducing the total number of lists needed, which significantly impacts execution time.
- 2. The main concept to understand here is the synchronization points are necessary only when more than one warp is used. Within a warp all instructions execute synchronously. A branch causes the nonbranched threads to stall. At the point the branch converges, you are guaranteed all instructions are in sync, although the warps can then instantly diverge again. Note that memory must be declared as volatile or you must have syncthreads points within the warp if you wish to guarantee visibility of writes between threads. See Chapter 12 on common problems for a discussion on the use of the volatile qualifier.
- 3. Templates would allow much of the runtime evaluation of the num_lists parameter to be replaced with compile time substitution. The parameter must always be a power of 2, and in practice will be limited to a maximum of 256. Thus, a number of templates can be created and the appropriate function called at runtime. Given a fixed number of iterations known at compiler time instead of runtime, the compiler can efficiently unroll loops and substitute variable reads with literals. Additionally, templates can be used to support multiple implementations for different data types, for example, using the atomicMin version for integer data while using a parallel reduction for floating-point data.
- 4. This is rather an open-ended question. There are many valid answers. As the number of sorted lists to merge increases, the problem becomes significantly larger. Elimination of the merge step would be a good solution. This could be achieved by partially sorting the original list into N sublists by value. Each sublist could then be sorted and the lists concatenated, rather than merged. This approach is the basis of another type of sort, sample sort, an algorithm we look at later in this chapter.

Consider also the size of the dataset in the example, 1024 elements. With 256 threads there are just four elements per list. A radix sort using a single bit is very inefficient for this number of
