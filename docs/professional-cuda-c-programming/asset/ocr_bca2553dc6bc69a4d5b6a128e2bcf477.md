```
} else {
  b = 200.0f;
}
c[tid] = a + b;

```

If you interleave data using a warp approach (instead of a thread approach), you can avoid warp divergence and achieve 100 percent utilization of the device. The condition (tid/warpSize)%2==0 forces the branch granularity to a multiple of warp size; the even warps take the if, and the odd warps take the else. This kernel produces the same output, but in a different order.

```
_global void warpKernel2(void) {
  int tid = blockDim.x * blockDim.x + threadIdx.x;
  float a, b;
  a = 0.0f;

  if ((tid / warpSize) % 2 == 0) {
    a = 100.0f;
  } else {
    b = 200.0f;
  }
  c[tid] = a + b;
}
```

Now you can measure the performance of these two kernels using the code in Listing 3-1. You can also download the file simpleDivergence.cu from Wrox.com. Because the first run on a device may have added overhead and the performance being measured here is very-grained, an extra kernel launch (warmingup, which is the same as mainKernel2) is added to remove this overhead.

# LISTING 3-1: simple warp (simpleDivergence.cu) (main function only)

```
int main(int argc, char **argv) {
  // set up device
  int dev = 0;
  cudaDeviceProp deviceProp;
  cudaGetDeviceProperties(&deviceProp, dev);
  printf("Using Device %d: %s\n", argv[0],dev, deviceProp.name);

  // set up data size
  int size = 64;
  int blockSize = 64;
  if(argc > 1) blockSize = atoi(argv[1]);
  if(argc > 2) size = atoi(argv[2]);
  printf("Data size %d *\n", size, size);

  // set up execution configuration
  dim3 block(blockSize,1);
  dim3 grid((size+block.x-1)/block.x,1);
  printf("Execution Configuration (block %d grid %d)\n",block.x, grid.x);

  // allocate gpu memory
  float *d_C;
  size_t nBytes = size * sizeof(float);
```