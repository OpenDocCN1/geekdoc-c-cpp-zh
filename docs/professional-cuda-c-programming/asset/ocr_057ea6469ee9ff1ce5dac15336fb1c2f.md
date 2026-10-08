The following kernel implements a matrix transpose with shared memory. It can be viewed as an extension of the setRowReadCol kernel discussed earlier the chapter. The difference between these kernels is that setRowReadCol handles the transpose of a single block of the input matrix using one thread. The kernel transposesSmem extends the transpose operations to use multiple blocks and multiple data.

```
__global void transposeSmem(float *out, float *in, int nx, int ny) {
    // static shared memory
    shared__ float tile[BDIMY][BDIMY];
    // coordinate in original matrix
    unsigned int ix,iy,ti;
    ix = blockIdx.x*blockDim.x + threadIdx.x;
    iy = blockIdx.y*blockDim.y + threadIdx.y;
    // linear global memory index for original matrix
    ti = iy*nx + ix;
    // thread index in transposed block
    unsigned int bix,row,icol;
    bix = threadIdx.y*blockDim.x + threadIdx.x;
    row = bix/blockDim.y;
    icol = bix%blockDim.y;
    // coordinate in transposed matrix
    ix = blockIdx.x * blockDim.y + icol;
    iy = blockIdx.y * blockDim.x + row;
    // linear global memory index for transposed matrix
    to = iy*ny + ix;
    
    if (ix < nx && iy < ny) {
        // load data from global memory to shared memory
        tile[threadIdx.x][threadIdx.y] = in[ti];
        // thread synchronization
        syncthreads();
        // store data to global memory from shared memory
        out[to] = tile[icol][row];
    }
}
```

kernelntransSmem can be broken down into the following steps:

+   1. A warp performs a coalesced read of a row from a block of the original matrix stored in global memory.
2. The warp then writes the data into shared memory using row-major ordering. As a result, there are no bank conflicts for this thread.
3. After all read/write operations in the thread block are synchronized, you have a 2D shared memory array filled with data from global memory.