For a given thread, the input matrix coordinates and the index into the global memory array used to store the input matrix are calculated as follows:

```
ix = blockIdx.x * blockDim.x * 2 + threadIdx.y;
y = blockIdx.x * blockDim.y + threadIdx.x;
ti = iy * nx + ix;
```

As illustrated in Figure 5-17, a block configuration of 32 x 16 is used with an unrolled block of size (32 + 32) x 16.

The new index in the transposed block in shared memory is calculated as follows:

```
bidx = threadIdx.y * blockDim.x + threadIdx.x;
irow = bidx / blockDim.y;
col_idx = icol * (blockDim.x * 2 + IPAD)
```

Because the shared memory array tile is 1D, the 2D thread index must be converted to a 1D shared memory index order to access the padded index

```
row_idx = threadIdx.y * (blockDim.x * 2 + IPAD) + threadIdx.x;
col_idx = icol * (blockDim.x * 2 + IPAD) + irow;
```

Because the padded memory is not used to store data, padded columns must be skipped when calculating indices.

Finally, the output matrix coordinates in the transposed matrix and the corresponding index into global memory used to store the result are calculated as follows:

```
ix2 = blockIdx.y * blockDim.y * 2 + icol;
y2 = blockIdx.x * blockDim.x * 2 + irow;
to = iy2 * ny + ix2;
```

![](bbox=[0.147, 0.586, 0.768, 0.873])

FIGURE 5-17