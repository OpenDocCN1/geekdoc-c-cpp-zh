
compilation only happens if the executable does not contain a binary image that is identical to the GPU in use. Consequently, all future architectures are backward compatible with the basic-level virtual architecture. Even GPUs for which the program was not compiled will execute legacy GPU code by simply compiling at runtime the PTX code embedded in the executable.

Just as with Java, code repositories are supported. Defining the environment variable CUDA_DECODED_CACHE to point to a directory will cause the runtime to save the compiled binary for later use, thus avoiding the startup delay necessary to compile the PTX code for the unknown GPU variant every time it is invoked.

We cover in the later chapters how you can view the real target assembly code, the result of the PTX to target translation.

## ERROR HANDLING

Error handling in CUDA, as with C in general, is not as good as it could be. There are few runtime checks performed, and if you do something stupid, the runtime will usually allow it. This results in GPU programs that exit strangely. If you are lucky, you will get an error message which, like compiler errors, you learn to interpret over time.

Almost all function calls in CUDA return the error type cudaError_t, which is simply an integer value. Any value other than cudaSuccess will indicate a fatal error. This is usually caused by your program not setting up something correctly prior to use, or using an object after it has been destroyed. It can also be caused by the GPU kernel timeout present in Microsoft Windows if the kernel runs for more than a few seconds and you have not disabled this when installing tools such as Parallel Nsight (see previous section). Out-of-bounds memory accesses may generate exceptions that will often print various error messages to stderr (standard error output).

As every function returns an error code, every function call must be checked and some handler written. This makes for very tiresome and highly indented programming. For example,

```
if (cudaMalloc(...) == cudaSuccess)
{
    if (cudaEventCreate(&event) == cudaSuccess)
    {
    ...
    }
    else
    {
    ...
    }
}
```

To avoid this type of repetitive programming, throughout the book we will use the following macro definition to make calls to the CUDA API:

```
#define CUDA_CALL(x) { const cudaError_t a = (x); if (a != cudaSuccess) { printf("\nCUDA Error: %s (err_num=%d) \n", cudaGetErrorString(a), a); cudaDeviceReset(); assert(0); } }
```

What this macro does is to allow you to specify x as some function call, for example,

```
CUDA_CALL(cudaEventCreate(&kernel_start));
```

This then creates a temporary variable a and assigns to it the return value of the function, which is of type cudaError_t. It then checks if this is not equal to cudaSuccess, that is, the call encountered some error. If there was an error detected, it prints to the screen the error returned plus a short description of what the error means. It also uses the assert macro, which identifies the source file and line in which the error occurs so you can easily track down the point at which the error is being detected.

This technique works for all the CUDA calls except for the invocation of kernels. Kernels are the programs you write to run on the GPU. These are executed using the <<< and >>> operators as follows:

```
my_kernel <<<num_blocks, num_threads>>>(param1, param2...);
```

For error checking of kernels, we'll use the following function:

```c
__host__ void cuda_error_check(const char * prefix, const char * postfix)
{
    if (cudaPeekAtLastError() != cudaSuccess)
    {
        printf("\n%s%s", prefix, cudaGetErrorString(cudaGetLastError()), postfix);
        cudaDeviceReset();
        wait_exit();
        exit(1);
    }
}
```

This function should be called immediately after executing the kernel call. It checks for any immediate errors, and if so, prints an error message, resets the GPU, optionally waits for a key press via the wait_exit function, and then exits the program.

Note that this is not foolproof, as the kernel call is asynchronous with the CPU code. That is, the GPU code is running in the background at the time we call cudaPeekAtLastError. If there has been no error detected at this time, then we see no error printed and the function continues to the next code line. Often that next code line will be a copy back from GPU memory to CPU memory. The error in the kernel may cause a subsequent API call to fail, which is almost always the next API call after the kernel call. Surrounding all calls to the API with the CUDA_CALL macro will flag the error at this point.

You can also force the kernel to complete prior to the error checking by simply inserting a call to cudaDeviceSynchronize prior to the cudaPeekAtLastError call. However, only do this on the debug version of the program or where you want the CPU to idle while the GPU is busy. As you should understand by the end of this text, such synchronous operation is good for debugging, but will harm performance, so you should be careful these calls do not remain in production code if they were inserted solely for debugging.

