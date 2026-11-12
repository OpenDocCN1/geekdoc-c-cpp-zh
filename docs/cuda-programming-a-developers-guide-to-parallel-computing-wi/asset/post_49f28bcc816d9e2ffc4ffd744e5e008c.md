
| Thread 0-15, Block 0 | Thread 16-31, Block 0 |
| --- | --- |
| Thread 32-47, Block 0 | Thread 48-63, Block 0 |
| Thread 64-79, Block 0 | Thread 80-95, Block 0 |
| Thread 96-111, Block 0 | Thread 112-127, Block 0 |
| Thread 0-15, Block 1 | Thread 16-31, Block 1 |
| Thread 32-47, Block 1 | Thread 48-63, Block 1 |
| Thread 64-79, Block 1 | Thread 80-95, Block 1 |
| Thread 96-111, Block 1 | Thread 112-127, Block 1 |
| Thread 0-15, Block 2 | Thread 16-31, Block 2 |
| Thread 32-47, Block 2 | Thread 48-63, Block 2 |
| Thread 64-79, Block 2 | Thread 80-95, Block 3 |
| Thread 96-111, Block 3 | Thread 112-127, Block 3 |
| Thread 0-15, Block 4 | Thread 16-31, Block 4 |
| Thread 32-47, Block 4 | Thread 48-63, Block 4 |
| Thread 64-79, Block 4 | Thread 80-95, Block 4 |
| Thread 96-111, Block 4 | Thread 112-127, Block 4 |

| Thread 0-15, Block 0 | Thread 0-15, Block 1 |
| --- | --- |
| Thread 16-31, Block 0 | Thread 16-31, Block 1 |
| Thread 32-47, Block 0 | Thread 32-47, Block 1 |
| Thread 48-63, Block 0 | Thread 48-63, Block 1 |
| Thread 64-79, Block 0 | Thread 64-79, Block 1 |
| Thread 80-95, Block 0 | Thread 80-95, Block 1 |
| Thread 96-111, Block 0 | Thread 96-111, Block 1 |
| Thread 112-127, Block 0 | Thread 112-127, Block 1 |
| Thread 0-15, Block 2 | Thread 0-15, Block 4 |
| Thread 16-31, Block 2 | Thread 16-31, Block 4 |
| Thread 32-47, Block 2 | Thread 32-47, Block 4 |
| Thread 48-63, Block 3 | Thread 48-63, Block 4 |
| Thread 64-79, Block 3 | Thread 64-79, Block 4 |
| Thread 80-95, Block 3 | Thread 80-95, Block 4 |
| Thread 96-111, Block 3 | Thread 96-111, Block 4 |
| Thread 112-127, Block 3 | Thread 112-127, Block 4 |

FIGURE 5.11 Alternative thread block layouts.

```
dim3 threads_square(16,8);
dim3 blocks_square(2,2);
```

In either arrangement you have the same total number of threads (32 x 4 = 128, 16 x 8 = 128). It's simply the layout of the threads that is different.

The dim3 type is simply a special CUDA type that you have to use to create a 2D layout of threads. In the rectangle example, you're saying you want 32 threads along the X axis by 4 threads along the Y axis, within a single block. You're then saying you want the blocks to be laid out as one block wide by four blocks high. You'll need to invoke the kernel with

```
some_kernel_func<<< blocks_rect, threads_rect >>>(a, b, c);
```

or

```
some_kernel_func<<< blocks_square, threads_square >>>(a, b, c);
```

As you no longer want just a single thread ID, but an X and Y position, you'll need to update the kernel to reflect this. However, you also need to linearize the thread ID because there are situations where you may want an absolute thread index. For this we need to introduce a couple of new concepts, shown in Figure 5.12.

You can see a number of new parameters, which are:

- gridDim.x - The size in blocks of the X dimension of the grid.
- gridDim.y - The size in blocks of the Y dimension of the grid.
- blockDim.x - The size in threads of the X dimension of a single block.
- blockDim.y - The size in threads of the Y dimension of a single block.

![](img/e0b192dbaf05f61ad420bee512a8c4e4_101_0.png)

FIGURE 5.12 Grid, block, and thread dimensions.

- threadIdx.x - The offset within a block of the X thread index.
- threadIdx.y - The offset within a block of the Y thread index.

