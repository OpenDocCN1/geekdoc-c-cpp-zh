
![](img/506ba3a4c9f4512233692f3f20de1f3a_132_0.png)

FIGURE 3-19

![](img/506ba3a4c9f4512233692f3f20de1f3a_132_1.png)

FIGURE 3-20

The following function is a recursive implementation of the interleaved pair approach:

```cpp
int recursiveReduce(int *data, int const size) {
  // terminate check
  if (size == 1) return data[0];

  // renew the stride
  int const stride = size / 2;

  // in-place reduction
  for (int i = 0; i < stride; i++) {
    data[i] += data[i + stride];
  }

  // call recursively
  return recursiveReduce(data, stride);
}
```

The code above implements addition, any commutative and associative operation could replace addition. For example, the maximum value in the input vector could be calculated by replacing the sum with a max. Other example valid operations are minimum, average, and product.

This general problem of performing a commutative and associative operation across a vector is known as the reduction problem. Parallel reduction is the parallel execution of this operation. Parallel reduction is one of the most common patterns, and a key operation in many algorithms. In this section, you will implement several different parallel kernels, and examine how different implementations affect performance.

## Divergence in Parallel Reduction

As a starting point, you will experiment with kernel implementing the neighboring pair approach illustrated in Figure 3-21. Each thread adds two adjacent elements to produce a partial sum.

![](img/506ba3a4c9f4512233692f3f20de1f3a_133_0.png)

FIGURE 3-21

In this kernel, there are two global memory arrays: one large array for storing the entire array to reduce, and one smaller array for holding partial sums of each thread block. Each thread block operates independently on a portion of the array. One iteration of the loop performs a single reduction step. The reduction is done in-place, which means that the values in global memory are replaced by partial sums at each step. __syncthreads() statement ensures that all partial sums for every thread in the current iteration have saved to global memory before any threads enter the next iteration. After the final round, the sum for the entire block is saved into global memory.

```cpp
void reduceNeighbor(int *g_idata, int *g_odata, unsigned int n) {
  // set thread ID
  unsigned int tid = threadIdx.x;

  // convert global data to local pointer
  int *idata = g_idata + blockIdx.x * blockDim.x;

  // boundary check
  if (tid == n) return;

  // in-place reduction in global memory
  for (int stride = 1; stride < blockDim.x; stride *= 2) {
    if (tid % (2 * stride) == 0) {
      idata[tid] += idata[tid + stride];
    }
  }
  // synchronize within block
  __syncthreads();
}
```

The distance between neighbor elements, stride, is initialized to 1 at first. After each reduction round, this distance is multiplied by 2. After the first round, the even elements of idata will be replaced by partial sums. After the second round, every fourth element of idata will be replaced with further partial sums. Because there is no synchronization between threads, the partial sum produced by each thread block is copied back to the host and summed sequentially, as illustrated in Figure 3-22.

![](img/506ba3a4c9f4512233692f3f20de1f3a_134_0.png)

FIGURE 3-22

You can find the full source code in reduceInteger.cu available from cuda.com. Listing 3-3 shows only the main function.

## LISTING 3-3: Reduce integer (reduceInteger.cu, main function only)

```cpp
int main(int argc, char **argv) {
  // set up device
  int dev = 0;
  cudaDeviceProp deviceProp;
  cudaDeviceProperties(&deviceProp, dev);
  printf("%s starting reduction at %s", argv[0]);
  printf("%d: %s", dev, deviceProp.name);
  cudaSetDevice(dev);
  bool result = false;

  // initialization
  int size = 1<<24; // total number of elements to reduce
  printf("%d with array size %d", size);

  // execution configuration
  int blocksize = 512; // initial block size
  if(argc > 1) {
    blocksize = atoi(argv[1]); // block size from command line argument
  }
  dim3 block(blocksize, 1);
  dim3 grid((size + block.x - 1) / block.x, 1);
  printf("grid %d block %d\n", grid.x, block.x);

  // allocate memory
  size_t bytes = size * sizeof(int);
  int *h_idata = (int *)malloc(bytes);
  int *h_odata = (int *)malloc(grid.x * sizeof(int));
  int *tmp = (int *)malloc(bytes);

  // initialize the array
  for (int i = 0; i < size; i++) {
    // mask off high 2 bytes to force number to 255
    h_idata[i] = (int)(rand() & 0xFF);
  }
  memcpy(tmp, h_idata, bytes);

  size_t tStart, iElaps;
  int gpu_sum = 0;

  // allocate device memory
  int *idata = NULL;
  int *odata = NULL;
  cudaMalloc((void **) &idata, bytes);
  cudaMalloc((void **) &odata, grid.x * sizeof(int));

  // cpu reduction
  iStart = seconds();
  int cpu_sum = recursiveReduce(tmp, size);
  iElaps = seconds() - iStart;
  printf("cpu reduce elapsed %d ms cpu-sum: %d\n", iElaps, cpu_sum);

  // kernel 1: reduceNeighbor
  cudaMemcpy(idata, h_idata, bytes, cudaMemcpyHostToDevice);

  cudaDeviceSynchronize();
  tStart = seconds();
  warmup<<<grid, block>>>(idata, oodata, size);
  cudaDeviceSynchronize();
  iElaps = seconds() - tStart;

  // copy results back to host
  cudaMemcpy(h_odata, odata, grid.x * sizeof(int), cudaMemcpyDeviceToHost);

  // sum results
  gpu_sum = 0;
  for (int i = 0; i < grid.x; i++) {
    gpu_sum += h_odata[i];
  }
  printf("gpu reduce elapsed %d ms gpu-sum: %d\n", iElaps, gpu_sum);

  result = (gpu_sum == cpu_sum);
  if(!result) printf("Test failed!\n");

  // free memory
  free(h_idata);
  free(h_odata);
  free(tmp);
  cudaFree(idata);
  cudaFree(odata);

  return EXIT_SUCCESS;
}
```
