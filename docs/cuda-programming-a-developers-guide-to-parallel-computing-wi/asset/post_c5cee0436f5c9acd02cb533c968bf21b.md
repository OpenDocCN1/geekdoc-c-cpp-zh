
```c
#include "const_common.h"
#include "stdio.h"
#include "conio.h"
#include "assert.h"

#define CUDA_CALL(x) (const cudaError_t a = (x); if (a != cudaSuccess) { printf("\nCUDA Error: %s (err_num=%d)\n", cudaGetErrorString(a), a); cudaDeviceReset(); assert(0); } )
#define KERNEL_LOOP 65536
```

```c
constant static const u32 const_data_01 = 0x55555555;
constant static const u32 const_data_02 = 0x77777777;
constant static const u32 const_data_03 = 0x33333333;
constant static const u32 const_data_04 = 0x11111111;
```

```c
__global__ void const_test_gpu_literal(u32 * const data, const u32 num_elements)
{
    const u32 tid = (blockIdx.x * blockDim.x) + threadIdx.x;
    if (tid < num_elements)
    {
        u32 d = 0x55555555;

        for (int i = 0; i < KERNEL_LOOP; i++)
        {
            d ^= 0x55555555;
            d |= 0x77777777;
            d &= 0x33333333;
            d ^= 0x11111111;
        }

        data[tid] = d;
    }
}
```

```c
__global__ void const_test_gpu_const(u32 * const data, const u32 num_elements)
{
    const u32 tid = (blockIdx.x * blockDim.x) + threadIdx.x;
    if (tid < num_elements)
    {
        u32 d = const_data_01;

        for (int i = 0; i < KERNEL_LOOP; i++)
        {
            d ^= const_data_01;
            d |= const_data_02;
            d &= const_data_03;
            d ^= const_data_04;
        }

        data[tid] = d;
    }
}
```

```c
__host__ void wait_exit(void)
{
    char ch;

    printf("\nPress any key to exit");
    ch = getch();
}
```

```c
__host__ void cuda_error_check(
    const char * prefix,
    const char * postfix)
{
    if (cudaPeekAtLastError() != cudaSuccess)
    {
        printf("\n%s%s%s", prefix, cudaGetErrorString(cudaGetLastError()), postfix);
        cudaDeviceReset();
        wait_exit();
        exit(1);
    }
}
```

```c
__host__ void gpu_kernel(void)
{
    const u32 num_elements = (128*1024);
    const u32 num_threads = 256;
    const u32 num_blocks = (num_elements+(num_threads-1)) / num_threads;
    const u32 num_bytes = num_elements * sizeof(u32);
    int max_device_num;
    const int max_runs = 6;

    CUDA_CALL(cudaGetDeviceCount(&max_device_num));

    for (int device_num=0; device_num < max_device_num; device_num++)
    {
        CUDA_CALL(cudaSetDevice(device_num));

        for (int num_test=0; num_test < max_runs; num_test++)
        {
            u32 * data_gpu;
            cudaEvent_t kernel_start1, kernel_stop1;
            cudaEvent_t kernel_start2, kernel_stop2;
            float delta_time1 = 0.0F, delta_time2=0.0F;
            struct cudaDeviceProp device_prop;
            char device_prefix[256];

            CUDA_CALL(cudaMalloc(&data_gpu, num_bytes));
            CUDA_CALL(cudaEventCreate(&kernel_start1));
            CUDA_CALL(cudaEventCreate(&kernel_stop2));
            CUDA_CALL(cudaEventCreateWithFlags(&kernel_start1, cudaEventBlockingSync));
            CUDA_CALL(cudaEventCreateWithFlags(&kernel_stop2, cudaEventBlockingSync));

            // printf("\nLaunching %u blocks, %u threads, num_blocks, num_threads);
            CUDA_CALL(cudaGetDeviceProperties(&device_prop, device_num));
            snprintf(device_prefix, 256, "ID%d %s", device_num, device_prop.name);

            // Warm up run
            // printf("\nLaunching literal kernel warm-up");
            const_test_gpu_literal <<<num_blocks, num_threads>>>(data_gpu, num_elements);
            cuda_error_check("Error: ", "returned from literal startup kernel");

            // Do the literal kernel
            // printf("\nLaunching literal kernel");
            CUDA_CALL(cudaEventRecord(kernel_start1,0));
            const_test_gpu_literal <<<num_blocks, num_threads>>>(data_gpu, num_elements);
            cuda_error_check("Error: ", "returned from literal runtime kernel");

            CUDA_CALL(cudaEventRecord(kernel_stop1,0));
            CUDA_CALL(cudaEventSynchronize(kernel_stop1));
            CUDA_CALL(cudaEventElapsedTime(&delta_time1, kernel_start1, kernel_stop1));
            // printf("\nLiteral Elapsed time: %.3fms", delta_time1);

            // Warm up run
            // printf("\nLaunching constant kernel warm-up");
            const_test_gpu_const <<<num_blocks, num_threads>>>(data_gpu, num_elements);
            cuda_error_check("Error: ", "returned from constant startup kernel");

            // Do the constant kernel
            // printf("\nLaunching constant kernel");
            CUDA_CALL(cudaEventRecord(kernel_start2,0));
            const_test_gpu_const <<<num_blocks, num_threads>>>(data_gpu, num_elements);
            cuda_error_check("Error: ", "returned from constant runtime kernel");

            CUDA_CALL(cudaEventRecord(kernel_stop2,0));
            CUDA_CALL(cudaEventSynchronize(kernel_stop2));
            CUDA_CALL(cudaEventElapsedTime(&delta_time2, kernel_start2, kernel_stop2));
            // printf("\nConst Elapsed time: %.3fms", delta_time2);

            if (delta_time1 > delta_time2)
                printf("\n%sConstant version is faster by: %.2fms (Const=%.2fms vs. Literal=%.2fms)",
                device_prefix, delta_time1-delta_time2, delta_time1, delta_time2);
            else
                printf("\n%sLiteral version is faster by: %.2fms (Const=%.2fms vs. Literal=%.2fms)",
                device_prefix, delta_time2-delta_time1, delta_time1, delta_time2);

            CUDA_CALL(cudaEventDestroy(kernel_start1));
            CUDA_CALL(cudaEventDestroy(kernel_start2));
            CUDA_CALL(cudaEventDestroy(kernel_stop1));
            CUDA_CALL(cudaEventDestroy(kernel_stop2));
            CUDA_CALL(cudaFree(data_gpu));
        }

        CUDA_CALL(cudaDeviceReset());
        printf("\n");
    }
    wait_exit();
}
```