You can work out the absolute thread index by working out the Y position and multiplying this by number of threads in a row. You then simply add in the X offset from the start of the row. Thus, the thread index calculation is

```
threadIdx.x = ((gridDim.x * blockDim.x) * idy) + idx;
```

So you need to modify the kernel to additionally return the X and Y positions plus some other useful bits of information, as follows:

```
__global__ void what_is_my_id_2d_A(
unsigned int * const block_x,
unsigned int * const block_y,
unsigned int * const thread,
unsigned int * const calc_thread,
unsigned int * const x_thread,
unsigned int * const y_thread,
unsigned int * const grid_dimx,
unsigned int * const block_dimx,
unsigned int * const grid_dimy,
unsigned int * const block_dimy,
{
    const unsigned int idx    = (blockIdx.x * blockDim.x) + threadIdx.x;
    const unsigned int idy    = (blockIdx.y * blockDim.y) + threadIdx.y;
    const unsigned int thread_id = ((gridDim.x * blockDim.x) * idy) + idx;

    block_x[thread_id]    = blockIdx.x;
    block_y[thread_id]    = blockIdx.y;
    thread[thread_id]     = threadIdx.x;
    calc_thread[thread_id] = thread_id;
    x_thread[thread_id]   = idy;
    y_thread[thread_id]   = idx;
    grid_dimx[thread_id]  = gridDim.x;
    block_dimx[thread_id] = blockDim.x;
    grid_dimy[thread_id] = gridDim.y;
    block_dimy[thread_id] = blockDim.y;
}
```

We'll call the kernel twice to demonstrate how you can arrange array blocks and threads. As you're now passing an additional dataset to compute, you need an additional cudaMalloc, cudaFree, and cudaMemcpy to copy the data from the device. As you're using two dimensions, you'll also need to modify the array size to allocate and transfer the correct size of data.

