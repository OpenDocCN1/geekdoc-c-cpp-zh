You cannot use the reference operator & on device variable from the host, because it is simply a symbol representing the physical location on the GPU. However, you can acquire the address of a global variable by explicitly making a call using the following CUDA API:

```
cudaError_t cudaSymbolAddress(void** devPtr, const void* symbol);
```

This function fetches the physical address of the global memory associated with the provided device symbol. After acquiring the address of the variable devData, you can use the cudaMemCopy function as:

```
float *dptr = NULL;
cudaSymbolAddress(void**)&dptr,devData);
cudaMemcpy(dptr, &value, sizeof(float), cudaMemcpyHostToDevice);
```

There is a single exception to directly referencing GPU memory from the host: pinned memory. Both host code and device code can access pinned memory by simply dereferencing a pointer. You will learn about pinned memory in the next section.

VARIABLES IN FILE SCOPE: VISIBLE VERSUS ACCESSIBLE
CUDA programming, you work in two worlds: the host and the device. In general, device kernels cannot access host variables and functions cannot access variables, even though these variables are declared in the same file scope.
The runtime API can access both host and device variables, but it is up to you to provide the correct arguments to the functions so they operate properly on correctly. Because the runtime API makes assumptions about the memory space of certain parameters, passing a host variable where it expects a device variable or vice versa will result in undefined behavior (likely crashing your application).

# MEMORY MANAGEMENT

Memory management in CUDA programming is similar to C programming, with the added programmer responsibility of explicitly managing data movement between the host and device. While NVIDIA is methodically moving closer to unifying the host and device memory space with each CUDA release, for most applications manual data movement is still a requirement. The latest advancements in this area will be covered in this chapter titled "Unified Memory." For now, we will focus on how you can explicitly manage memory and data movement using CUDA functions to:

+   - Allocate and deallocate device memory
- Transfer data between the host and device

In order to achieve maximum performance, CUDA provides functions that prepare device memory on the host and explicitly transfer data to and from the device.