This program consists of two GPU kernels, const_test_gpu_literal and const_test_gpu_const. Notice how each is declared with the __global__ prefix to say this function has public scope. Each of these kernels fetches some data as either constant data or literal data within the for loop, and uses it to manipulate the local variable d. It then writes this manipulated value out to global memory. This is necessary only to avoid the compiler optimizing away the code.

The next section of code gets the number of CUDA devices present and iterates through the devices using the cudaSetDevice call. Note that this is possible because at the end of the loop the host code calls cudaDeviceReset to clear the current context.

Having set the device, the program allocates some global memory and creates two events, a start and a stop timer event. These events are fed into the execution stream, along with the kernel call. Thus, you end up with the stream containing a start event, a kernel call, and a stop event. These events would normally happen asynchronously with the CPU, that is, they do not block the execution of the CPU and execute in parallel. This causes some problems when trying to do timing, as a CPU timer would see no elapsed time. The program, therefore, calls cudaEventSynchronize to wait on the last event, the kernel stop event, to complete. It then calculates the delta time between the start and stop events and thus knows the execution time of the kernel.

This is repeated for the constant and literal kernels, including the execution of a warm-up call to avoid any initial effects of filling any caches. The results are shown as follows:

| ID | Device | Faster Version | Difference (ms) | Constant (ms) | Literal (ms) |
|----|--------|----------------|-----------------|---------------|--------------|
| 0 | GeForce GTX 470 | Constant | 0.00 | 345.23 | 345.23 |
| 0 | GeForce GTX 470 | Constant | 0.01 | 330.95 | 330.94 |
| 0 | GeForce GTX 470 | Literal | 0.00 | 336.60 | 336.60 |
| 0 | GeForce GTX 470 | Constant | 5.67 | 336.60 | 330.93 |
| 0 | GeForce GTX 470 | Constant | 5.59 | 336.60 | 331.01 |
| 0 | GeForce GTX 470 | Constant | 14.30 | 345.23 | 330.94 |
| 1 | GeForce 9800 GT | Literal | 4.04 | 574.85 | 578.89 |
| 1 | GeForce 9800 GT | Literal | 3.55 | 578.18 | 581.73 |
| 1 | GeForce 9800 GT | Literal | 4.68 | 575.85 | 580.53 |
| 1 | GeForce 9800 GT | Constant | 5.25 | 581.06 | 575.81 |
| 1 | GeForce 9800 GT | Literal | 4.01 | 572.08 | 576.10 |
| 1 | GeForce 9800 GT | Constant | 8.47 | 578.40 | 569.93 |
| 2 | GeForce GTX 260 | Literal | 0.27 | 348.74 | 349.00 |
| 2 | GeForce GTX 260 | Literal | 0.26 | 348.72 | 348.98 |
| 2 | GeForce GTX 260 | Literal | 0.26 | 348.74 | 349.00 |
| 2 | GeForce GTX 260 | Literal | 0.26 | 348.74 | 349.00 |
| 2 | GeForce GTX 260 | Literal | 0.13 | 348.83 | 348.97 |
| 2 | GeForce GTX 260 | Literal | 0.27 | 348.73 | 348.99 |
| 3 | GeForce GTX 460 | Literal | 0.59 | 541.43 | 542.02 |
| 3 | GeForce GTX 460 | Literal | 0.17 | 541.20 | 541.37 |
| 3 | GeForce GTX 460 | Constant | 0.45 | 542.29 | 541.83 |
| 3 | GeForce GTX 460 | Constant | 0.27 | 542.17 | 541.89 |
| 3 | GeForce GTX 460 | Constant | 1.17 | 543.55 | 542.38 |
| 3 | GeForce GTX 460 | Constant | 0.24 | 542.92 | 542.68 |

What is interesting to note is that there is very little, if any, difference in the execution time if you look at this as a percentage of the total execution time. Consequently we see a fairly random distribution as to which version, the constant or the literal, is faster. Now how does this compare with using global memory? To test this, we simply replace the literal kernel with one that uses global memory as shown in the following:

```c
__device__ static u32 data_01 = 0x55555555;
__device__ static u32 data_02 = 0x77777777;
__device__ static u32 data_03 = 0x33333333;
__device__ static u32 data_04 = 0x11111111;

__global__ void const_test_gpu_mem(u32 * const data, const u32 num_elements)
{
    const u32 tid = (blockIdx.x * blockDim.x) + threadIdx.x;
    if (tid < num_elements)
    {
        u32 d = 0x55555555;

        for (int i = 0; i < KERNEL_LOOP; i++)
        {
            d ^= data_01;
            d |= data_02;
            d &= data_03;
            d |= data_04;
        }

        data[tid] = d;
```
