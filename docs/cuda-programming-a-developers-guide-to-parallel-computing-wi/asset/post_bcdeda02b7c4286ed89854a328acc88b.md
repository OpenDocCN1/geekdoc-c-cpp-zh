
```
num_threads, (num_elem / 2));

// Invoke the kernel
odd_even_sort_ptr_kernel_gmem<<<num_blocks, num_threads>>>(data_gpu, num_elem);

cuda_error_check("Error Invoking kernel*",
        "odd_even_sort_gpu_kernel_gmem");

// Copy back to CPU memory space
CUDA_CALL(cudaMemcpy(data_cpu, data_gpu, size_in_bytes, cudaMemcpyDeviceToHost));

// Free memory on the device
CUDA_CALL(cudaFree(data_gpu));

print_array(0, data_cpu, num_elem);
```

One question that should be in your mind about this code is what happens at the block boundaries. Let's look at the results with one and two blocks with a dataset small enough to print here:

```
Invoking Odd Even sort with 1 blocks of 8 threads (8 active)
Run 000: 00 01 02 03 04 05 06 07 08 09 10 11 12 13 14 15
Test passed

and

Invoking Odd Even sort with 2 blocks of 4 threads (8 active)
Run 000: 08 09 10 11 12 13 14 15 00 01 02 03 04 05 06 07
Test failed
```

Notice in the second output the sort occurred only within the block. The values on the right needed to propagate to the left and vice versa. However, as the blocks do not overlap, they are not able to do this. The obvious solution would be to overlap the blocks, but this would not be an ideal solution.

CUDA was designed to allow blocks to run in any order, without a means for cross-block synchronization within a single kernel run. It is possible by issuing multiple kernels to synchronize between blocks, but this mechanism works well only where you have a small number of synchronization steps. In this kernel we'd need to overlap the blocks on every iteration. This would lose all locality, as now two SMs need to share the same dataset. We also need a global memory atomic or a reduction operation to keep track of whether any blocks performed a swap and have to continue issuing kernels until no swaps had taken place in any block—a lot of host interaction. That would not be a good route to go down.

So we're left with the two choices found in most sorts that decompose into blocks. Either presort the input lists so the values in list N<sub>i-1</sub> are less than N<sub>0</sub>, which are larger than N<sub>1</sub>, the solution we used with the sample sort, or merge N separate lists, the merge sort problem we also looked at earlier.

## Reduction

Reduction is used significantly in parallel programming. We'll look at some of the many ways we can perform a reduction to see which method produces the best results on the various compute platforms and to understand why.

We'll look first at computing the sum of _N_ 32-bit integers, some 48 million to give a reasonable sized dataset. With such a large number of values one of the first issues we need to consider is overflow. If we add 0xFFFFFFFF and 0x00000001 then we have an overflow condition with a 32-bit number. Therefore, we need to accumulate into a 64-bit number. This presents some issues. First, any atomic-based accumulation would require an atomic 64-bit integer add. Unfortunately, this is supported in shared memory only with compute 2.x hardware and in global memory only in compute 1.2 hardware onward.

## Global atomic add

Let's look first at the simplest form of reduction:

```
// Every thread does atomic add to the same
// address in GMEM
__global__ void reduce_gmem(const uint32 * const data,
u64 * const result,
const uint32 num_elements)
{
    const uint32 tid = (blockIdx.x * blockDim.x) + threadIdx.x;
    if (tid < num_elements)
        atomicAdd(result, (u64) data[tid]);
}
```

In this first example, each thread reads a single element from memory and adds it to a single result in global memory. This, although very simple, is probably one of the worst forms of a reduce operation. The interblock atomic operation means the value needs to be shared across all of the SMs.

In the older hardware this means physically writing to global memory. In the compute 2.x hardware this means maintaining an L2 cache entry, shared among all the SMs, and eventually writing this to global memory. The results we see are as follows:

| | ID:0 GeForce GTX 470:GMEM passed Time | ID:3 GeForce GTX 460:GMEM passed Time |
|---|---|---|
| Processing 48 MB of data, 12M elements | 197.84 ms | 164.28 ms |

We'll look here at the compute 2.x devices, as these support 64-bit integer atomics.

