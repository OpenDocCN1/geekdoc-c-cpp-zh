
end of the source data. We neither want to read or write out-of-bounds arrays, so this check is necessary.

Note that this also implicitly means we cannot perform a __syncthreads operation within this if block, as all threads, even those off the end of the array, must participate in such a synchronization operation.

```
// Have the first thread of every warp
// clear the shared memory entry
if ((threadIdx.x % WARP_SIZE) == 0)
{
    warp_shared_ballot[warp_num] = 0;
}
```

Next we have to clear the value of the shared memory we're about to use. Shared memory can hold the value from the last kernel run and is not implicitly initialized to zero. As we need only a single writer, the first thread in each warp clears the value. Note we do not require any synchronization here because the first thread in every warp does the write. Branching within a warp in this way causes the other threads to implicitly wait at the end of the if statement.

```
// Call __ballot to set the N'th bit in the word
// with a warp if the predicate is true
// OR the bits from all threads in the warp into
// one value per warp held in shared memory
atomicOr( &warp_shared_ballot[warp_num],
_ballot_non_atom( predicate_func(data[tid], threshold)) );
```

We can now have every thread in every active warp call the atomicOr function with the address of the shared memory element for this current warp. We pass to the OR operation the value returned from the __ballot call. We pass to __ballot the return value from the calling predicate_func function pointer, passing it the two data items to evaluate. This then jumps off and does the evaluation, in this case calling the predicate_gt function defined earlier.

```
// Wait for all warps to complete
__syncthreads();
```

Now we have to wait for all warps within the block to execute before we can do the second part, the block level accumulate.

```
// From the first warp, activate up to 32 threads
// Actual number of threads needed is the number
// warps in the block
// All other threads drop out at this point
if (threadIdx.x < number_of_warps)
{
```

As the maximum number of threads per block is 1024, the maximum number of warps per block is 32 (1024 / 32 = 32). Thus, we can process the accumulate using just a single warp. We could have used thread 0 from each warp as we did before, but in this case we want the other warps to complete, not be left executing a single thread each.

```
// Have thread zero, zero the accumulator
if (threadIdx.x == 0)
{
    block_shared_accumulate = 0;
}
```

Again we have no idea of the existing value in the shared memory element we're about to use to accumulate into, so we need to zero it. Note that, as we now have only one warp running, no synchronization is required. Thread 0 will enter the condition while threads 1...31 will pass over it and implicitly wait for thread 0 to recover with them.

```
// Add to the single accumulator the number
// of bits set from each warp.
// Max threads equals number of warps
// which is typically 8 (256 threads), but
// max 32 (1024 threads)
atomicAdd(&block_shared_accumulate,
__popc(warp_shared_ballot[threadIdx.x]));
```

We now add to the block-based shared memory accumulator the number of bits that were set in the result produced for the other warps in the block. These are in adjacent elements of shared memory, one element per warp. Thus, there are no read shared memory bank conflicts. However, the threads need to serialize the writes to the accumulator to ensure correctness. As you typically have 256 threads per block, this gives eight warps. This serialization does not really warrant a parallel-type reduction. However, with a larger number of warps a parallel reduction might work slightly faster.

```
// No sync is required as only warp zero
// accumulates
// Have thread zero write out the result
if (threadIdx.x == 0)
{
```

As we need only one writer, we select thread 0 to perform the next operation.

```
// Read from SMEM the result for the block
const u32 block_result = block_shared_accumulate;
// Store the value for the block
block_results[blockIdx.x] = block_result;
// Add the value into GMEM total for all blocks
atomicAdd( gmem_accum, block_result );
```

Finally, we read the block level accumulator from shared memory into a register, as we'll make use of it twice. We then write the block result to global memory, something we only have to do if we're interested in the block results in addition to the overall accumulated result.

We then call the atomicAdd function to add into the single global accumulator the overall result. Note that we cannot zero the result of the final accumulator in any of the blocks. It must be done by the host prior to the call to the function. The reason for this is simple. The blocks, and the warps within those blocks, may execute in any order. Thus, we cannot say something like if (threadIdx.x == 0) && (blockIdx.x == 0) then zero the accumulator. Doing this may work because it just so happens that warp 0 of block 0 executed first, but this is poor practice. CUDA's execution model is such that blocks can be, and are, executed out of order. You cannot assume any implicit order of block execution.

With a minor modification to supply the missing _ballot function for the GTX 260 (a compute 1.3 device), we can run this kernel on a range of devices. Note we can't use the 9800GT as it's a compute 1.1 device and therefore does not support shared memory based atomic operations.

Processing 48 MB of data, 12M elements

| Device | Status | Time |
|---|---|---|
| ID:0 GeForce GTX 470 | GPU Reduction Passed | 8.34 ms |
| ID:2 GeForce GTX 260 | GPU Reduction Passed | 12.49 ms |
| ID:3 GeForce GTX 460 | GPU Reduction Passed | 17.35 ms |

