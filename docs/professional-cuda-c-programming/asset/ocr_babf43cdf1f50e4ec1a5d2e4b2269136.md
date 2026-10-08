Figure 5-13 illustrates the two memory operations using a simplified five-bank shared memory implementation.

Bank 0 Bank 1 Bank 2 Bank 3 Bank 4

![](bbox=[0.147, 0.185, 0.558, 0.381])

FIGURE 5-13

The kernel code is as follows:

```
__global void setReadCol(int *out) {
    // static shared memory
    shared int tile[BDIMY] [BDIMY];

    // mapping from thread index to global memory index
    unsigned int idx = threadIdx.y * blockDim.x + threadIdx.x;

    // shared memory store operation
    tile[threadIdx.y][threadIdx.x] = idx;

    // wait for all threads to complete
    syncthreads();

    // shared memory load operation
    out[idx] = tile[threadIdx.x][threadIdx.y];
}
```

After checking the memory transactions for this kernel with nvprof, the following metrics will be reported:

```
Kernel:setRowCol(int*)
1 shared_load_transactions_per_request  16.000000
1 shared_store_transactions_per_request  1.000000
```

The store operation is conflict-free, but the load operation reports a 16-way conflict.

# Dynamic Shared Memory

You can implement these kernels by declaring shared memory dynamically. You can either declare dynamic shared memory outside the kernel to make it global to file, or inside the