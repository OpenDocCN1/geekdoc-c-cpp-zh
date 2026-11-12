```
```cpp
if (list_indexes[tid] < num_elements_per_list)
{
// Work out from the list_index, the index into
// the linear array
const u32 src_idx = tid + (list_indexes[tid] * num_lists);

// Read the data from the list for the given
// thread
data = src_array[src_idx];
}
else
{
data = 0xFFFFFFFF;
}

// Store the current data value and index
reduction_val[tid] = data;
reduction_idx[tid] = tid;

// Wait for all threads to copy
__syncthreads();

// Reduce from num_lists to one thread zero
while (tid_max != 0)
{
// Gradually reduce tid_max from
// num_lists to zero
if (tid < tid_max)
{
// Calculate the index of the other half
const u32 val2_idx = tid + tid_max;

// Read in the other half
const u32 val2 = reduction_val[val2_idx];

// If this half is bigger
if (reduction_val[tid] > val2)
{
// The store the smaller value
reduction_val[tid] = val2;
reduction_idx[tid] = reduction_idx[val2_idx];
}
}

// Divide tid_max by two
tid_max >>= 1;

__syncthreads();
}
```
```