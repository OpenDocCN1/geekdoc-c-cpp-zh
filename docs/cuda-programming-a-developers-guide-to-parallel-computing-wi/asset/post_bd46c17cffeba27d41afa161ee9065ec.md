
Have you noticed the small error we have introduced in adding in another block? You will now launch 256 threads in total and index array from 0 to 255. If you don't also change the size of the array, from 128 elements to 256 elements, you will access and write beyond the end of the array. This array out-of-bounds error will not be caught by the compiler and the code may actually run, depending on what is located after the destination array. Be careful when invoking a kernel that you do not access out of bounds elements.

For this example, we will stick with the 128-byte array size and change the kernel to invoke two blocks of 64 threads each.

```cpp
some_kernel_func<<< 2, 64 >>>(a, b, c);
```

Thus, you get what is shown in Figure 5.8.

Notice how, despite now having two blocks, the thread_idx parameter still equates to the array index, exactly as before. So what is the point of using blocks? In this trivial example, absolutely nothing. However, in any real-world problem, you have far more than 512 elements to deal with. In fact, if you look at the limit on the number of blocks, you find you have 65,536 blocks you can use.

At 65,536 blocks, with 512 threads per block, you can schedule 33,554,432 (around 33.5 million) threads in total. At 512 threads, you can have up to three blocks per SM. Actually, this limit is based on the total number of threads per SM, which is 1536 in the latest Fermi hardware, and as little as 768 in the original G80 hardware.

If you schedule the maximum of 1024 threads per block on the Fermi hardware, 65,536 blocks would translate into around 64 million threads. Unfortunately, at 1024 threads, you only get one thread block per SM. Consequently, you'd need some 65,536 SMs in a single GPU before you could not allocate at least one block per SM. Currently, the maximum number of SMs found on any card is 30. Thus, there is some provision for the number of SMs to grow before you have more SMs than the number of blocks the hardware can support. This is one of the beauties of CUDA—the fact it can scale to thousands of execution units. The limit of parallelism is really only the limit of the amount of parallelism that can be found in the application.

With 64 million threads, assuming one thread per array element, you can process up to 64 million elements. Assuming each element is a single-precision floating-point number, requiring 4 bytes of data, you'd need around 256 million bytes, or 256 MB, of data storage space. Almost all GPU cards support at least this amount of memory space, so working with threads and blocks alone you can achieve quite a large amount of parallelism and data coverage.

| Block 0 Warp 0 (Thread 0 to 31) | Block 0 Warp 1 (Thread 32 to 63) | Block 1 Warp 0 (Thread 64 to 95) | Block 1 Warp 1 (Thread 96 to 127) |
| :--- | :--- | :--- | :--- |
| Address 0 to 31 | Address 32 to 63 | Address 64 to 95 | Address 96 to 127 |

FIGURE 5.8 Block mapping to address.

For anyone worried about large datasets, where large problems can run into gigabytes, terabytes, or petabytes of data, there is a solution. For this, you generally either process more than one element per thread or use another dimension of blocks, which we'll cover in the next section.

## Block arrangement

To ensure that we understand the block arrangement, we're going to write a short kernel program to print the block, thread, warp, and thread index to the screen. Now, unless you have at least version 3.2 of the SDK, the `printf` statement is not supported in kernels. So we'll ship the data back to the CPU and print it to the console window. The kernel program is thus as follows:

```cpp
__global__ void what_is_my_id(unsigned int * const block,
                              unsigned int * const thread,
                              unsigned int * const warp,
                              unsigned int * const calc_thread)
{
    /* Thread id is block index * block size + thread offset into the block */
    const unsigned int threadIdx = (blockIdx.x * blockDim.x) + threadIdx.x;

    block[threadIdx] = blockIdx.x;
    thread[threadIdx] = threadIdx.x;

    /* Calculate warp using built in variable warpSize */
    warp[threadIdx] = threadIdx.x / warpSize;

    calc_thread[threadIdx] = threadIdx;
}
```

Now on the CPU you have to run a section of code, as follows, to allocate memory for the arrays on the GPU and then transfer the arrays back from the GPU and display them on the CPU.

