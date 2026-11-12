

#define BUFFER_SIZE 8192
CUmodule cuModule;
CUjit_option options[6];
void* values[6];
float walltime;
char error_log[BUFFER_SIZE], info_log[BUFFER_SIZE];
char* PTXCode = "some PTX code";
char* PTXCode1 = "some other PTX code";
CUjit_state linkState;
int err;
void* cubin;
size_t cubinSize;
options[0] = CU_JIT_WALL_TIME;
values[0] = (void*)&walltime;
options[1] = CU_JIT_INFO_LOG_BUFFER;
values[1] = (void*)info_log;
options[2] = CU_JIT_INFO_LOG_BUFFER_SIZE_BYTES;
values[2] = (void*)BUFFER_SIZE;
options[3] = CU_JIT_ERROR_LOG_BUFFER;
values[3] = (void*)error_log;
options[4] = CU_JIT_ERROR_LOG_BUFFER_SIZE_BYTES;
values[4] = (void*)BUFFER_SIZE;
options[5] = CU_JIT_LOG_VERBOSE;
values[5] = (void*)1;
cuLinkCreate(6, options, values, &linkState);
err = cuLinkAddData(linkState, CU_JIT_INPUT_PTX,
                   PTXCode, CUjit_option(PTXCode) + strlen(PTXCode) + 1, 0, 0, 0, 0);
if (err != CUDA_SUCCESS) {
    printf("Link error:\n%s\n", error_log);
    err = cuLinkAddData(linkState, CU_JIT_INPUT_PTX,
                        PTXCode1, CUjit_option(PTXCode1) + strlen(PTXCode1) + 1, 0, 0, 0, 0);
    if (err != CUDA_SUCCESS) {
        printf("Link error:\n%s\n", error_log);
        cuLinkComplete(linkState, &cubin, &cubinSize);
        printf("\nLinkState in %fms, cubin size:%zu\n", walltime, info_log);
        printf("\nLinking cubin in %fms, Linker output:\n%s\n", walltime, info_log);
        cuModuleLoadData(cuModule, cubin);
        cuLinkDestroy(linkState);
    }
}

Full code can be found in the `ptxjit` CUDA sample.

## 1.3. Kernel Execution

cuLaunchKernel() launches a kernel with a given execution configuration.

Parameters are passed either as an array of pointers (next to last parameter of cuLaunchKernel()) where the nth pointer corresponds to the nth parameter and points to a region of memory from which the parameter is copied, or as one of the extra options (last parameter of cuLaunchKernel()).

When parameters are passed as an extra option (the CU_LAUNCH_PARAM_BUFFER_POINTER option), they are passed as a pointer to a single buffer where parameters are assumed to be properly offset with respect to each other by matching the alignment requirement for each parameter type in device code.

Alignment requirements in device code for the built-in vector types are listed in Table 4. For all other basic types, the alignment requirement in device code matches the alignment requirement in host code and can therefore be obtained using __alignof().

