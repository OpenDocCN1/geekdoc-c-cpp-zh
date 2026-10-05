# CUDA Kernel for Adding Two Arrays

Let’s illustrate this with a basic CUDA example. The goal of this example is to create two arrays of integers and add them together element-wise, storing the result in a third array. This operation will be performed in parallel on a GPU.

First, we need to include the CUDA headers:

```
#include #include
```

Following that, we define our CUDA which performs the addition:

```
__global void *a, int *b, int *c, int N) { index = threadIdx.x + blockIdx.x * blockDim.x; (index < N) = a[index] + b[index]; }
```

In this ‘__global_’ qualifier indicates that this function is a kernel that runs on the GPU but can be called from the host code (CPU). The variables ‘a’, ‘b’, and ‘c’ represent pointers to the arrays that will be used for the addition, and ‘N’ represents the size of the arrays. The line calculating the ‘index’ identifies the unique index of the thread within the parallel execution context, allowing each thread to operate on a different element of the arrays.

Next, we write the host code to allocate memory, initialize the arrays, and call the