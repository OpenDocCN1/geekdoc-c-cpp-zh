```
```cpp
const u32 num_samples,
const u32 num_elements,
const u32 * const src_data,
const u32 * const sample_data,
u32 * const bin_count,
const u32 num_threads,
const char * prefix
{
    const u32 num_blocks = num_elements / num_threads;

    start_device_timer();

    count_bins_gpu_kernel5<<<num_blocks, num_threads>>>(num_samples, src_data,
                        sample_data, bin_count);
        cuda_error_check(prefix, "Error invoking count_bins_gpu_kernel5");

    const TIMER_T func_time = stop_device_timer();
    return func_time;
}
```
```

Unlike the function to select samples where the maximum number of threads was limited by the number of samples, here we are limited only by the number of elements in the source array. Thus, the host function launches a kernel that contains one thread per element.

The kernel works out its element, and reads it from the source dataset in a nice coalesced manner. Using more threads per block here allows for increased read bandwidth from the global memory.

Each usage of a warp will jump off into the binary search, and will, after not too many iterations, return. With a random list of elements you get some thread divergence. However, in the more common case of a mostly sorted list, all threads tend to follow the same route, thus causing very little thread divergence in practice.

When all the threads of a warp have returned from the binary search, they increment the values in one of N bins held in global memory via an atomic write. Atomic operations to global memory are operations that are guaranteed to complete, uninterrupted, regardless of which thread on which SM initiated the action. Thus, we can safely have many threads write to the same address. Obviously one can physically write, so any clash of values results in serialization of the requests.

Unfortunately with a mostly sorted list we find that, because blocks are allocated in turn, most active blocks are in a similar area of memory. While this is very good for locality, it does mean all the threads are hitting the same memory area for the writes. With a sorted list we thus see a degradation of speed in this approach, but not a significant one, as we'll see later.

# Prefix sum

A prefix sum is useful in that it can be used to create a table of values that index into an array that has variable-length records. The size of each bin in our case is a variable length and each bin is stored sequentially in memory one after another. Thus, we can calculate a prefix sum array and then use array element 0 to access the start of bin 0, array element one to access the start of bin one, etc.

The code for the prefix sum on the CPU is quite simple: