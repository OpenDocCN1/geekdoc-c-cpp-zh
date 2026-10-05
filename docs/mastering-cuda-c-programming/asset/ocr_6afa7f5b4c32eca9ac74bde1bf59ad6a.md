# Debugging CUDA Kernels

One of the most powerful features of CUDA-GDB is the ability to debug CUDA kernels as they execute on the GPU. You can set breakpoints inside your kernel code, and when execution reaches this point, you’ll gain control in CUDA-GDB to inspect the state of your application.

Here’s how you can set a breakpoint inside a CUDA kernel for a specific thread:

```
break my_kernel.cu:42@threadIdx.x==0 && blockIdx.x==0
```

This command sets a breakpoint at line 42 of my_kernel.cu for the first thread of the first block. Such fine-grained control is crucial for debugging race conditions and thread-specific bugs.