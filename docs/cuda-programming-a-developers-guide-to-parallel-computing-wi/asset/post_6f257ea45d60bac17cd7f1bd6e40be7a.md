
```cpp
const u32 num_samples,
const u32 num_elements,
u32 * const data,
const u32 * const sample_data,
const u32 * const bin_count,
const u32 * const dest_bin_idx,
u32 * const sort_tmp,
const u32 num_threads,
const char * prefix
{
start_device_timer();

const u32 num_blocks = num_samples / num_threads;

sort_bins_gpu_kernel3<<<(num_blocks, num_threads)>>>(num_samples, num_elements, data,
sample_data, bin_count, dest_bin_idx, sort_tmp);

cuda_error_check(prefix, "Error invoking sort_bins_gpu_kernel");

const TIMER_T func_time = stop_device_timer();
return func_time;
}
```

We use a host function to invoke num_samples threads that are split into blocks depending on the number of threads requested per block.

```cpp
__global__ void sort_bins_gpu_kernel3(
const u32 num_samples,
const u32 num_elements,
u32 * const data,
const u32 * const sample_data,
const u32 * const bin_count,
const u32 * const dest_bin_idx,
u32 * const sort_tmp,
)
// Calculate the thread we're using
const u32 tid = (blockIdx.x * blockDim.x) + threadIdx.x;

if (tid != (num_samples-1))
radix_sort(data, dest_bin_idx[tid], dest_bin_idx[tid+1], sort_tmp);
else
radix_sort(data, dest_bin_idx[tid], num_elements, sort_tmp);
}
```

The kernel is a two-level kernel, as the array dest_bin_idx holds only the start index. For the last element, accessing [tid+1] would cause an array overflow issue, so the very last thread needs to be handled slightly differently.

Sorting the multiple blocks is done with a modified version of the radix_sort kernel we developed in Chapter 5.

```cpp
__device__ void radix_sort(
u32 * const data,
const u32 start_idx,
const u32 end_idx,
u32 * const sort_tmp)
{
// Sort into num_list, lists
// Apply radix sort on 32 bits of data
for (u32 bit=0; bit<32; bit++)
{
// Mask off all but the bit we're interested in
const u32 bit_mask = (1u << bit);
// Set up the zero and one counter
u32 base_cnt_0 = start_idx;
u32 base_cnt_1 = start_idx;
for (u32 i=start_idx; i<end_idx; i++)
{
// Fetch the test data element
const u32 elem = data[i];
// If the element is in the one list
if ((elem & bit_mask) > 0u)
{
// Copy to the one list
sort_tmp[base_cnt_1++] = elem;
}
else
{
// Copy to the zero list (inplace)
data[base_cnt_0++] = elem;
}
}
// Copy data back to source from the one's list
for (u32 i=start_idx; i<base_cnt_1; i++)
{
data[base_cnt_0++] = sort_tmp[i];
}
}
```

The radix sort simply iterates over the dataset it has been provided for a given block. For each bit it places the value into either the 0 or 1 list. The caller defines the start and end indexes of the array over which the sort will take place.

## Analyzing the results

With a sample size of 16 K and a source dataset size of 1 MB we see the following results on a mostly sorted list:

```
ID:3 GeForce GTX 460: Test 32 - Selecting 16384 from 1048576 elements using 512 blocks
of 32 threads
Select Sample Time - CPU: 0.19 GPU:0.03
Sort Sample Time - CPU: 2.13 GPU:125.57
Count Bins Time - CPU: 157.59 GPU:17.00
Calc. Bin Idx Time - CPU: 0.03 GPU:0.58
Sort to Bins Time - CPU: 163.81 GPU:16.94
Sort Bins Time - CPU: 72.06 GPU:64.46
Total Time - CPU: 395.81 GPU:224.59
Qsort Time - CPU: 185.41 GPU:N/A
```

```
ID:3 GeForce GTX 460: Test 32 - Selecting 16384 from 1048576 elements using 256 blocks
of 64 threads
Select Sample Time - CPU: 0.53 GPU:0.03
Sort Sample Time - CPU: 2.06 GPU:125.57
Count Bins Time - CPU: 157.75 GPU:19.07
Calc. Bin Idx Time - CPU: 0.13 GPU:0.26
Sort to Bins Time - CPU: 164.09 GPU:19.09
Sort Bins Time - CPU: 72.31 GPU:62.11
Total Time - CPU: 396.88 GPU:226.13
Qsort Time - CPU: 184.50 GPU:N/A
```

```
ID:3 GeForce GTX 460: Test 32 - Selecting 16384 from 1048576 elements using 128 blocks
of 128 threads
Select Sample Time - CPU: 0.28 GPU:0.03
Sort Sample Time - CPU: 2.09 GPU:125.57
Count Bins Time - CPU: 157.91 GPU:13.96
Calc. Bin Idx Time - CPU: 0.09 GPU:0.26
Sort to Bins Time - CPU: 164.22 GPU:14.00
Sort Bins Time - CPU: 71.19 GPU:91.33
Total Time - CPU: 395.78 GPU:245.16
Qsort Time - CPU: 185.19 GPU:N/A
```

```
ID:3 GeForce GTX 460: Test 32 - Selecting 16384 from 1048576 elements using 64 blocks of
256 threads
Select Sample Time - CPU: 0.22 GPU:0.03
Sort Sample Time - CPU: 2.00 GPU:125.57
Count Bins Time - CPU: 158.78 GPU:12.43
Calc. Bin Idx Time - CPU: 0.13 GPU:0.49
Sort to Bins Time - CPU: 164.38 GPU:12.39
Sort Bins Time - CPU: 71.16 GPU:84.89
Total Time - CPU: 396.66 GPU:235.80
Qsort Time - CPU: 186.13 GPU:N/A
```

