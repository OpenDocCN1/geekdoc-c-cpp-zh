kernel to restrict it to kernel scope. Dynamic shared memory must be declared as an unsigned 1D array; therefore, you need to calculate access indices based on 2D thread indices. Because you are going to write in row-major order and read in column-major order in this kernel, you need to maintain two indices as follows:

+   - row_idx: 1D row-major offset calculated from 2D thread indices
- col_idx: 1D column-major memory offset calculated from 2D thread indices

You wrote shared memory in row-major order using the calculated row_idx as follows:

```
tile[row_idx] = row_idx;
```

Using proper synchronization after the shared memory tile has been filled, you then read it in column-major order and assign to global memory as follows:

```
out[row_idx] = tile[col_idx];
```

Because out is stored in global memory and threads are arranged in row-major order within a block, you want to write out in row-major order by thread coordinate to ensure coalesced stores.

```
__global void setRowColDyn(int *out) {
    // dynamic shared memory
    extern __shared__ int tile[];

    // mapping from thread index to global memory index
    unsigned int row_idx = threadIdx.y * blockDim.x + threadIdx.x;
    unsigned int col_idx = threadIdx.x * blockDim.y + threadIdx.y;

    // shared memory store operation
    tile[row_idx] = row_idx;

    // wait for all threads to complete
    syncthreads();

    // shared memory load operation
    out[row_idx] = tile[col_idx];
}
```

The shared memory size must be specified when launching the kernel, as follows:
setRowColDyn<<<grid, block, BDIMY * sizeof(int)>(d_C);

This kernel is also available in checkSharedMem.cu. Try checking the memory transactions of the setRowColDyn kernel with nprof. The following is reported:

```
Kernel: setRowColDyn(int*)
1 shared_load_transactions_per_request    16.000000
1 shared_store_transactions_per_request    1.000000
```

These results are identical to the previous RowReadCol example, but using dynamically declared shared memory with 2D array index calculation. The write operation is conflict-free, while the read operation reports a 16-way conflict.