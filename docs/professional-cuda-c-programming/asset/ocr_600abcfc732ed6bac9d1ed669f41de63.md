Bank 0 Bank 1 Bank 2 Bank 3 Bank 4 padding

| | | |
|---|---|---|
| | (ix,iy) | row_idx = (blockDim.x+1)*threadidx.y + threadidx.x |
| (iy,ix) | | col_idx = (blockDim.x + 1)*threadidx.x + threadidx.y |

FIGURE 5-14

Because the global memory used to store data in the following kernel is smaller than the padded shared memory, you need three indices: one index for row-major writers to shared memory, one index for column-major reads from shared memory, and one index for coalesced accesses to unpadded global memory, as shown:

```
__global void setReadColDynPad(int *out) {
    // dynamic shared memory
    extern __shared__ int tile[];

    // mapping from thread index to global memory index
    unsigned row_idx = threadidx.y * (blockDim.x + IPAD) + threadidx.x;
    unsigned col_idx = threadidx.x * (blockDim.x + IPAD) + threadidx.y;

    unsigned g_idx = threadidx.y * blockDim.x + threadIdx.x;

    // shared memory store operation
    tile[row_idx] = g_idx;

    // wait for all threads to complete
    syncthreads();

    // shared memory load operation
    out[g_idx] = tile[col_idx];
}
```

Specify the size of shared memory when launching the kernel, as follows:

```
setReadColDynPad<<<grid, (BDMIX + 1) * BDIM, sizeof(int)>(d_C);
```

Check the memory of this kernel with nvprof. The following results are reported on a K40:

```
Kernel: setReadColDynPad(int*)
1 shared_load_transactions_per_request 1.000000
1 shared_store_transactions_per_request 1.000000
```