The only exception is when the host compiler aligns double and long long (and long on a 64-bit system) on a one-word boundary instead of a two-word boundary (for example, using gcc's compilation flag -mno-align-double) since in device code these types are always aligned on a two-word boundary.

CUdeviceptr is an integer, but represents a pointer, so its alignment requirement is __alignof(void*).

The following code sample uses a macro (ALIGN_UP()) to adjust the offset of each parameter to meet its alignment requirement and another macro (ADD_TO_PARAM_BUFFER()) to add each parameter to the parameter buffer passed to the CU_LAUNCH_PARAM_BUFFER_POINTER option.

```
#define ALIGN_UP(offset, alignment) \
    (offset) = ((offset) + (alignment) - 1) & ~((alignment) - 1)
char paramBuffer[1024];
size_t paramBufferSize = 0;
#define ADD_TO_PARAM_BUFFER(value, alignment) \
    do { \
        paramBufferSize = ALIGN_UP(paramBufferSize, alignment); \
        memcpy(paramBuffer + paramBufferSize, \
               &(value), sizeof(value)); \
        paramBufferSize += sizeof(value); \
    } while (0)
int i;
ADD_TO_PARAM_BUFFER(i, __alignof(i));
float4 f4;
ADD_TO_PARAM_BUFFER(f4, 16); // float4's alignment is 16
char c;
ADD_TO_PARAM_BUFFER(c, __alignof(c));
float f;
ADD_TO_PARAM_BUFFER(f, __alignof(f));
CUdeviceptr devPtr;
ADD_TO_PARAM_BUFFER(devPtr, __alignof(devPtr));
float2 f2;
ADD_TO_PARAM_BUFFER(f2, 8); // float2's alignment is 8
void* extra[] = {
    CU_LAUNCH_PARAM_BUFFER_POINTER, paramBuffer,
    CU_LAUNCH_PARAM_BUFFER_SIZE, &paramBufferSize,
    CU_LAUNCH_PARAM_END
};
cuLaunchKernel(cuFunction,
               blockWidth, blockHeight, blockDepth,
               gridWidth, gridHeight, gridDepth,
               0, 0, 0, extra);
```

The alignment requirement of a structure is equal to the maximum of the alignment requirements of its fields. The alignment requirement of a structure that contains built-in vector types, CUdeviceptr, or non-aligned double and long long might therefore differ between device code and host code. Such a structure might also be padded differently. The following structure, for example, is not padded at all in host code, but it is padded in device code with 12 bytes after field `f` since the alignment requirement for field `f4` is 16.

```
typedef struct {
    float f;
    float f4[4];
} myStruct;
```

## 1.4. Interoperability between Runtime and Driver APIs

An application can mix runtime API code with driver API code.

If a context is created and made current via the driver API, subsequent runtime calls will pick up this context instead of creating a new one.

If the runtime is initialized (implicitly as mentioned in CUDA Runtime), `cuCtxGetCurrent()` can be used to retrieve the context created during initialization. This context can be used by subsequent driver API calls.

The implicitly created context from the runtime is called the *primary context* (see Initialization). It can be managed from the driver API with the Primary Context Management functions.

Device memory can be allocated and freed using either API. `CUdeviceptr` can be cast to regular pointers and vice-versa:

```
CUdeviceptr devPtr;
float* d_data;
// Allocation using driver API
cuMemAlloc(&devPtr, size);
d_data = (float*)devPtr;
// Allocation using runtime API
cudaMalloc(&d_data, size);
devPtr = (CUdeviceptr)d_data;
```

In particular, this means that applications written using the driver API can invoke libraries written using the runtime API (such as cuFFT, cuBLAS, ...).

All functions from the device and version management sections of the reference manual can be used interchangeably.

## Appendix J. CUDA ENVIRONMENT VARIABLES

Environment variables related to the Multi-Process Service are documented in the Multi-Process Service section of the GPU Deployment and Management guide.

### Table 17 CUDA Environment Variables

| Category | Variable | Values | Description |
| :--- | :--- | :--- | :--- |
| Device Enumeration and Properties | CUDA_VISIBLE_DEVICES | A comma-separated sequence of GPU identifiers | GPU identifiers are given as integer indices or as UUID strings. GPU UUID strings should follow the same format as given by nvidia-smi, such as GPU-89329737-d72c-4110-c12f-200dbae61676. However, for compatibility with older CUDA forms, candidates are allowed; simply specify enough digits from the beginning of the GPU UUID to uniquely identify that GPU in the target system. For example, CUDA_VISIBLE_DEVICES=GPU-89329737 may be a valid way to refer to the above GPU UUID, assuming no other GPU in the system shares this prefix. Only the devices whose index is present in the sequence are visible to CUDA applications and they are enumerated in the order of the sequence. If one of the indexes is invalid, only the devices whose index precedes the invalid index are visible to CUDA applications. For example, setting CUDA_VISIBLE_DEVICES to 2,1 causes device 0 to be invisible and device 2 to be enumerated before device 1. Setting CUDA_VISIBLE_DEVICES to 0,2,1,1 causes devices 0 and 2 to be visible and device 1 to be invisible. |
| | CUDA_MANAGED_FORCE_DEVICE_ALLOC | 0 or 1 (default is 0) | Forces the driver to place all managed allocations in device memory. |
| | CUDA_DEVICE_ORDER | FASTEST_FIRST, PCI_BUS_ID, ... | FASTEST_FIRST causes CUDA to guess which device is fastest using a simple |