```cpp
#include <stdio.h>
#include <stdlib.h>
#include <conio.h>
__global__ void what_is_my_id(unsigned int * const block,
                              unsigned int * const thread,
                              unsigned int * const warp,
                              unsigned int * const calc_thread)
{
    /* Thread id is block index * block size + thread offset into the block */
    const unsigned int threadIdx = (blockIdx.x * blockDim.x) + threadIdx.x;

    block[threadIdx] = blockIdx.x;
    thread[threadIdx] = threadIdx.x;

    /* Calculate warp using built in variable warpSize */
    warp[threadIdx] = threadIdx.x / warpSize;

    calc_thread[threadIdx] = threadIdx;
}

#define ARRAY_SIZE 128
#define ARRAY_SIZE_IN_BYTES (sizeof(unsigned int) * (ARRAY_SIZE))

/* Declare statically four arrays of ARRAY_SIZE each */

unsigned int cpu_block[ARRAY_SIZE];
unsigned int cpu_thread[ARRAY_SIZE];
unsigned int cpu_warp[ARRAY_SIZE];
unsigned int cpu_calc_thread[ARRAY_SIZE];

int main(void)
{
    /* Total thread count = 2 * 64 = 128 */
    const unsigned int num_blocks = 2;
    const unsigned int num_threads = 64;
    char ch;

    /* Declare pointers for GPU based params */
    unsigned int * gpu_block;
    unsigned int * gpu_thread;
    unsigned int * gpu_warp;
    unsigned int * gpu_calc_thread;

    /* Declare loop counter for use later */
    int i;

    /* Allocate four arrays on the GPU */
    cudaMalloc((void **)&gpu_block, ARRAY_SIZE_IN_BYTES);
    cudaMalloc((void **)&gpu_thread, ARRAY_SIZE_IN_BYTES);
    cudaMalloc((void **)&gpu_warp, ARRAY_SIZE_IN_BYTES);
    cudaMalloc((void **)&gpu_calc_thread, ARRAY_SIZE_IN_BYTES);

    /* Execute our kernel */
    what_is_my_id<<<num_blocks, num_threads>>>(gpu_block, gpu_thread, gpu_warp,
                                               gpu_calc_thread);

    /* Copy back the gpu results to the CPU */
    cudaMemcpy(cpu_block, gpu_block, ARRAY_SIZE_IN_BYTES,
               cudaMemcpyDeviceToHost);
    cudaMemcpy(cpu_thread, gpu_thread, ARRAY_SIZE_IN_BYTES,
               cudaMemcpyDeviceToHost);
    cudaMemcpy(cpu_warp, gpu_warp, ARRAY_SIZE_IN_BYTES,
               cudaMemcpyDeviceToHost);
    cudaMemcpy(cpu_calc_thread, gpu_calc_thread, ARRAY_SIZE_IN_BYTES,
               cudaMemcpyDeviceToHost);

    /* Free the arrays on the GPU as now we're done with them */
    cudaFree(gpu_block);
    cudaFree(gpu_thread);
    cudaFree(gpu_warp);
    cudaFree(gpu_calc_thread);

    /* Iterate through the arrays and print */
    for (i = 0; i < ARRAY_SIZE; i++)
    {
        printf("Calculated Thread: %3u - Block: %2u - Warp %2u - Thread %3u\n",
               cpu_calc_thread[i], cpu_block[i], cpu_warp[i], cpu_thread[i]);
    }

    ch = getch();
}
```

In this example, what you see is that each block is located immediately after the one before it. As you have only a single dimension to the array, laying out the thread blocks in a similar way is an easy way to conceptualize a problem. The output of the previous program is as follows:

```
Calculated Thread: 0 - Block: 0 - Warp 0 - Thread 0
Calculated Thread: 1 - Block: 0 - Warp 0 - Thread 1
Calculated Thread: 2 - Block: 0 - Warp 0 - Thread 2
Calculated Thread: 3 - Block: 0 - Warp 0 - Thread 3
Calculated Thread: 4 - Block: 0 - Warp 0 - Thread 4
...
Calculated Thread: 30 - Block: 0 - Warp 0 - Thread 30
Calculated Thread: 31 - Block: 0 - Warp 0 - Thread 31
Calculated Thread: 32 - Block: 0 - Warp 1 - Thread 32
Calculated Thread: 33 - Block: 0 - Warp 1 - Thread 33
Calculated Thread: 34 - Block: 0 - Warp 1 - Thread 34
...
Calculated Thread: 62 - Block: 0 - Warp 1 - Thread 62
Calculated Thread: 63 - Block: 0 - Warp 1 - Thread 63
Calculated Thread: 64 - Block: 1 - Warp 0 - Thread 0
Calculated Thread: 65 - Block: 1 - Warp 0 - Thread 1
Calculated Thread: 66 - Block: 1 - Warp 0 - Thread 2
Calculated Thread: 67 - Block: 1 - Warp 0 - Thread 3
...
Calculated Thread: 94 - Block: 1 - Warp 0 - Thread 30
Calculated Thread: 95 - Block: 1 - Warp 0 - Thread 31
Calculated Thread: 96 - Block: 1 - Warp 1 - Thread 32
Calculated Thread: 97 - Block: 1 - Warp 1 - Thread 33
Calculated Thread: 98 - Block: 1 - Warp 1 - Thread 34
Calculated Thread: 99 - Block: 1 - Warp 1 - Thread 35
Calculated Thread: 100 - Block: 1 - Warp 1 - Thread 36
...
Calculated Thread: 126 - Block: 1 - Warp 1 - Thread 62
Calculated Thread: 127 - Block: 1 - Warp 1 - Thread 63
```
