
multiple blocks interact. As it happens, shared memory is the main factor we need to consider limiting the number of blocks we're likely to be able to put into each SM.

If you look at the initial radix sort function, it is not very efficient. How would you optimize this function? The most obvious change is that you do not need separate 0 and 1 lists. The 0 list can be created from reusing the space in the original list. This not only allows you to discard the 1 list, but also removes a copy back to the source list. This saves a lot of unnecessary work.

Finally, did you notice that the bit mask is actually constant within a single iteration of the bit loop? It is thus an invariant within the i loop and can be moved out to the bit loop. This is a standard compiler optimization called invariant analysis. Most compilers would move this outside the i loop. Compiler optimization is notoriously badly documented and can change from one compiler to another and even between versions of compilers. Relying on optimization steps of compilers is therefore, generally, bad programming practice and best avoided. Therefore, we'll explicitly move the calculation to ensure it gets executed in the correct place. See Chapter 9 on optimization for coverage of typical compiler optimizations.

The slightly optimal code we end up with is as follows:

```
__device__ void radix_sort2(u32 * const sort_tmp,
    const u32 num_lists,
    const u32 num_elements,
    u32 * const sort_tmp_1)
{
    // Sort into num_lists lists
    // Apply radix sort on 32 bits of data
    for (u32 bit=0;bit<32;bit++)
    {
        const u32 bit_mask = (1 << bit);
        u32 base_cnt_0 = 0;
        u32 base_cnt_1 = 0;

        for (u32 i=0; i<num_elements; i+=num_lists)
        {
            const u32 elem = sort_tmp[i+tid];

            if ( (elem & bit_mask) > 0 )
            {
                sort_tmp_1[base_cnt_1+tid] = elem;
                base_cnt_1+=num_lists;
            }
            else
            {
                sort_tmp[base_cnt_0+tid] = elem;
                base_cnt_0+=num_lists;
            }
        }
    }
// Copy data back to source from the 1's list
    for (u32 i=0; i<base_cnt_1; i+=num_lists)
    {
        sort_tmp[base_cnt_0+i+tid] = sort_tmp[i+tid];
    }
    __syncthreads();
}
```

There are further optimizations that can be made, but the key issue here is that we're now using only one temporary storage area, which in turn allows the processing of more elements. This is important because, as we'll see later, the number of lists is an important factor. So how do these changes affect the performance of the radix sort?

If you look at Table 6.7, you'll see the worst case, using a single thread, has come down from 82 ms to 52 ms. The best case in the previous run, 0.26 ms, has come down to 0.21 ms, which is about a 20% improvement in execution speed.

| Device/Threads | 1 | 2 | 4 | 8 | 16 | 32 | 64 | 128 | 256 |
|---|---|---|---|---|---|---|---|---|---|
| GTX470 | 26.51 | 14.35 | 7.65 | 3.96 | 2.05 | 1.09 | 0.61 | 0.36 | 0.24 |
| 9800GT | 42.8 | 23.22 | 12.37 | 6.41 | 3.3 | 1.78 | 0.98 | 0.63 | 0.4 |
| GTX260 | 52.54 | 28.46 | 15.14 | 7.81 | 4.01 | 2.17 | 1.2 | 0.7 | 0.46 |
| GTX460 | 21.62 | 11.81 | 6.34 | 3.24 | 1.69 | 0.91 | 0.51 | 0.31 | 0.21 |

## Merging lists

Merge lists of sorted elements is another algorithm that is commonly used in parallel programming. However, let's start by looking at some serial code to merge an arbitrary number of sorted lists into a single sorted list, as this is the simplest case.

```
void merge_array(const u32 * const src_array,
                 u32 * const dest_array,
                 const u32 num_lists,
                 const u32 num_elements)
{
    const u32 num_elements_per_list = (num_elements / num_lists);
    u32 list_indexes[MAX_NUM_LISTS];
    for (u32 list=0; list < num_lists; list++)
    {
        list_indexes[list] = 0;
    }
    for (u32 i=0; i<num_elements;i++)
    {
        dest_array[i] = find_min(src_array,
                                 list_indexes,
                                 num_lists,
                                 num_elements_per_list);
    }
}
```

