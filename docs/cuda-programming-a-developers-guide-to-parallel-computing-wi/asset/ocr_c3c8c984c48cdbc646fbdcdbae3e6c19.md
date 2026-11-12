```
/* Total thread count = 16 * 8 = 128 */
const dim3 threads_square(16, 8); /* 16 * 8 * 8 */
const dim3 blocks_square(2,2);

/** Needed to wait for a character at exit */
char ch;

/** Declare pointers for GPU based params */
unsigned int * gpu_block_x;
unsigned int * gpu_block_y;
unsigned int * gpu_thread;
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

```