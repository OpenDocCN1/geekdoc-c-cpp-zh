Runtime initialization functions are used to either initialize or clean up OpenACC state. A subset of the runtime initialization functions is described in Table 8-9. If acc_init is not explicitly called by an OpenACC application, runtime initialization is automatically performed as part of the first OpenACC operation of an application.

# TABLE 8-9: Runtime Initialization Functions in the OpenACC Runtime API

| FUNCTION DECLARATION | DESCRIPTION |
|---|---|
| void acc_init(acc_device_t) | Initialize the OpenACC runtime on a device of the provided type. |
| void acc_shutdown(acc_device_t) | Disconnect the OpenACC runtime from the currently active device with the specified type. |

Memory management functions are used to manage the allocation of accelerator memory and transfer of data between host and accelerator. In, many cases they duplicate functionality of the OpenACC data directives and clauses. A subset of the memory management functions is described in Table 8-10.

# TABLE 8-10: Memory Management Functions in the OpenACC Runtime API

| FUNCTION DECLARATION | DESCRIPTION |
|---|---|
| void * acc_malloc(size_t) | Allocates the specified number of bytes on the accelerator, returning the address of the allocated memory |
| void acc_free(void *) | Frees memory starting at the specified address |
| void acc_copyin, acc_present_or_copyin, acc_create, acc_present_or_create, acc_copyout, acc_delete | Each of these functions takes a void* as its first argument and size_t as its second argument. They implement the same operation with an identical name, performing operation using the number of bytes specified as the second argument starting at the host address specified by the first argument |\| int acc_is_present(void*, size_t) | Checks if the memory starting at the provided address and with the specified length is copied to the accelerator

# Combining OpenACC and the CUDA Libraries

While CUDA and OpenACC are separate programming models, they can be used in the same application. Doing so requires changes to how the application is compiled. The deviceptr class must be used to share data between CUDA and OpenACC. This section will demonstrate a single application that uses CUDA libraries and OpenACC together in a single source file. The example application can be downloaded from Wrox.com in cuda-openacc.cu.