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

As the maximum number of threads per block is 1024, the maximum number of warps per block is 32 (1024 + 32 = 32). Thus, we can process the accumulate using just a single warp. We could have used thread 0 from each warp as we did before, but in this case we want the other warps to complete, not be left executing a single thread each.