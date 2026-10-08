
With these concepts clear in mind, you can design an efficient kernel to avoid bank conflict and fully utilize the benefits of shared memory.

## Square Shared Memory

You can use shared memory to cache global data with square dimensions in a straightforward fashion. The simple dimensionality of a square array makes it easy to calculate 1D memory offsets from 2D thread indices. Figure 5-12 illustrates a shared memory tile with 32 elements in each dimension, stored in row-major order. The top figure shows the actual arrangement of 1D data layout, and the bottom figure shows the logical 2D shared memory tile with a mapping between 4-byte data elements and banks.

| Byte address | 0 | 4 | 8 | 12 | 16 | 20 | 24 | 28 | ... | 4088 | 4092 |
| 4-byte word index | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | ... | 1022 | 1023 |

| Bank 0 | Bank 1 | Bank 2 | Bank 3 | ... | ... | Bank 30 | Bank 31 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Row 0 | 0 | 1 | 2 | 3 | ... | ... | ... | ... |
| Row 1 | 32 | 33 | 34 | 35 | ... | ... | 60 | 62 | 63 |
| Row 2 | 64 | 65 | | | ... | ... | ... | 95 |
| Row 3 | 96 | 97 | | | ... | ... | ... | 127 |
| Row 30 | 960 | | | | ... | ... | ... | 991 |
| Row 31 | 992 | | | | ... | ... | 1023 | 1023 |

FIGURE 5-12

You can declare a 2D shared memory variable statically, as follows:

```
__shared int tile[N][N];
```

Because this shared memory tile is square, you can choose to access it from a 2D thread block with neighboring threads elements in either the x or y dimension:

```
tile[threadIdx.y][threadIdx.x]
tile[threadIdx.x][threadIdx.y];
```

Which of these methods is likely to perform better? You need to pay attention to how threads map to shared memory. Recall that it is optimal to have threads in the same warp accessing separate banks. Threads in the same warp are identified by consecutive values of threadIdx.x. Elements in shared memory belonging to different banks are also stored concurrently, by word offset. It is best to have with consecutive values of threadIdx.x accessing consecutive locations in shared memory. From this, you can conclude that the first pattern (tile[threadIdx.y][threadIdx.x]) will exhibit better performance and fewer bank conflicts than the second (tile[threadIdx.x][threadIdx.y]), because neighboring threads are accessing neighboring cells along the innermost array.

## Accessing Row-Major versus Column-Major

Consider an example in which one grid with 2D block containing 32 threads in each dimension is used. You can define the block dimensions using the following macro:

```
#define BDIMX 32
#define BDIMY 32
```

You can also use that macro to define the execution configuration for the kernel:

```
dim3 block (BDIMX,BDIMY);
dim3 grid (1,1);
```

The kernel has two simple operations:

- Write global thread indices to a 2D shared memory array in row-major order.
- Read those values from shared memory in row-major order and store them to global memory.

First, you can declare a 2D shared memory array statically as follows:

```
__shared__ int tile[BDIMY][BDIMX];
```

Next, you need to calculate the global index for each thread of its 2D ID. Because only one thread block will be launched, the index conversion can be simplified:

```
unsigned int idx = threadIdx.y * blockDim.x + threadIdx.x;
```

For the examples in this section, idx will be used to read a value from an input matrix. Storing the value of idx to the output array allows you to visualize the access pattern of the kernel based on where threads write their global IDs.

Writing the global thread index into the shared memory tile in row-major order can be performed as follows:

```
tile[threadIdx.y][threadIdx.x] = idx;
```

Once a synchronization point is reached (using syncthreads()), all threads must have stored data to the shared memory, so you can then assign values to global memory from shared memory in row-major order as follows:

```
out[idx] = tile[threadIdx.y][threadIdx.x];
```

The kernel code is as follows:

```
__global_ void setRowReadRow(int *out) {
    // static shared memory
    shared__ int tile [BDIMY] [BDIMX];

    // mapping from thread index to global memory index
    unsigned int idx = threadIdx.x + blockDim.x;

    // shared memory store operation
    tile[threadIdx.y] [threadIdx.x] = idx;

    // wait for all threads to complete
    syncthreads();

    // shared memory load operation
    out[idx] = tile[threadIdx.y][threadIdx.x];
}
```

So, you have three memory operations:

- One operation on shared memory
- One operation on shared memory
- One operation on global memory

Because threads in the warp have consecutive threadIdx.y and threadIdx.x values and threadIdx.x to index the innermost dimension of the shared memory tile, this kernel is free of bank conflicts. On the other hand, if you swap threadIdx.y and threadIdx.x when assigning data to the shared memory, the accesses of a warp will be in column-major order. Every shared memory load will cause a 32-way conflict for a Fermi device, and a 16-way bank conflict for a Kepler device.

```
__global_ void setColReadCol(int *out) {
    // static shared memory
    shared__ int tile [BDIMX] [BDIMY];

    // mapping from thread index to global memory index
    unsigned int idx = threadIdx.y * blockDim.x + threadIdx.x;

    // shared memory store operation
    tile[threadIdx.x] [threadIdx.y] = idx;

    // wait for all threads to complete
    syncthreads();

    // shared memory load operation
    out[idx] = tile[threadIdx.x][threadIdx.y];
}
```

Before testing the performance of these kernels, you will need to prepare global memory. You are encouraged to write the main function and all of example kernels in this section also available in checksemSquare.cu. Compile it to an executable named smemSquare using the command:

```
nvcc checksemSquare.cu -o smemSquare
```

```
nvprof ./smemSquare
```

The results on Tesla K40 with 4-byte shared memory access mode are shown here. They clearly show that accessing memory is improved by row performance as a result of neighboring threads referencing neighboring nodes.

| Time (%) | Calls | Avg | Name |
| :--- | :--- | :--- | :--- |
| 13.25% | 2.66800us | 1 | 2.66800us | setColReadCol(int*) |
| 11.36% | 2.30400us | 1 | 2.30400us | setRowRowNum(int*) |

Next, you can check for conflicts in the kernel functions using the nvprof metrics:

```
shared_load_transactions_per_request
shared_store_transactions_per_request
```

The results reported from nvprof are as follows. These results indicate that the store and load requests from a warp in kernel are serviced by one transaction, while the same requests in kernel setColRow are serviced by 16 transactions. This confirms that the kernel has a 16-way conflict on Kepler using a shared memory bank width of 8 bytes.

| Kernel | shared_load_transactions_per_request | shared_store_transactions_per_request |
| :--- | :--- | :--- |
| setColReadCol(int*) | 16.000000 | 16.000000 |
| setRowRowNum(int*) | 1.000000 | 1.000000 |

## Writing Row-Major and Reading Column-Major

The following kernels implement shared memory in row-major order, and shared memory reads in column-major order. Writing to the shared memory in row-major order is implemented by putting the innermost dimension of thread as the column index of the 2D shared memory tile (identical to the last example):

```
tile[threadIdx.y] = [threadIdx.x] = idx;
```

Assigning values to global memory from the shared memory in column-major order is implemented by swapping the thread index when referencing shared memory:

```
out[idx] = tile[threadIdx.x];
```

Figure 5-13 illustrates the two memory operations using a simplified five-bank shared memory implementation.

Bank 0 Bank 1 Bank 2 Bank 3 Bank 4

![](img/506ba3a4c9f4512233692f3f20de1f3a_248_0.png)

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
