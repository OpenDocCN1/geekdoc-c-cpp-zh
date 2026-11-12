![](bbox=[0.29, 0.09, 0.76, 0.54])

# Figure 6 Grid of Thread Blocks

The number of threads per block and the number of blocks per grid specified in the <<< ... >>> syntax can be of type int or dim3. Two-dimensional blocks or grids can be specified as in the example above.

Each block within the grid can be identified by a one-dimensional, two-dimensional, or three-dimensional unique index accessible within the kernel through the built-in blockIdx variable. The dimension of the thread block is accessible within the kernel through the built-in blockDim variable.