The issue with the atomic writes, even to L2 cache, is they force a serialization of the threads. We have six blocks in each SM, 256 threads per block, generating 1536 threads per SM. On the GTX470 we have 14 SMs, so a total of 21,504 active threads. On the GTX460 we have 7 SMs, so a total of 10,752 active threads. Performing an atomic operation on a single global memory cell means we create a lineup, or serialization, of 10 K to 21 K threads. Every thread has to queue, once for every single element it processes. Clearly a poor solution, even if it is a somewhat simple one.

## Reduction within the threads

We can improve this situation by performing some of the reduction within the thread. We can do this very simply by changing the data type and adjusting the kernel to ensure we don't go out of bounds.

```
// Every thread does atomic add to the same
// address in GMEM
__global__ void reduce_gmem_ILP2(const uint2 * const data,
u64 * const result,
const u32 num_elements)
{
const u32 tid = (blockIdx.x * blockDim.x) + threadIdx.x;

if (tid < (num_elements>>1))
{
uint2 element = data[tid];

const u64 add_value = ((u64)element.x) +
((u64)element.y);

atomicAdd(result, add_value);
}
}
```

```
// Every thread does atomic add to the same
// address in GMEM
__global__ void reduce_gmem_ILP4(const uint4 * const data,
u64 * const result,
const u32 num_elements)
{
const u32 tid = (blockIdx.x * blockDim.x) + threadIdx.x;

if (tid < (num_elements>>2))
{
uint4 element = data[tid];

const u64 add_value = ((u64)element.x) +
((u64)element.y) +
((u64)element.z) +
((u64)element.w);

atomicAdd(result, add_value);
}
}
```

In the first example we process two elements per thread and four in the second using the built-in vector types uint2 and uint4. This produces the following timings:

- ID:0 GeForce GTX 470:GMEM ILP2 passed Time 98.96 ms
- ID:3 GeForce GTX 460:GMEM ILP2 passed Time 82.37 ms
- ID:0 GeForce GTX 470:GMEM ILP4 passed Time 49.53 ms
- ID:3 GeForce GTX 460:GMEM ILP4 passed Time 41.47 ms

Although, a dramatic reduction, we've not really solved the problem. All we have done is to half or quarter the number of times each thread has to queue by performing a local reduction. This drops the overall time to approximately one-half and one-quarter of the original. However, there is still a 5 K thread lineup trying to write to the global memory.

Note in performing the addition locally, we reduce the number of global writes by a factor equal to the level of ILP. However, we have to be careful about how the addition is performed. You could write:

```
const u64 add_value = ((u64)element.x) + element.y + element.z + element.w;
```

In C, an expression is typically evaluated from left to right. A promotion of the left operator generates an implicit promotion of the right operator. Thus, you might expect element.x to be promoted to an unsigned 64-bit type, and as element.y is to be added to it, it will also be promoted. As element.z and element.w will subsequently be added, you might also expect these to be promoted. You are, however, thinking like a serial programmer. The z and w elements can be calculated independently of x and y. This is exactly what the PTX code does. As neither z nor w has been promoted to a 64-bit value, the addition is done as a 32-bit addition, which may result in an overflow.

The problem lies in that C permits any order of evaluation where the operator is commutative. However, as you typically see a left to right evaluation, people assume this is how all compilers work. This is one of the portability issues between C compilers. When we move to a superscalar processor such as a GPU, it performs the two sets of additions independently to make the maximum use of the pipeline. We don't want it to wait 18–22 plus cycles for the first addition to complete then make the subsequent additions in series.

Thus, the correct way to write such additions is:

```
const u64 add_value = ((u64)element.x) + ((u64)element.y) + ((u64)element.z) + ((u64)element.w);
```

Here every value is converted to a 64-bit number before the addition takes place. Then any ordering of the addition is fine for integer values. Note for floating-point values simply converting to doubles is not enough. Due to the way floating-point numbers work adding a very tiny number to a very large number will result in the small number being discarded, as the floating-point notation does not have the required resolution to hold such values. The best approach to this type of problem is to first sort the floating-point values and work from the smallest number to the largest.

We can take the ILP technique a little further by using multiple elements of uint4 and adjusting the kernel accordingly.

```
// Every thread does atomic add to the same
// address in GMEM
__global__ void reduce_gmem_ILP8(const uint4 * const data,
u64 * const result,
const u32 num_elements)
{
    const u32 tid = (blockIdx.x * blockDim.x) + threadIdx.x;
    if (tid < (num_elements>>3))
    {
        const u32 idx = (tid * 2);
        uint4 element = data[idx];
        u64 value = ((u64)element.x) +
```
