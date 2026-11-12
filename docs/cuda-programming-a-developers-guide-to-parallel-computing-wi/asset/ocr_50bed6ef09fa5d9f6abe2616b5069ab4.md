```
const u32 num_elements)
{
// Take the middle of the two sections
u32 size = (num_elements >> 1);
u32 start_idx = 0;
bool found = false;
do
{
    const u32 src_idx = (start_idx+size);
    const u32 test_value = src_data[src_idx];
    if (test_value == search_value)
        found = true;
    else
        if (search_value >> test_value)
            start_idx = (start_idx+size);
    if (found == false)
        size >>= 1;
} while ( (found == false) && (size != 0) );
return (start_idx + size);
}
```

The binary search routine works by reducing the size parameter to zero. It returns the index or the bin in which the search value should be placed.

```
// Single data point, atomic add to gmem
__global__ void count_bins_gpu_kernel5(
    const u32 num_samples,
    const u32 * const src_data,
    const u32 * const sample_data,
    u32 * const bin_count)
{
    const u32 tid = (blockIdx.x * blockDim.x) + threadIdx.x;
    // Read the sample point
    const u32 data_to_find = src_data[tid];
    // Obtain the index of the element in the search list
    const u32 idx = bin_search(sample_data, data_to_find, num_samples);
    atomicAdd(&bin_count[idx],1);
}
__host__ TIMER_T count_bins_gpu(
```