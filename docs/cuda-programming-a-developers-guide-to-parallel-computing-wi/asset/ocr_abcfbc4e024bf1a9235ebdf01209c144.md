```
const TIMER_T func_time = stop_device_timer();

return func_time;
}
```

Finally, to work out the index into the source data we simply multiply our sample data index (tid) by the size of the sample interval. For the sake of simplicity we'll only look at the case where the dataset sizes are multiples of one another.

Notice both the CPU and GPU versions return the time taken for the operation, something we'll do in each section of the sort to know the various timings of each operation.

# Sorting the samples

Next we need to sort the samples we've selected. On the CPU we can simply call the qsort (quicksort) routine from the standard C library.

```
__host__ TIMER_T sort_samples_cpu(
__uint32 * const sample_data,
const u32 num_samples)
{
const TIMER_T start_time = get_time();

qsort(sample_data, num_samples, sizeof(u32),
&compare_func);

const TIMER_T end_time = get_time());
return end_time - start_time;
}
```

On the GPU, however, these standard libraries are not available, so we'll use the radix sort we developed earlier. Note, radix sort is also provided by the Thrust library, so you don't have to write it as we've done here. I won't replicate the code here since we've already looked at it in detail in the shared memory section.

One thing to note, however, is the version we developed before does a radix sort on a single SM in shared memory and then uses a shared memory reduction for the merge operation. This is not an optimal solution, but we'll use it for at least the initial tests.

# Counting the sample bins

Next we need to know how many values exist in each sample bin. The CPU code for this is as follows:

```
__host__ TIMER_T count_bins_cpu(const u32 num_samples,
const u32 num_elements,
const u32 * const src_data,
const u32 * const sample_data,
u32 * const bin_count)
{
const TIMER_T start_time = get_time();
for (u32 src_idx=0; src_idx<num_elements; src_idx++)
```