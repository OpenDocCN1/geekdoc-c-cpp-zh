
list_indexes, num_lists, num_elements_per_list);

There are two options that can be employed, to pass the necessary values through registers, or to create an area of memory called a stack frame. Most modern processors have a large register set (32 or more registers). Thus, for a single level of calls, often this is enough. Older architectures use stack frames and push the values onto the stack. The called function then pops the values off the stack. As you require memory to do this, on the GPU this would mean using "local" memory, which is local only in terms of which thread can access it. In fact, "local" memory can be held in global memory, so this is hugely inefficient, especially on the older architectures (1.x) where it's not cached. At this point we need to rewrite the merge routine to avoid the function call. The new routine is thus:

```cpp
// Uses a single thread for merge
__device__ void merge_array(const u32 * const src_array,
                            u32 * const dest_array,
                            const u32 num_lists,
                            const u32 num_elements,
                            const u32 tid)
{
__shared__ u32 list_indexes[MAX_NUM_LISTS];

// Multiple threads
list_indexes[tid] = 0;
__syncthreads();

// Single threaded
if (tid == 0)
{
    const u32 num_elements_per_list = (num_elements / num_lists);

    for (u32 i=0; i<num_elements; i++)
    {
        u32 min_val = 0xFFFFFFFF;
        u32 min_idx = 0;

        // Iterate over each of the lists
        // (u32 list=0; list<num_lists; list++)
        {
            // If the current list has already been
            // emptied then ignore it
            if (list_indexes[list] < num_elements_per_list)
            {
                const u32 src_idx = list + (list_indexes[list] * num_lists);
                const u32 data = src_array[src_idx];
```

## Table 6.8 Initial Single-Thread Merge Sort Results

| Device/Threads | 1 | 2 | 4 | 8 | 16 | 32 | 64 | 128 | 256 |
|---|---|---|---|---|---|---|---|---|---|
| GTX470 | 27.9 | 16.91 | 12.19 | 12.31 | 17.82 | 31.46 | 59.42 | 113.3 | 212.7 |
| 9800GT | 44.83 | 27.21 | 19.55 | 19.53 | 28.07 | 51.08 | 96.32 | 183.08 | 342.16 |
| GTX260 | 55.03 | 33.38 | 24.05 | 24.15 | 34.88 | 62.9 | 118.71 | 225.73 | 422.55 |
| GTX460 | 22.76 | 13.85 | 10.11 | 10.41 | 15.29 | 27.18 | 51.46 | 90.26 | 184.54 |

![](img/e0b192dbaf05f61ad420bee512a8c4e4_150_0.png)

## FIGURE 6.10 Initial single-thread merge sort graph.

```cpp
if (data <= min_val)
{
    min_val = data;
    min_idx = list;
}
}
list_indexes[min_idx++]++;
dest_array[i] = min_val;
}
}
```

This function now combines the original merge_array function and its find_min function. Recompiling now results in no additional stack frame. Running the code, we find the results shown in Table 6.8. If you graph this, it's somewhat easier to see (Figure 6.10).

| Device | 9800GT | GTX260 | GTX460 | GTX470 |
|---|---|---|---|---|
| Core clock | 650 MHz | 625 MHz | 726 MHz | 608 MHz |
| Memory bandwidth | 61 GB/s | 123 GB/s | 115 GB/s | 134 GB/s |

What is surprising from this graph is the worst performer is actually the GTX260, which is slower than the previous generation 9800GT. It's interesting to also note the GTX460 is faster than the GTX470 in this particular test. To understand this, you need to look at the specific devices used, as shown in Table 6.9.

You can see the 9800GT has a higher internal clock rate than the GTX260. The same is true of the GTX460 and GTX470. Since the program is using just a single SM, and memory access is dominated by shared memory access time, this is entirely to be expected.

However, perhaps the most interesting feature you can see from the graph is that increasing the number of threads beyond a certain point actually makes the calculation go slower. This initially seems counterintuitive if you have never seen this relationship before. What this type of result points to is that there is some conflict of resources or the problem does not scale in a linear manner when you increase the number of threads.

The problem is the latter. The merge step is single thread and must look at N lists for every element. As the number of lists is increased, the problem space becomes 2N, 4N, 8N, etc. in line with the number of threads. The optimal point for this algorithm, based on the timings, is actually between four and eight lists of data. This is not very good, as it considerably limits the potential amount of parallelism.

## Parallel merging

For better performance, clearly more than one thread in the merge stage is required. However, this introduces a problem, in that we're writing to a single list. To do this, the threads need to cooperate in some manner. This makes the merge somewhat more complex.

```cpp
// Uses multiple threads for merge
// Deals with multiple identical entries in the data
__device__ void merge_array6(const u32 * const src_array,
u32 * const dest_array,
const u32 num_lists,
const u32 num_elements,
const u32 tid)
{
const u32 num_elements_per_list = (num_elements / num_lists);
__shared__ u32 list_indexes[MAX_NUM_LISTS];
list_indexes[tid] = 0;
// Wait for list_indexes[tid] to be cleared
__syncthreads();

// Iterate over all elements
for (uint32 i=0; i<num_elements;i+=4)
{
    // Create a value shared with the other threads
    __shared__ uint32 min_val;
    __shared__ uint32 min_tid;

    // Use a temp register for work purposes
    uint32 data;

    // If the current list has not already been
    // emptied then read from it, else ignore it
    if (list_indexes[tid] < num_elements_per_list)
    {
        // Work out from the list_index, the index into
        // the linear array
        const uint32 src_idx = tid + (list_indexes[tid] * num_lists);

        // Read the data from the list for the given
        // thread
        data = src_array[src_idx];
    }
    else
    {
        data = 0xFFFFFFFF;
    }

    // Had zero clear the min values
    if (tid == 0)
    {
        // Write a very large value so the first thread wins the min
        min_val = 0xFFFFFFFF;
        min_tid = 0xFFFFFFFF;
    }

    // Wait for all threads
    __syncthreads();

    // Have every thread try to store it's value into
    // min_val. Only the thread with the lowest value
    // will win
    atomicMin(&min_val, data);
    atomicMin(&min_tid, data);

    // Make sure all threads have taken their turn.
    __syncthreads();

// If this thread was the one with the minimum
if (min_val == data)
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
}
}
```

This version uses num_lists threads to do the merge operation. However, only a single thread writes to the output data list at a time, thus ensuring the single output list is correct at all times.

It makes use of the atomicMin function. Instead of one thread reading all the values from the lists and computing the minimum, each thread calls atomicMin with the value of its list entry. Once all threads have called the atomicMin function, each thread reads it back and compares this with the value it tried to write. If the values are the same, then the thread was the winning thread. However, there is one further problem in that there may be several winning threads, because the data item can be repeated in one or more lists. Thus, a second elimination step is required by only those threads with identical data. Most of the time, this second step will not be necessary. However, in the worst case of sorting a list of identical numbers, it would cause every thread to have to go through two elimination steps.

So how does this version perform? As you can see from Table 6.10 and Figure 6.11, we have reduced the total execution time using the larger number of threads (128 and 256 threads) by

## Table 6.10 atomicMin Parallel Merge Sort Results (ms)

| Device/Threads | 1 | 2 | 4 | 8 | 16 | 32 | 64 | 128 | 256 |
|---|---|---|---|---|---|---|---|---|---|
| GTX470 | 29.15 | 17.38 | 10.96 | 7.77 | 6.74 | 7.43 | 9.15 | 13.55 | 22.99 |
| GTX260 | 55.97 | 32.67 | 19.87 | 13.22 | 10.51 | 10.86 | 13.96 | 19.97 | 36.68 |
| GTX460 | 23.78 | 14.23 | 9.06 | 6.54 | 5.86 | 6.67 | 8.41 | 12.59 | 21.58 |
