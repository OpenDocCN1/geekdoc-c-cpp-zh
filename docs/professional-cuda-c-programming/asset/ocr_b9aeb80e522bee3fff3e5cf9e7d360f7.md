Kernels can only read from constant memory. Constant memory must therefore be initialized by the host using:

```
cudaError_t cudaMemcpyToSymbol(const void* symbol, const void* src,
               size_t count);
```

This function count bytes from the memory pointed by src to the memory pointed by symbol, which is a variable that resides on the device in global or constant memory. This function is synchronous in most cases.

Constant memory performs best when all threads in a warp read the same memory address. For example, a coefficient for a mathematical formula is a good use for constant memory because all threads in a warp will use the same coefficient to conduct the same calculation on different data. If each thread in a warp reads from a different address, and only once, then constant memory is not the best choice because a single read from constant memory broadcasts to all threads in a warp.

# ## Texture Memory

Texture memory resides in device memory and is cached in a Per-SM, read-only cache. Texture memory is a type of global memory that is accessed through a dedicated read-only cache. The read-only cache includes support for hardware filtering, performing floating-point interpolation as part of the process. Texture memory is optimized for 2D spatial locality, so threads in a warp use texture memory to access 2D data will achieve the best performance. For applications, this is ideal and provides a performance advantage over the cache and the filtering hardware. However, for other applications texture memory can be slower than global memory.

# ## Global Memory

Global memory is the largest, highest-latency, and most commonly used memory on a GPU. The global name refers to its state and lifetime. Its state can be accessed from the device from any SM throughout the lifetime of the application.

A variable in global memory can either be declared statically or dynamically. You can declare a global variable statically in device code using the following qualifier:

```
__device__
```

In the “CUDA Programming Model” of Chapter 2, you learned how to dynamically allocate global memory. Global memory is allocated by the host using cudaMalloc and freed by the host using cudaFree. Pointers to global memory are passed to kernel functions as parameters. Global memory allocations exist for the lifetime of an application and are accessible to all of kernels. You must take care when accessing global memory from multiple threads. Because thread execution cannot be synchronized across thread blocks, there is a potential hazard of multiple threads in thread blocks concurrently modifying the same location in global memory, which will lead to an undefined program behavior.

Global memory resides in device memory and is accessible via naturally 32-byte, 64-byte, or 128-byte memory transactions. These memory transactions must be aligned; for the first address