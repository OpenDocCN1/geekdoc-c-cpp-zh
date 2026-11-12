The first task is to work out how many iterations over the data each thread needs to make. The parameter gridDim.x holds the number of blocks launched. Each block consists of blockDim.x threads. Thus, we can work out how many elements of data each thread must accumulate. We then accumulate these in local_result, and only when the block is complete, do a single write to global memory.

This reduces the contention from a thread-level contention to a block-level contention. As we're only launching a few hundred blocks, the probability of them all requiring the write at the same time is reasonably low. Clearly as we increase the number of blocks, the potential contention increases. Once we have loaded all the SMs with the maximum number of permitted blocks, there is little reason to increase the number of blocks further, other than for work balancing.

The GTX460 is perhaps the worst example, as with only 7 SMs, each with 6 blocks, we should saturate the device at only 42 blocks. The GTX470 would need 90 blocks. We, therefore, try all number of blocks (49,152) down to 16 in powers of two, fewer blocks would be necessary to fully populate the SMs. This generates the following results:

```
I0:0 GeForce GTX 470:GMEM loop1 49152 passed Time 197.82 ms
I0:0 GeForce GTX 470:GMEM loop1 24576 passed Time 98.96 ms
I0:0 GeForce GTX 470:GMEM loop1 12288 passed Time 49.56 ms
I0:0 GeForce GTX 470:GMEM loop1 6144 passed Time 24.83 ms
I0:0 GeForce GTX 470:GMEM loop1 3072 passed Time 12.48 ms
I0:0 GeForce GTX 470:GMEM loop1 1536 passed Time 6.33 ms
I0:0 GeForce GTX 470:GMEM loop1 768 passed Time 3.35 ms
I0:0 GeForce GTX 470:GMEM loop1 384 passed Time 1.62 ms
I0:0 GeForce GTX 470:GMEM loop1 192 passed Time 2.62 ms
I0:0 GeForce GTX 470:GMEM loop1 96 passed Time 1.87 ms
I0:0 GeForce GTX 470:GMEM loop1 64 passed Time 1.48 ms
I0:0 GeForce GTX 470:GMEM loop1 48 passed Time 1.50 ms
I0:0 GeForce GTX 470:GMEM loop1 32 passed Time 1.75 ms
I0:0 GeForce GTX 470:GMEM loop1 16 passed Time 2.98 ms
```

```
I0:3 GeForce GTX 460:GMEM loop1 49152 passed Time 164.25 ms
I0:3 GeForce GTX 460:GMEM loop1 24576 passed Time 82.45 ms
I0:3 GeForce GTX 460:GMEM loop1 12288 passed Time 41.52 ms
I0:3 GeForce GTX 460:GMEM loop1 6144 passed Time 21.01 ms
I0:3 GeForce GTX 460:GMEM loop1 3072 passed Time 10.77 ms
I0:3 GeForce GTX 460:GMEM loop1 1536 passed Time 5.60 ms
I0:3 GeForce GTX 460:GMEM loop1 768 passed Time 3.16 ms
I0:3 GeForce GTX 460:GMEM loop1 384 passed Time 2.51 ms
I0:3 GeForce GTX 460:GMEM loop1 192 passed Time 2.19 ms
I0:3 GeForce GTX 460:GMEM loop1 96 passed Time 2.12 ms
I0:3 GeForce GTX 460:GMEM loop1 64 passed Time 2.05 ms
I0:3 GeForce GTX 460:GMEM loop1 48 passed Time 2.41 ms
I0:3 GeForce GTX 460:GMEM loop1 32 passed Time 1.96 ms
I0:3 GeForce GTX 460:GMEM loop1 16 passed Time 2.70 ms
```

If we look at this first on the very large number of blocks we see a fairly linear drop as we halve the number of blocks for each run, for both the GTX470 and GTX460 cards. We're halving the number of