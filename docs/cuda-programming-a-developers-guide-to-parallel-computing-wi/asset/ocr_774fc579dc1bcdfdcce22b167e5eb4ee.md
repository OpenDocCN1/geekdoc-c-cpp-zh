compilation only happens if the executable does not contain a binary image that is identical to the GPU in use. Consequently, all future architectures are backward compatible with the basic-level virtual architecture. Even GPUs for which the program was not compiled will execute legacy GPU code by simply compiling at runtime the PTX code embedded in the executable.

Just as with Java code depositories are supported. Defining the environment variable CUDA_DECODED_CAHE to point to a directory will cause the runtime to save the compiled binary for later use, thus avoiding the startup delay necessary to compile the PTX code for the unknown GPU variant every time it is invoked.

We cover in the later chapters how you can view the real target assembly code, the result of the PTX to target translation.

# ERROR HANDLING

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

To avoid this type of repetitive programming, throughout the book we will use the following macro definition to making calls to the CUDA API:

```
#define CUDA_CALL(x) { const cudaError_t a = (x); if (a != cudaSuccess) { printf("\nCUDA Error: %s (err_num=%d) \n", cudaGetErrorString(a), a); cudaDeviceReset(); assert(0); } }
```

What this macro does is to allow you to specify x as some function call, for example,