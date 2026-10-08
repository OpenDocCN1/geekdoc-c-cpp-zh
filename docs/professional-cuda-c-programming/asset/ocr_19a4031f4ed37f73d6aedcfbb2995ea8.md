# Memory Allocation and Deallocation

The CUDA programming model assumes a heterogeneous system that consists of a host and a device, with its own separate memory space. Kernel functions operate in the device memory space, and the CUDA runtime provides functions to allocate and deallocate device memory. You can allocate global memory on the host using the following function:

```
cudaError_t cudaMalloc(void **devPtr, size_t count);
```

This function allocates bytes of global memory on the device and returns the location of that memory in devPtr. The allocated memory is suitably aligned for any variable type, including integers, floating-point values, booleans, and so on. The cudaMalloc function returns cudaError on failure. The values contained in the allocated global memory are not cleared. It is your responsibility to either fill the allocated global memory with data transferred from the host, or initialize it with the following function:

```
cudaError_t cudaMemset(void *devPtr, int value, size_t count);
```

This function fills each of the count bytes starting at the device memory address devPtr with the value stored in the variable value.

Once an application is no longer using a piece of allocated global memory, it can be deallocated using:

```
cudaError_t cudaFree(void *devPtr);
```

This function frees the global memory pointed to by devPtr, which must have been previously allocated using a device allocation function (such as cudaMalloc). Otherwise, it returns an error cudaErrorInvalidDevicePointer. cudaFree also returns an error if the address has already been freed.

Device memory allocation and deallocation are expensive operations, so device memory should be reused whenever possible to minimize the impact on overall performance.

# Memory Transfer

Once global memory is allocated, you can transfer the data to the device from the host using the following function:

```
cudaError_t cudaMempy(void *dst, const void *src, size_t count,
enum cudaMemcpyKind kind);
```

This function copy bytes from the memory location src to the memory location dst. The variable kind specifies the direction of the copy and can have the following values:

```
cudaMemcpyHostToHost
cudaMemcpyHostToDevice
cudaMempyDeviceToHost
cudaMemcpyDeviceToDevice
```

If the pointers dst and src do not match the direction specified by kind, the behavior of cudaMempy is undefined. This function exhibits synchronous behavior in most cases.

An example that uses cudaMempy is shown in Listing 4-2. This example transfers data back and forth between the host and the device. Global memory is allocated using cudaMalloc and data is transferred to the device using the direction specified as