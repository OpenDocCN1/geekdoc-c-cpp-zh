
We still have a total of six instructions, but now the first set does the load and the second set the increment of the pointer. The increment of the pointer is now a simple addition, much simpler than a multiply, and the result is not needed until the next iteration of the loop.

Applying the same strategy to the other array operations yields a reduction in execution time from 39.4 ms to 36.3 ms, a drop of 3 ms or around 10%. However, what about this variability in work done by each warp? Where does this come from?

Sample sort sorts data into blocks, or bins, which we independently sort using a single warp. If we do a dump of the values from single warp, we see something interesting.

```
Bin Usage - Max:331 Min:0 Avg:32.10275
0000:00000022 0001:00000000 0002:0000003e 0003:0000001d 0004:00000028 0005:00000000
0006:00000018 0007:0000003d
0008:00000052 0009:00000000 0010:0000001d 0011:00000000 0012:00000061 0013:00000000
0014:00000000 0015:00000000
0016:00000024 0017:00000009 0018:00000021 0019:00000000 0020:0000002b 0021:00000021
0022:00000000 0023:00000000
0024:00000025 0025:00000000 0026:00000056 0027:00000050 0028:00000019 0029:00000000
0030:00000025 0031:0000001d
```

There are a significant number of bins where the entries are zero. There are others where the total number of entries is very large. As one thread processes each bin, to iterate over the entire dataset, we need to iterate for the maximum of the bins from a given warp. The first warp shown has a maximum value of 0x9d (157 decimals) and a minimum value of zero. By the time we're at iteration 157, only a single thread from the entire warp is active. We see this reflected in the large difference between issued and executed instructions we saw earlier. (Instructions per clock, Figure 7.7). It's the bins with very large instruction counts that are taking the time.

We see a reduction in the execution time of the radix sort when we double the number of samples, because the peaks are pushed down and split out into more bins. However, sorting the samples then becomes the dominating issue. The problem is the distribution of samples to bins.

The large number of zero bins is actually caused by duplicates in the sample dataset. The source data array is filled with data via a simple call to rand(), which returns a non-so-random number. After a certain period these repeat. As the samples are selected at a uniform distance to one another, the sample set contains many duplicates. Removing this error in the random dataset removes almost all zeros from the bin count, but has an unintended effect that the execution time now climbs back up to the original 40 ms.

We can, however, apply another technique to this problem, that of loop unrolling and tail reduction, both of which we cover in Chapter 9. We replace the following code segment:

```
for (u32 i=start_idx; i<end_idx; i++)
{
    // Fetch the test data element
    const u32 elem = (*data_in_ptr);
    data_in_ptr++;
}
```

with

```
// Unroll 4 times
u32 i=start_idx;
if ( (end_idx - start_idx) >= 4)
{
    for ( i < (end_idx - 4); i+=4)
    {
        // Fetch the test first and second data element
        const u32 elem1 = (*data_in_ptr);
        const u32 elem2 = (*(data_in_ptr+1));
        const u32 elem3 = (*(data_in_ptr+2));
        const u32 elem4 = (*(data_in_ptr+3));
        data_in_ptr+=4;
    }
}
```

Suppose the difference between start_idx and end_idx is 32, one of the common cases. The number of iterations in the first loop will be 32. However, by unrolling the loop by a factor of four, we reduce the number of operations by a factor of four, that is, eight iterations. There are a few other important effects of loop unrolling. Notice we need, in the case of a factor of four, three additional registers to store three additional data points. We also need to handle the end loop condition where we may still have zero to three elements to process.

Looking at the PTX code we see:

```
:const.u32 elem1 = (*data_in_ptr);
mov.s64 %rd20, %rd14;
ld.u32 %r23, [%rd20+0];
:const.u32 elem2 = (*(data_in_ptr+1));
mov.s64 %rd21, %rd14;
ld.u32 %r25, [%rd21+4];
mov.s32 %r26, %r25;
:const.u32 elem3 = (*(data_in_ptr+2));
mov.s64 %rd22, %rd14;
ld.u32 %r27, [%rd22+8];
mov.s32 %r28, %r27;
:const.u32 elem4 = (*(data_in_ptr+3));
mov.s64 %rd23, %rd14;
ld.u32 %r29, [%rd23+12];
mov.s32 %r30, %r29;
:data_in_ptr+=4;
mov.s64 %rd24, %rd14;
add.u64 %rd25, %rd24, 16;
mov.s64 %rd14, %rd25;
```

