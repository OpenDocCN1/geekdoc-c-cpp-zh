cause a memory access violation using rectangular shared memory. You will need to re-implement all of the kernels described in the previous section by recalculating access indices based on matrix dimensions.

Without loss of generality, you are going to examine a rectangular shared memory array with 32 elements per row and 16 elements per column. The dimensions are defined in the following macros:

```
#define BDIMX 32
#define BDIM 16
```

The rectangular shared memory tile is allocated as follows:

```
__shared__ int tile [BDIMX][BDIMY];
```

For simplicity, the kernel will be launched with one grid, and one 2D block using the same size as the rectangular shared memory array, as follows:

```
dim3 block (BDIMX, BDIMY);
dim3 grid (1,1);
```

# Accessing Row-Major versus Accessing Column-Major

The first two kernels you will investigate were also used in the square case:

```
__global void setRowReadRow(int *);
__global void setColReadCol(int *);
```

You need to pay careful attention to the declaration of the rectangular shared memory array in each kernel. The length of the innermost dimension of the shared memory array tile is the same as the innermost dimension of the 2D thread block:

```
__shared__ int tile [BDIMX][BDIMY];
```

In the kernel setColReadCol, the length of the innermost dimension of the shared memory array tile is the same as the outermost dimension of the 2D thread block:

```
__shared__ int tile [BDIMX][BDIMY];
```

You can download the code for this example in the checkSmemRectangle.cu from Wrox.com. Compile it and check the bank results with the following nvprof metrics:

```
shared_load_transactions_per_request
shared_store_transactions_per_request
```

The results on a K40 are reported as follows:

```
Kernel:setRowReadRow(int*)
  1 shared_load_transactions_per_request 1.000000
  1 shared_store_transactions_per_request 1.000000
Kernel:setColReadCol(int*)
  1 shared_load_transactions_per_request 8.000000
  1 shared_store_transactions_per_request 8.000000
```