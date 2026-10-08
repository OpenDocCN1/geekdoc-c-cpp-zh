unsigned int iy = blockIdx.x * blockDim.y + threadIdx.y;
unsigned int idx = iy * NX + ix;

```
if (ix < NX && iy < NY) {
  C[idx] = A[idx] + B[idx];
}
```

# A grid of a kernel

![](bbox=[0.147, 0.237, 0.745, 0.545])

Specify a large matrix with 16,384 elements in each dimension:

```
int nx = 1<<14;
int ny = 1<<14;
```

The following code snippet allows block dimensions to be configurable from the command line:

```
if (argc > 2) {
  dimx = atoi(argv[1]);
  dimy = atoi(argv[2]);
}

dim3 block(dimx, dimy);
dim3 grid((nx + block.x - 1) / block.x, (ny + block.y - 1) / block.y);
```

You can find the full code for this example in sumMatrix.cu, downloadable from Wrox.com. Compile it with the following command:

```
$ nvcc -O3 -arch=sm_20 sumMatrix.cu -o sumMatrix
```

You will use the generated sumMatrix executable to experiment with block and grid configurations in upcoming sections.