## CONCLUSION

You should now have a working installation of the CUDA SDK, including the GPU computing SDK samples and a debugging environment. You should be able to build a simple GPU SDK sample, such as the deviceQuery project, and have it identify the GPUs in your system when run.

## Grids, Blocks, and Threads

5

### WHAT IT ALL MEANS

NVIDIA chose a rather interesting model for its scheduling, a variant of SIMD it calls SPMD (single program, multiple data). This is based on the underlying hardware implementation in many respects. At the heart of parallel programming is the idea of a thread, a single flow of execution through the program in the same way a piece of cotton flows through a garment. In the same way threads of cotton are woven into cloth, threads used together make up a parallel program. The CUDA programming model groups threads into special groups it calls warps, blocks, and grids, which we will look at in turn.

### THREADS

A thread is the fundamental building block of a parallel program. Most C programmers are familiar with the concept if they have done any multicore programming. Even if you have never launched a thread in any code, you will be familiar with executing at least one thread, the single thread of execution through any serial piece of code.

With the advent of dual, quad, hex core processors, and beyond, more emphasis is explicitly placed on the programmer to make use of such hardware. Most programs written in the past few decades, with the exception of perhaps the past decade, were single-threaded programs because the primary hardware on which they would execute was a single-core CPU. Sure, you had clusters and supercomputers that sought to exploit a high level of parallelism by duplicating the hardware and having thousands of commodity servers instead of a handful of massively powerful mainframes. However, these were mostly restricted to universities and large institutions, not generally available to the masses.

Thinking in terms of lots of threads is hard. It’s much easier to think in terms of one task at a time. Serial programming languages like C/C++ were born from a time when serial processing speed doubled every few years. There was little need to do the hard parallel programming. That stopped almost a decade ago, and now, like it or not, to improve program speed requires us to think in terms of parallel program design.

### Problem decomposition

Parallelism in the CPU domain tends to be driven by the desire to run more than one (single-threaded) program on a single CPU. This is the task-level parallelism that we covered earlier. Programs, which are data intensive, like video encoding, for example, use the data parallelism model and split the task in N parts where N is the number of CPU cores available. You might, for example, have each CPU core calculate one “frame” of data where there are no interdependencies between frames. You may also choose to split each frame into N segments and allocate each one of the segments to an individual core.

In the GPU domain, you see exactly these choices when attempting to speed up rendering of 3D worlds in computer games by using more than one GPU. You can send complete, alternate frames to each GPU (Figure 5.1). Alternatively, you can ask one GPU to render the different parts of the screen.

![](img/e0b192dbaf05f61ad420bee512a8c4e4_84_0.png)

FIGURE 5.1 Alternate frame rendering (AFR) vs. Split Frame Rendering (SFR).

![](img/e0b192dbaf05f61ad420bee512a8c4e4_84_1.png)

FIGURE 5.2 Coarse-grained parallelism.

However, there is a trade off here. If the dataset is self-contained, you can use less memory and transfer less data by only providing the GPU (or CPU) with the subset of the data you need to calculate. In the SFR GPU example used here, there may be no need for GPU3, which is rendering the floor to know the content of data from GPU0, which is probably rendering the sky. However, there may be shadows from a flying object, or the lighting level of the floor may need to vary based on the time of day. In such instances, it might be more beneficial to go with the alternate frame rendering approach because of this shared data.

We refer to SFR type splits as coarse-grained parallelism. Large chunks of data are split in some way between N powerful devices and then reconstructed later as the processed data. When designing applications for a parallel environment, choices at this level seriously impact the performance of your programs. The best choice here is very much linked to the actual hardware you will be using, as you will see with the various applications we develop throughout this book.

With a small number of powerful devices, such as in CPUs, the issue is often how to split the workload evenly. This is often easier to reason because you are typically talking about only a small number of devices. With huge numbers of smaller devices, as with GPUs, they average out peaks in workload much better, but suffer from issues around synchronization and coordination.

In the same way as you have macro (large-scale) and micro (small-scale) economics, you have coarse and fine-grained parallelism. However, you only really find fine-grained parallelism at the
