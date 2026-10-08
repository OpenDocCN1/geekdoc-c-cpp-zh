The store and load requests to shared memory are serviced by one transaction in the kernel setReadRow. The requests are serviced by eight transactions in the kernel setColRead. The Kepler K40 band width is eight words, and 16 4-byte elements in a column are arranged into banks, as illustrated in Figure 5-6; therefore, the operation reports an eight-way conflict.

# Writing Row-Major and Reading Column-Major

In this section, you will implement a kernel that writes to shared memory in row-major order and reads from shared memory in column-major order using a rectangular shared memory array. This kernel is applicable in real-world applications; it performs a transpose using shared memory to improve performance by maximizing-latency loads and stores, and coalescing global memory

The 2D shared memory tile is declared as follows:

```
__shared int tile [BDIMY] [BDIMX];
```

The kernel has three memory operations:

+   - Write to a shared memory row with each warp to avoid bank conflicts.
- Read from a shared memory column with each warp to perform a matrix transpose.
- Write to a global memory row from each warp with coalesced access.

The procedure for calculating the proper shared and global memory accesses is as follows. First, the2D thread index of the current thread is converted to a 1D global thread ID:

```
unsigned int idx = threadIdx.y * blockDim.x + threadIdx.x;
```

This 1D, row-major mapping ensures that global memory accesses are coalesced. Because data elements in the output global memory are transposed, you need to calculate the new coordinate in the transpose matrix, as follows:

```
unsigned int irow = idx / blockDim.y;
unsigned int icol = idx % blockDim.y;
```

You initialize the shared memory tile by storing the global thread IDs to the 2D shared memory tile as follows:

```
tile[threadIdx.y][threadIdx.x] = idx;
```

At this point, the data in shared memory is stored linearly from 0 to BDIMX*BDIMY-1. Each warp performs row-major writes to shared memory, there is no bank-conflict during the write operation.

Now, you can access the shared memory data to transpose with the coordinates earlier. By accessing shared memory using swapped irow and icol, you can transpose the data using the global 1D thread IDs. As shown in the following snippet, a warp reads data elements from one column in shared memory, and performs a coalesced write to global memory.

```
out[idx] = tile[icol][irow];
```