We're doing something quite important here, introducing instruction level parallelism through the use of independent elements per thread. Table 7.1 and Figure 7.8 show the effect loop unrolling has. As you can see from Table 7.1 and Figure 7.8, introducing a small amount of thread level parallelism significantly drops the execution time of the radix sort. However, notice something else: The

| Unroll | 0 | 2 | 4 | 6 | 8 | 10 | 12 | 14 | 16 |
|---|---|---|---|---|---|---|---|---|---|
| Time | 40 | 37.02 | 33.98 | 33.17 | 32.78 | 32.64 | 32.25 | 33.17 | 32.51 |
| Registers | 38 | 38 | 40 | 42 | 44 | 44 | 44 | 44 | 44 |

![](img/e0b192dbaf05f61ad420bee512a8c4e4_243_0.png)

## FIGURE 7.8
Unroll level versus time and register usage.

number of registers never climbs above 44, even though we can use up to 63 in Fermi. What is happening at this point is the compiler introduces a call stack and no longer grows the number of registers used.

We've applied a couple of optimization techniques to the source code, which you might reasonably expect a compiler to automatically apply. We'll not remove any of these, so any gain should come from the compiler adding additional optimizations. Let's see if this is the case by switching to the release mode, which enables all the compiler optimizations by default (Table 7.2 and Figure 7.9).

We see from Table 7.2 and Figure 7.9 a very similar pattern to the release or optimized version, indicating that the optimizations we have just applied are not themselves applied automatically by the compiler. What is also noticeable is again we see the same pattern, that four elements per thread helps considerably, but beyond this the effect is marginal. Notice, even with optimizations enabled, the compiler does not automatically unroll the loop. Thus, we'll stick with manual unrolling by four, as the additional speed versus extra register usage is not a good tradeoff.

You might have expected the compiler to have pulled, or hoisted, out the read operations and placed them at the start of an unrolled loop. In many cases it will do this, except in the difficult cases, which are unfortunately all too often what we hit. Where you have a read followed by write followed by another read, the compiler cannot easily know if the write operation wrote to the same data area that is being read from. Thus, it must maintain the read-write-read sequence to ensure correctness. As

| Unroll | 0 | 2 | 4 | 6 | 8 | 10 | 12 | 14 | 16 |
|---|---|---|---|---|---|---|---|---|---|
| Debug | 40 | 37.02 | 33.98 | 33.17 | 32.78 | 32.64 | 32.25 | 33.17 | 32.51 |
| Release | 32.34 | 26.25 | 25.07 | 24.7 | 24.36 | 24.26 | 24.1 | 24.13 | 24.24 |

![](img/e0b192dbaf05f61ad420bee512a8c4e4_244_0.png)

## FIGURE 7.9
Debug versus release timing.

the programmer however, you know if the read operations are affected by the preceding write operations and can replace the read-write-read sequence with a much more efficient read-read-write sequence.

As we've now radically changed the timing on one aspect, dropping it from 40 ms to 25 ms, we should rerun the scan of the problem space to see if this now changes the optimum number of samples/threads.

One thing that becomes noticeable is the release version of QSort is actually much faster, over twice the speed in fact. This makes it considerably harder to produce a faster sort. However, quick sort is now a large component of the sample sort, as we preset the samples on the CPU. Thus, this reduction in execution time helps considerably. The best timing is as follows:

```
I/O: GeForce GTX 470: Test 16 - Selecting 32768 from 1048576 elements using 128 blocks of 256 threads

Num Threads:
Select Sample Time - CPU: 0.38 GPU: 0.38 0.19 0.50 0.31
Sort Sample Time - CPU: 4.63 GPU: 4.63 4.69 4.31 4.31
Count Bins Time - CPU: 64.50 GPU: 5.71 5.65 5.59 5.31
Calc. Bin Idx Time - CPU: 0.06 GPU: 1.55 0.79 0.86 0.79
Sort to Bins Time - CPU: 80.44 GPU: 6.25 6.08 5.96 5.71
Sort Bins Time - CPU: 62.81 GPU:27.37 25.10 36.28 39.87
```