```
#define ARRAY_SIZE_X 32
#define ARRAY_SIZE_Y 16

#define ARRAY_SIZE_IN_BYTES ((ARRAY_SIZE_X) * (ARRAY_SIZE_Y) * (sizeof(unsigned int)))

/* Declare statically six arrays of ARRAY_SIZE each */
unsigned int cpu_block_x[ARRAY_SIZE_Y][ARRAY_SIZE_X];
unsigned int cpu_block_y[ARRAY_SIZE_Y][ARRAY_SIZE_X];
unsigned int cpu_thread[ARRAY_SIZE_Y][ARRAY_SIZE_X];
unsigned int cpu_calc_thread[ARRAY_SIZE_Y][ARRAY_SIZE_X];
unsigned int cpu_warp[ARRAY_SIZE_Y][ARRAY_SIZE_X];
unsigned int cpu_grid_dimx[ARRAY_SIZE_Y][ARRAY_SIZE_X];
unsigned int cpu_grid_dimy[ARRAY_SIZE_Y][ARRAY_SIZE_X];
unsigned int cpu_block_dimx[ARRAY_SIZE_Y][ARRAY_SIZE_X];
unsigned int cpu_block_dimy[ARRAY_SIZE_Y][ARRAY_SIZE_X];

int main(void)
{
    /* Total thread count = 32 * 4 = 128 */
    const dim3 threads_rect(32, 4); /* 32 * 4 * 4 */
    const dim3 blocks_rect(1,4);

/* Total thread count = 16 * 8 = 128 */
const dim3 threads_square(16, 8); /* 16 * 8 * 8 */
const dim3 blocks_square(2,2);

/** Needed to wait for a character at exit */
char ch;

/** Declare pointers for GPU based params */
unsigned int * gpu_block_x;
unsigned int * gpu_block_y;
unsigned int * gpu_thread;
unsigned int * gpu_warp;
unsigned int * gpu_calc_thread;
unsigned int * gpu_xthread;
unsigned int * gpu_ythread;
unsigned int * gpu_grid_dimx;
unsigned int * gpu_grid_dimy;
unsigned int * gpu_block_dimx;
unsigned int * gpu_block_dimy;

/** Allocate four arrays on the GPU */
cudaMalloc((void **)&gpu_block_x, ARRAY_SIZE_IN_BYTES);
cudaMalloc((void **)&gpu_block_y, ARRAY_SIZE_IN_BYTES);
cudaMalloc((void **)&gpu_thread, ARRAY_SIZE_IN_BYTES);
cudaMalloc((void **)&gpu_calc_thread, ARRAY_SIZE_IN_BYTES);
cudaMalloc((void **)&gpu_xthread, ARRAY_SIZE_IN_BYTES);
cudaMalloc((void **)&gpu_ythread, ARRAY_SIZE_IN_BYTES);
cudaMalloc((void **)&gpu_grid_dimx, ARRAY_SIZE_IN_BYTES);
cudaMalloc((void **)&gpu_grid_dimy, ARRAY_SIZE_IN_BYTES);
cudaMalloc((void **)&gpu_block_dimx, ARRAY_SIZE_IN_BYTES);
cudaMalloc((void **)&gpu_block_dimy, ARRAY_SIZE_IN_BYTES);

for (int kernel=0; kernel < 2; kernel++)
{
switch (kernel)
{
case 0:
{
/** Execute our kernel */
/* what_is_my_id_2d<<<(blocks_rect, threads_rect)>>>(gpu_block_x, gpu_block_y,
gpu_thread, gpu_calc_thread, gpu_xthread, gpu_ythread, gpu_grid_dimx, gpu_block_dimx,
gpu_grid_dimy, gpu_block_dimy); */
break;
}
case 1:
{
/* Execute our kernel */
what_is_my_id_2d_A<<<(blocks_square, threads_square)>>(gpu_block_x, gpu_block_y,
    gpu_thread, gpu_calc_thread, gpu_xthread, gpu_ythread, gpu_grid_dimx, gpu_block_dimx,
    gpu_grid_dimy, gpu_block_dimy);
    break;

default: exit(1); break;
}

/* Copy back the gpu results to the CPU */
cudaMemcpy(cpu_block_x, gpu_block_x, ARRAY_SIZE_IN_BYTES,
    cudaMemcpyDeviceToHost);
cudaMemcpy(cpu_block_y, gpu_block_y, ARRAY_SIZE_IN_BYTES,
    cudaMemcpyDeviceToHost);
cudaMemcpy(cpu_warp, gpu_warp, ARRAY_SIZE_IN_BYTES,
    cudaMemcpyDeviceToHost);
cudaMemcpy(cpu_thread, gpu_thread, ARRAY_SIZE_IN_BYTES,
    cudaMemcpyDeviceToHost);
cudaMemcpy(cpu_xthread, gpu_xthread, ARRAY_SIZE_IN_BYTES,
    cudaMemcpyDeviceToHost);
cudaMemcpy(cpu_ythread, gpu_ythread, ARRAY_SIZE_IN_BYTES,
    cudaMemcpyDeviceToHost);
cudaMemcpy(cpu_grid_dimx, gpu_grid_dimx, ARRAY_SIZE_IN_BYTES,
    cudaMemcpyDeviceToHost);
cudaMemcpy(cpu_grid_dimy, gpu_grid_dimy, ARRAY_SIZE_IN_BYTES,
    cudaMemcpyDeviceToHost);
cudaMemcpy(cpu_block_dimx, gpu_block_dimx, ARRAY_SIZE_IN_BYTES,
    cudaMemcpyDeviceToHost);
cudaMemcpy(cpu_block_dimy, gpu_block_dimy, ARRAY_SIZE_IN_BYTES,
    cudaMemcpyDeviceToHost);

printf("\nKernel %d\n", kernel);
/* Iterate through the arrays and print */
for (int y=0; y < ARRAY_SIZE_Y; y++)
{
    for (int x=0; x < ARRAY_SIZE_X; x++)
    {
    printf("CT%u: %2u BKX: %lu BKY: %lu ThX: %2u YTID: %2u XTID: %2u GDX: %lu BDX: %lu GDY: %lu BDY: %lu\n", cpu_calc_thread[y][x], cpu_block_x[y][x], cpu_block_y[y][x],
    cpu_thread[y][x], cpu_xthread[y][x], cpu_ythread[y][x], cpu_grid_dimx[y][x],
    cpu_block_dimx[y][x], cpu_grid_dimy[y][x], cpu_block_dimy[y][x]);
    }
}

/* Wait for any key so we can see the console window */
ch = getch();

/* Wait for any key so we can see the console window */
printf("Press any key to continue\n");
}
```