Notice how the entire sort process (224-245 ms) is dominated by the sorting of the sample dataset on the GPU (~125 ms). As the sample dataset becomes large the sort-and-merge approach used for this phase doesn't work well.

One solution to this problem would be to run the sample sort on the sample data; where the sample dataset is large, this is a good approach. However, for a 16 K sample set, it takes around 9 ms to run the sample sort compared with a 2 ms quick sort time from the CPU.

It always makes sense to use whichever device works best at a given solution. For small sample sizes, the CPU will usually be faster than the GPU. The GPU requires reasonably sized datasets, after which point it easily surpasses the CPU. Therefore, the optimal solution is simply to run quick sort on the sample set on the CPU and then transfer this to the GPU for the large-scale parallel "grunt" work of the sorting.

When we use this approach the timings drop significantly.

```
Id:3 GeForce GTX 460: Test 32 - Selecting 16384 from 1048576 elements using 512 blocks
of 32 threads
Select Sample Time - CPU: 0.09 GPU:0.09
Sort Sample Time - CPU: 2.09 GPU:2.09
Count Bins Time - CPU: 157.69 GPU:17.02
Calc. Bin Idx Time - CPU: 0.09 GPU:0.58
Sort Bins Time - CPU: 163.78 GPU:16.94
Sort Bins Time - CPU: 71.97 GPU:64.47
Total Time - CPU: 395.72 GPU:101.19
Qsort Time - CPU: 184.78 GPU:N/A
```

You can see the sample sort time is around 55% of the time of the quick sort on the CPU with a 16 K sample size (101 ms GPU, 185 ms CPU). If we vary the sample size, we increase the amount of available parallelism in the problem. See Table 6.15 and Figure 6.26.

What you can see from Table 6.15 and Figure 6.26 is that as the number of samples increases, the time drops dramatically. The best time is achieved for the GTX460 at 128K samples, or one-eighth of the number of the data to be sorted. The GTX470, with its much larger number of SMs, starts to rapidly outperform the GTX460 from 2048 sample points onward. The GTX260 by comparison (the previous generation of hardware) needs many more sample points to come close to the Fermi performance.

At 128K sample points the sorting of the samples again becomes significant (see Table 6.16) and our strategy of using quick sort on the CPU becomes the bottleneck. If we look in detail at the results from the GTX470, we see that at 256K sample points up to 50% of the time is spent sorting the sample data. At this point a sample sort of the sample data becomes a good option (Table 6.16).

| Device/Samples | 256 | 512 | 1024 | 2048 | 4096 | 8K | 16K | 32K | 64K | 128K | 256K |
|---|---|---|---|---|---|---|---|---|---|---|---|
| Qsort | 184 | 184 | 184 | 184 | 184 | 184 | 184 | 184 | 184 | 184 | 184 |
| GTX460 | 506 | 273 | 158 | 151 | 115 | 105 | 101 | 101 | 69 | 64 | 85 |
| GTX470 | 546 | 290 | 161 | 94 | 91 | 72 | 62 | 60 | 43 | 46 | 68 |
| GTX260 | 1082 | 768 | 635 | 485 | 370 | 286 | 215 | 190 | 179 | 111 | 88 |

![](img/e0b192dbaf05f61ad420bee512a8c4e4_212_0.png)

FIGURE 6.26
Graph of sample sort results.

| Operation/Samples | 256 | 512 | 1024 | 2048 | 4096 | 8K | 16K | 32K | 64K | 128K | 256K |
|---|---|---|---|---|---|---|---|---|---|---|---|
| Select samples | 0 | 0.03 | 0 | 0.09 | 0.06 | 0.28 | 0.5 | 0.5 | 0.84 | 0.97 | 1.78 |
| Sort samples | 0 | 0.06 | 0.6 | 0.28 | 0.38 | 0.97 | 2.03 | 4.34 | 9.38 | 19.72 | 41.72 |
| Count bins | 14.6 | 14.2 | 13.62 | 12.38 | 10.66 | 9.34 | 9.26 | 8.38 | 6.03 | 5.35 | 5.38 |
| Prefix sum | 0.13 | 0.27 | 0.53 | 1.05 | 0.19 | 0.33 | 0.62 | 1.2 | 0.57 | 0.87 | 1.46 |
| Sort to bins | 14.6 | 14.2 | 13.65 | 12.4 | 10.7 | 9.37 | 9.33 | 8.45 | 6.09 | 5.41 | 5.46 |
| Sort bins | 517 | 261 | 133.5 | 68.29 | 69.86 | 52.5 | 40.9 | 37.2 | 20.2 | 13.94 | 12.15 |
| Total | 546 | 290 | 162 | 94 | 92 | 73 | 63 | 60 | 43 | 46 | 68 |

To give some comparison with almost sorted data versus entirely random data, we'll run the same test over a random dataset (Table 6.17). Various tests have shown the best performance was achieved with 128 threads per block.

As you can see from Table 6.17 the faster run was the GTX470 at 67 ms. This is five times faster than the serial quick sort on the CPU host. Around 32 K samples with 128 threads per block would appear to be the optimal launch configuration for 1 MB of data. See Figure 6.27.

## Questions on global memory

- 1. Discuss the reasons why sample sort is quicker when the list is mostly sorted?
- 2. How might you improve the sample sort algorithm presented here?
- 3. Do you foresee any problems using larger dataset sizes? What might you have to change to run larger datasets?
