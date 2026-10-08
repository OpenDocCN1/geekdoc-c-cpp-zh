The results are summarized here:

| Device "Tesla K40 (0)"
| Kernel: reduceSmem(int*, int*, unsigned int)
| 1 Global Load Transactions | 524288 |
| 1 Global Store Transactions | 131072 |
| Kernel: reduceGmem(int*, int*, unsigned int)
| 1 Global Load Transactions | 2883584 |
| 1 Global Store Transactions | 1179648 |

It is clear from the results that using shared memory reduced global memory access by a significant amount.

# # Parallel Reduction with Unrolling

In the preceding kernels, each thread block handles one block of data. In Chapter 3, you unrolled blocks to improve kernel performance by enabling multiple I/O operations to be in-flight at. The following kernel unrolls four blocks; each thread handles data elements from four blocks. With unrolling, you get the following benefits:

+   - Increased global throughput by exposing more parallel I/O per thread
- Reduction of global memory store transactions by one-fourth
- Overall kernel performance improvement

The kernel code is as follows:

```
__global_ void reduceSmemUnroll(int *g_idata, int *g_odata, unsigned int n) {
    // static shared memory
    shared_ int smem[DIM];

    // set thread ID
    unsigned int tid = threadIdx.x;

    // global index, 4 blocks of input data processed at a time
    unsigned int idx = blockIdx.x * blockDim.x * 4 + threadIdx.x;

    // unrolling 4 blocks
    int tmpSum = 0;

    // boundary check
    if (idx + 3 * blockDim.x <= n) {
        int a1 = g_idata[idx];
        int a2 = g_idata[idx + blockDim.x];
        int a3 = g_idata[idx + 2 * blockDim.x];
        int a4 = g_idata[idx + 3 * blockDim.x];
        tmpSum = a1 + a2 + a3 + a4;
    }

    smem[tid] = tmpSum;
```