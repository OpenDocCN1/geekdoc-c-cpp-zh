The following code examples illustrate how the use of managed memory can change the way in which host code is written. First, a simple program written without the benefit of Unified Memory:

```
```cpp
__global__ void AplusB(int *ret, int a, int b) {
    ret[threadIdx.x] = a + b + threadIdx.x;
}

int main() {
    int *ret;
    cudaMalloc((ret, 1000 * sizeof(int));
    AplusB<<< 1, 1000 >>>(ret, 10, 100);
    int *host_ret = (int *)malloc(1000 * sizeof(int));
    cudaMemcpy(host_ret, ret, 1000 * sizeof(int), cudaMemcpyDefault);
    for(int i = 0; i < 1000; i++)
        printf("%d: A+B = %d\n", i, host_ret[i]);
    free(host_ret);
    cudaFree(ret);
    return 0;
}
```
```

This first example combines two numbers together on the GPU with a per-thread ID and returns the values in an array. Without managed memory, both host- and device-side storage for the return values is required (host_ret and ret in the example), as is an explicit copy between the two using cudaMemcpy().

Compare this with the Unified Memory version of the program, which allows direct access of GPU data from the host. Notice the cudaMallocManaged() routine, which returns a pointer valid from both host and device code. This allows ret to be used without a separate host_ret copy, greatly simplifying and reducing the size of the program.

```
```cpp
__global__ void AplusB(int *ret, int a, int b) {
    ret[threadIdx.x] = a + b + threadIdx.x;
}

int main() {
    int *ret;
    cudaMallocManaged((ret, 1000 * sizeof(int));
    AplusB<<< 1, 1000 >>>(ret, 10, 100);
    cudaDeviceSynchronize();
    for(int i = 0; i < 1000; i++)
        printf("%d: A+B = %d\n", i, ret[i]);
    cudaFree(ret);
    return 0;
}
```
```

Finally, language integration allows direct reference of a GPU-declared __managed__ variable and simplifies a program further when global variables are used.

```
```cpp
device __managed__ int ret[1000];
__global__ void AplusB(int a, int b) {
    ret[threadIdx.x] = a + b + threadIdx.x;
}

int main() {
    AplusB<<< 1, 1000 >>>(10, 100);
    cudaDeviceSynchronize();
    for(int i = 0; i < 1000; i++)
        printf("%d: A+B = %d\n", i, ret[i]);
    return 0;
}
```
```

Note the absence of explicit cudaMemcpy() commands and the fact that the return array ret is visible on both CPU and GPU.