What is perhaps strange at first glance is that the GTX260 is 50% faster than the more modern GTX460. However, the GTX260 has approximately four times the number of SMs. Each SM has its own internal set of shared memory so the GTX260 has a much wider bandwidth to the shared memory than the GTX460.

We can also make one small modification. As we're using the atomicOr function we actually don't need the additional atomicity of __ballot, so we can in all cases use the nonatomic version. This revises the timing a little.

Processing 48 MB of data, 12M elements

| Device | Status | Time |
|---|---|---|
| ID:0 GeForce GTX 470 | GPU Reduction Passed | 7.35 ms |
| ID:2 GeForce GTX 260 | GPU Reduction Passed | 12.53 ms |
| ID:3 GeForce GTX 460 | GPU Reduction Passed | 14.11 ms |

Result: 8742545

You can see that this drops the time significantly on Fermi devices, as the GTX260 is already using the nonatomic version. The time for the GTX470 is reduced by 15% and the time for the GTX460 is reduced by 21%. This slightly improved time allows us to scan some 1632 million elements per second on a single GTX470. This will, however, be reduced if we use more complex predicates and/or a dataset requiring more than one block dimension.

To get a feel for this, what happens to the timing if we change the results to within a boundary, rather than simply larger than a threshold? For this we need to modify the predicate condition as follows:

```
__device__ int predicate_within(const u32 a,
        const u32 b,
        const u32 c)
{
    return ( (a > b) && (a < c) );
}
```

Thus, we have introduced another condition, potentially increasing significantly the overall timing. What is the effect in practice?

Processing 48 MB of data, 12M elements

| Device | Status | Time |
|---|---|---|
| ID:0 GeForce GTX 470 | GPU Reduction Passed | 7.49 ms |
| ID:2 GeForce GTX 260 | GPU Reduction Passed | 12.62 ms |
| ID:3 GeForce GTX 460 | GPU Reduction Passed | 14.23 ms |

Result: 7679870

You can see that the effect of adding another condition is marginal at best, with a 0.1 ms difference in execution time. This would imply the predicate could become reasonably complex without causing a significant slowdown.

The fact that we can use very complex predicate conditions allows for very complex operations to be coded efficiently on a GPU. Even codes where the data points must be gathered in some way can use such a set of primitives. All we need to do in such cases is adjust the predicate to take more data.

## PROFILING

We'll pick up the example we looked at in Chapter 6, sample sort, and use it to look at how we can use profiling tools to identify problems in the implementation of a given algorithm.

The sample sort example already contains a number of timing elements, which we can use to adjust various parameters. Please re-read the sample sort example in Chapter 6 if you're not familiar with how sample sort works.

The major parameters are the number of samples and the number of threads. If we ask the program to explore the possible search space, doubling the number of samples per iterations and using 32, 64, 128, or 256 threads, we find the following promising cases.

ID:0 GeForce GTX 470: Test 16 - Selecting 16384 from 1048576 elements using 64 blocks of 256 threads

Num Threads: 32 64 128 256

| Metric | CPU | 32 threads | 64 threads | 128 threads | 256 threads |
|---|---|---|---|---|---|
| Select Sample Time | 0.56 | 0.56 | 0.19 | 0.06 | 0.56 |
| Sort Sample Time | 5.06 | 5.06 | 5.06 | 5.06 | 5.06 |
| Count Bins Time | 196.88 | 7.28 | 4.80 | 5.06 | 4.47 |
| Calc. Bin Idx Time | 0.13 | 1.05 | 0.71 | 0.70 | 0.98 |
| Sort to Bins Time | 227.56 | 7.63 | 4.85 | 4.62 | 4.49 |
| Sort Bins Time | 58.06 | 64.77 | 47.88 | 60.58 | 54.51 |
| Total Time | 488.25 | 86.34 | 63.49 | 75.61 | 69.88 |
| QSORT Time | 340.44 | | | | |

ID:0 GeForce GTX 470: Test 16 - Selecting 32768 from 1048576 elements using 128 blocks of 256 threads

Num Threads: 32 64 128 256

| Metric | CPU | 32 threads | 64 threads | 128 threads | 256 threads |
|---|---|---|---|---|---|
| Select Sample Time | 0.63 | 0.63 | 0.63 | 0.75 | 0.38 |
| Sort Sample Time | 10.88 | 10.88 | 11.06 | 10.63 | 10.69 |
| Count Bins Time | 222.19 | 7.85 | 5.51 | 5.39 | 5.22 |
| Calc. Bin Idx Time | 0.19 | 1.76 | 0.99 | 0.98 | 1.16 |
| Sort to Bins Time | 266.06 | 8.19 | 5.53 | 5.40 | 5.24 |
| Sort Bins Time | 37.38 | 57.57 | 39.40 | 44.81 | 41.66 |
