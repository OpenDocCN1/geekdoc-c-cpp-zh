![](bbox=[0.24, 0.11, 0.77, 0.35])

# FIGURE 6.12 Final stages of GPU parallel reduction.

```
// Uses multiple threads for reduction type merge
__device__ void merge_array(const u32 * const src_array,
                            u32 * const dest_array,
                            const u32 num_lists,
                            const u32 num_elements,
                            const u32 tid)
{
    const u32 num_elements_per_list = (num_elements / num_lists);

    __shared__ u32 list_indexes[MAX_NUM_LISTS];
    __shared__ u32 reduction_val[MAX_NUM_LISTS];
    __shared__ u32 reduction_id[MAX_NUM_LISTS];

    // Clear the working sets
    list_indexes[tid] = 0;
    reduction_val[tid] = 0;
    reduction_id[tid] = 0;
    __syncthreads();

    for (u32 i=0; i<num_elements;i++)
    {
        // We need (num_lists / 2) active threads
        u32 tid_max = num_lists >> 1;

    u32 data;

    // If the current list has already been
    // emptied then ignore it
```