Shared memory has two purposes: first, to act as a block of local, high-speed, per-thread memory, and second, to facilitate interblock communication via global memory. Only in the latter case does shared memory need to be declared as volatile. Thus, the `__shared__` directive does not implicitly declare the parameter as volatile since the programmer may not always wish to enforce reads and writes when the compiler is able to use a register to optimize out some of these. It is perfectly valid practice not to use a `syncthreads` call when the threads are cooperating within a warp, but you must realize that the shared memory has no longer been made coherent to every thread in the warp.

When you have interblock communication via global memory, the view each block sees of global memory is again not consistent between blocks without explicit synchronization. We have the same issue as with shared memory, in that the compiler may optimize away intermediate global writes and write only the last one out to memory. This can be overcome by using the volatile keyword for access within a block. However, CUDA does not specify block execution order, so this does not deal with interblock-based dependencies. These are handled in two ways. First, and the most common, is the termination and invocation of another kernel. Implicit in this is a completion of all pending global memory transactions and a flush of all caches. The second method is used where you wish to perform some operation within the same kernel invocation. In this instance you need to call the `__threadfence` primitive, which simply causes, and waits for, any writes from the calling thread to be visible to all affected threads. For shared memory, this equates to the threads within the same block, as only these threads can see the shared memory allocated to a given block. For global memory, this equates to all threads within the device.

# Compute level-dependent functions

The compute 2.x hardware supports many additional functions not present in the earlier hardware. The same is true of compute 1.3 devices. If you search through the CUDA programming guide it will list various functions as available only on certain compute levels. For example, `__syncthreads_count` is a compute 2.0 function.

Unfortunately, the default CUDA projects (e.g., the New Project wizard in Visual Studio) use CUDA 1.0 support. Thus, when you have a Fermi card installed (a compute 2.x device) and compile the project using a compute 2.0 directive, the compiler rather unhelpfully states the following:

```
Error 1 error: identifier "__syncthreads_count" is undefined j:\CUDA\Chapter-09-OddEvenSort\OddEvenSort kernel.cu 145 OddEven
```

It doesn't say this function is supported only under the compute 2.0 architecture. This would be at least helpful in helping you identify the problem. It just says it's undefined, which makes most programmers assume they have missed an include statement or have done something wrong. Thus, they are sent off in the wrong direction searching for a solution.

The issue is simply resolved by setting the GPU architecture level by changing the properties of the GPU option of the CUDA runtime, as shown in Figure 12.1. This results in the following command line option being added to the compiler invocation command:

```
-gencode=arch=compute_20,code="sm_20,compute_20"*
```

Note that you can set, by default, up to three architectures in the standard project created by Visual Studio for CUDA projects. Code can be written for various compute levels using the compiler preprocessor. In fact, this is what is being used to make higher compute level functions visible.