![](bbox=[0.14, 0.12, 0.82, 0.48])

# FIGURE 5.12 Grid, block, and thread dimensions.

threadIdx.x-The offset within a block of the X thread index.
threadIdx.y-The offset within a block of the Y thread index.

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
```