Assuming there are num_lists lists to collect data from, you need some way to track where we are in the list. The program uses the array list_indexes for this. As the number of lists is likely to be small, you can use the stack and thus declare the array as a local variable. Note this would be a bad idea with a GPU kernel, as the stack allocation may get placed into slow global memory, depending on the particular GPU variant. Shared memory would likely be the optimal location on the GPU, depending on the number of lists needed.

![](img/e0b192dbaf05f61ad420bee512a8c4e4_146_0.png)

FIGURE 6.9 Multiple lists partially merged.

First, the index values are all set to zero. Then the program iterates over all elements and assigns the value in the sorted array from the result of a function, find_min. The find_min function identifies the smallest value from a set of num_lists values.

```
u32 find_min(const u32 * const src_array,
             u32 * const list_indexes,
             const u32 num_lists,
             const u32 num_elements_per_list)
{
    u32 min_val = 0xFFFFFFFF;
    u32 min_idx = 0;

    // Iterate over each of the lists
    for (u32 i = 0; i < num_lists; i++)
    {
        // If the current list has already been emptied
        // then ignore it
        if (list_indexes[i] < num_elements_per_list)
        {
            const u32 src_idx = i + (list_indexes[i] * num_lists);
            const u32 data = src_array[src_idx];

            if (data < min_val)
            {
                min_val = data;
                min_idx = i;
            }
        }
    }

    list_indexes[min_idx]++;
    return min_val;
}
```

The function works by iterating through the lists of sorted values and maintaining an index into where it is in each list. If it identifies a smaller value than min_val, it simply updates min_val to this new value. When it has scanned all the lists, it increments the relevant list index and returns the value it found.

Now let's look at the GPU implementation of this algorithm. First, the top-level function:

```
__global__ void gpu_sort_array_array(
    u32 * const data,
    const u32 num_lists,
    const u32 num_elements)
{
    const u32 tid = (blockIdx.x * blockDim.x) + threadIdx.x;

    __shared__ u32 sort_tmp[NUM_ELEM];
    __shared__ u32 sort_tmp_l[NUM_ELEM];

    copy_data_to_shared(data, sort_tmp, num_lists,
        num_elements, tid);

    radix_sort2(sort_tmp, num_lists, num_elements,
        tid, sort_tmp_l);

    merge_array6(sort_tmp, data, num_lists,
        num_elements, tid);
}
```

This is quite a simple program for now. It will be invoked with a single block of N threads. We'll develop this as an example of how to use shared memory. Looking at the first function, we see the following:

```
__device__ void copy_data_to_shared(const u32 * const data,
    u32 * const sort_tmp,
    const u32 num_lists,
    const u32 num_elements,
    const u32 tid)
{
    // Copy data into temp store
    for (u32 i = 0; i < num_elements; i += num_lists)
    {
        sort_tmp[i + tid] = data[i + tid];
    }
    __syncthreads();
}
```

Here the program reads data from global memory in rows and not columns into the shared memory. This step is important for two reasons. First, the program will repeatedly read and write from this memory. Therefore, you want the fastest store possible, so we need to use shared memory instead of global memory. Second, global memory provides the best performance when accessed by rows. Column access produces a scattered memory pattern that the hardware is unable to coalesce, unless every thread accesses the same column value and these addresses are adjacent. Thus, in most cases the GPU has to access far more memory fetch operations than are necessary and the speed of the program will drop by an order of magnitude.

When you compile this program, if you have the -v flag set on the nvcc compiler options, it will print an innocent looking message saying it created a stack frame. For example,

```
1>ptxas info : Function properties for _Z12merge_arrayPKjPjjjj
> 40 bytes stack frame, 40 bytes spill stores, 40 bytes spill loads
```

When a function makes a call into a subfunction and passes parameters, those parameters must somehow be provided to the called function. The program makes just such a call:

```
dest_array[i] = find_min(src_array.
```
