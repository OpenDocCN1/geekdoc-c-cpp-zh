Sorting the multiple blocks is done with a modified version of the radix_sort kernel we developed in Chapter 5.

```
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