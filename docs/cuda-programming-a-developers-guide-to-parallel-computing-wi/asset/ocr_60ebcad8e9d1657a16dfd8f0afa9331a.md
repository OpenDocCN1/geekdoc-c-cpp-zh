```
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