```
```c
int (*predicate_func)(const u32 a, const u32 b) )
{
// Calculate absolute thread number
const u32 tid = (blockIdx.x * blockDim.x) + threadIdx.x;

// Current warp number - divide by 32
const u32 warp_num = threadIdx.x >> 5;

// Total number of warp number - divide by 32
const u32 number_of_warps = blockDim.x >> 5;

// If not off the end of the array then contribute
if (tid < num_elements)
{
// Have the first thread of every warp
// clear the shared memory entry
if ((threadIdx.x % WARP_SIZE) == 0)
{
warp_shared_ballot[warp_num] = 0;
}

// Call __ballot to set the N'th bit in the word
// with a warp if the predicate is true
// OR the bits from all threads in the warp into
// one value per warp held in shared memory
atomicOr( &warp_shared_ballot[warp_num],
__ballot_nonatom( predicate_func(data[tid], threshold)) );
}

// Wait for all warps to complete
__syncthreads();

// From the first warp, activate up to 32 threads
// Actual number of threads needed is the number
// warps in the block
// All other warps drop out at this point
if (threadIdx.x < number_of_warps)
{
// Have thread zero, zero the accumulator
if (threadIdx.x == 0)
{
block_shared_accumulate = 0;
}

// Add to the single accumulator the number
// of bits set from each warp.
```
```