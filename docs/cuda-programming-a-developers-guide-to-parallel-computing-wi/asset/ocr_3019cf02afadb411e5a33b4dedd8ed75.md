```
}
if (tid == 0)
{
    // Incrementet the list pointer for this thread
    list_Indexes[reduction_idx[0]]++;
    // Store the winning value
    dest_array[i] = reduction_val[0];
}
// Wait for tid zero
__syncthreads();
}
}
```

This code works by creating a temporary list of data in shared memory, which it populates with a dataset from each cycle from the num_list datasets. Where a list has already been emptied, the dataset is populated with 0xFFFFFFFF, which will exclude the value from the list. The while loop gradually reduces the number of active threads until there is only a single thread active, thread zero. This then copies the data and increments the list indexes to ensure the value is not processed twice. Notice the use of the __syncthreads directive within the loop and at the end. The program needs to sync across warps when there are more than 32 threads (one warp) in use.

So how does this perform? As you can see from Table 6.11 and Figure 6.13, this approach is significantly slower than the atomicMin version, the fastest reduction being 8.4 ms versus the 5.86 ms atomicMin (GTX460, 16 threads). This is almost 50% slower than the atomicMin version. However, one thing to note is that it's a little under twice the speed of the atomicMin when using 256 threads (12.27 ms versus 21.58 ms). This is, however, still twice as slow as the 16-thread version.

Although this version is slower, it has the advantage of not requiring the use of the atomicMin function. This function is only available on compute 1.2 devices, which is generally only an issue if you need to consider the consumer market or you need to support really old Tesla systems. The main issue, however, is that atomicMin can only be used with integer values. A significant number of real-world problems are floating-point based. In such cases we need both algorithms.

However, what we can take from both the atomicMin and the parallel reduction method is that the traditional merge sort using two lists is not the ideal case on a GPU. You get increasing performance from

| Device/Threads | 1 | 2 | 4 | 8 | 16 | 32 | 64 | 128 | 256 |
|---|---|---|---|---|---|---|---|---|---|
| GTX470 | 28.4 | 17.67 | 12.44 | 10.32 | 9.98 | 10.59 | 11.62 | 12.94 | 14.61 |
| 9800GT | 45.66 | 28.35 | 19.82 | 16.25 | 15.61 | 17.03 | 19.03 | 21.45 | 25.33 |
| GTX260 | 56.07 | 34.71 | 24.22 | 19.84 | 19.04 | 20.6 | 23.2 | 26.28 | 31.01 |
| GTX460 | 23.22 | 14.52 | 10.3 | 8.63 | 8.4 | 8.94 | 9.82 | 10.96 | 12.27 |