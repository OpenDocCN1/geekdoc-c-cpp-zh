In a matrix addition kernel, a thread is usually assigned one data element to process. Accessing the assigned data from global memory using block and thread index is the first issue you need to solve. Typically, there are three kinds of indices for a 2D case you need to manage:

+   - Thread and block index
- Coordinate of a given point in the matrix
- Offset in linear global memory

For a given thread, you can obtain the offset in global memory by the block and thread index by first mapping the thread and block index to coordinates in the matrix, then mapping those coordinates to a global memory location.

In the first step, you can map the thread and block index to the coordinate of a matrix with the following formula:

```
ix = threadIdx.x + blockIdx.x * blockDim.x
y = threadIdx.y + blockIdx.y * blockDim.y
```

In the second step, you can map a matrix coordinate to a global memory location/index with the following formula:

```
idx = iy * nx + ix
```

Figure 2-10 illustrates the relationship among block and thread indices, matrix coordinates, and linear global memory indices.

![](bbox=[0.095, 0.513, 0.6, 0.765])

matrix coordinate: (ix, iy)
global linear memory index: idx = iy*nx + ix

FIGURE 2-10