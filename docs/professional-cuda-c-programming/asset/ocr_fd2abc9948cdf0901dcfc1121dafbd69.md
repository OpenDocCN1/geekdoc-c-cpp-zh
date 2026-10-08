# Original Matrix Transposed Matrix

![](bbox=[0.095, 0.125, 0.824, 0.439])

index 1D shared memory idx - blockDim.x*ly + ix

shared memory (ix,y)

new coordinate in transposed block

FIGURE 5-16

Using shared memory increases performance of the transpose kernel, as shown in Table 5-3.

# TABLE 5-3: Performance of Transpose Kernels

| KERNELS | TESLA M2090 (ECC OFF) | TESLA K40 (ECC OFF) |
|---|---|---|--|
| | ELAPSED TIME (MS) | BANDWIDTH (GB/S) | ELAPSED TIME (MS) | BANDWIDTH (GB/S) |
| copyGmem | 1.048 | 128.07 | 0.758 | 177.15 |
| naiveGmem | 3.611 | 37.19 | 1.947 | 68.98 |
| transposeSmem | 1.551 | 86.54 | 1.149 | 116.82 |

The number of global memory transactions performed per request by nvprof for the transposeSmem kernel is:

```
Device "Tesla K40c ()" Metrics Transactions
Kernel: transposeSmem(float*, float*, int, int)
1  gld_transactions_per_request  1.000000
1  gst_transactions_per_request  2.000000
```

The replay of global memory stores is reduced from 32 to 2. Because the block width in the transpose block is 16, the writes of the first half and the second half of a warp are stripped by 4,080; therefore, a warp request to write to global memory is serviced by two transactions. Changing the block size to 32x32 would reduce the count to 1. However, a thread block configuration of 32x16 enables more parallelism than the 32x32 launch configuration. Later, you will investigate which optimization is more beneficial.