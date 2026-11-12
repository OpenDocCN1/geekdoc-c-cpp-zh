

计算能力 7.x 设备允许单个线程块寻址共享内存的全部容量：Volta 上为 96 KB，Turing 上为 64 KB。依赖每块超过 48 KB 共享内存分配的内核是特定于架构的，因此它们必须使用动态共享内存（而非静态大小的数组），并通过 cudaFuncSetAttribute() 显式选择加入，如下所示。

```
// device code
__global__ void MyKernel(...)
{
    ...
}

// Host code
int maxbytes = 98304; // 96 KB
cudaFuncSetAttribute(MyKernel, cudaFuncAttributeMaxDynamicSharedMemorySize,
                     maxbytes);
MyKernel <<<gridDim, blockDim>>>(...);
```

否则，共享内存的行为与计算能力 5.x 设备相同（参见共享内存）。

## 附录 I. 驱动程序 API

本附录假设读者了解 CUDA 运行时中描述的概念。

驱动程序 API 实现在 **cuda** 动态库（**cuda.dll** 或 **cuda.so**）中，该库在安装设备驱动程序时会复制到系统上。其所有入口点均以 cu 开头。

这是一个基于句柄的命令式 API：大多数对象由不透明句柄引用，可将这些句柄传递给函数以操作对象。

驱动程序 API 中可用的对象在表 16 中汇总。

### 表 16 CUDA 驱动程序 API 中可用的对象

| 对象 | 句柄 | 描述 |
| :--- | :--- | :--- |
| 设备 | CUdevice | 支持 CUDA 的设备 |
| 上下文 | CUcontext | 大致相当于 CPU 进程 |
| 模块 | CUmodule | 大致相当于动态库 |
| 函数 | CUfunction | 内核 |
| 堆内存 | CUdeviceptr | 指向设备内存的指针 |
| CUDA 数组 | CUarray | 设备上一维或二维数据的不透明容器，可通过纹理或表面引用读取 |
| 纹理引用 | CUtexref | 描述如何解释纹理内存数据的对象 |
| 表面引用 | CUsurfref | 描述如何读取或写入 CUDA 数组的对象 |
| 流 | CUstream | 描述 CUDA 流的对象 |
| 事件 | CUevent | 描述 CUDA 事件的对象 |

在调用任何驱动程序 API 函数之前，必须使用 **cuInit()** 初始化驱动程序 API。随后必须创建一个 CUDA 上下文，将其附加到特定设备，并使其成为调用主机线程的当前上下文，如上下文中详细所述。

在 CUDA 上下文中，内核由主机代码显式加载为 PTX 或二进制对象，如模块中所述。因此，用 C++ 编写的内核必须单独编译为 PTX 或二进制对象。内核使用 API 入口点启动，如内核执行中所述。

任何希望在未来设备架构上运行的应用程序都必须加载 PTX，而非二进制代码。这是因为二进制代码是特定于架构的，因此与未来架构不兼容，而 PTX 代码会在加载时由设备驱动程序编译为二进制代码。

以下是使用驱动程序 API 编写的内核示例中的主机代码：

```
int main()
{
    int N = ...;
    size_t size = N * sizeof(float);

    // Allocate input vectors h_A and h_B in host memory
    float* h_A = (float*)malloc(size);
    float* h_B = (float*)malloc(size);

    // Initialize input vectors
    ...

    // Initialize
    cuInit(0);

    // Get number of devices supporting CUDA
    int deviceCount = 0;
    cuDeviceGetCount(&deviceCount);
    if (deviceCount == 0) {
        printf("There is no device supporting CUDA.\n");
        exit(0);
    }

    // Get handle for device 0
    CUdevice cuDevice;
    cuDeviceGet(&cuDevice, 0);

    // Create context
    CUcontext cuContext;
    cuCtxCreate(&cuContext, 0, cuDevice);

    // Create module from binary file
    CUmodule cuModule;
    cuModuleLoad(&cuModule, "VecAdd.ptx");

    // Allocate vectors in device memory
    CUdeviceptr d_A;
    cuMemAlloc(&d_A, size);
    CUdeviceptr d_B;
    cuMemAlloc(&d_B, size);
    CUdeviceptr d_C;
    cuMemAlloc(&d_C, size);

    // Copy vectors from host memory to device memory
    cuMemcpyHtoD(d_A, h_A, size);
    cuMemcpyHtoD(d_B, h_B, size);

    // Get function handle from module
    CUfunction vecAdd;
    cuModuleGetFunction(&vecAdd, cuModule, "VecAdd");

    // Invoke kernel
    int threadsPerBlock = 256;
    int blocksPerGrid =
        (N + threadsPerBlock - 1) / threadsPerBlock;
    void* args[] = { &d_A, &d_B, &d_C, &N };
    cuLaunchKernel(vecAdd,
                   blocksPerGrid, 1, 1, threadsPerBlock, 1, 1,
                   0, 0, args, 0);

    ...
}
```

完整代码可在 vectorAddDrv CUDA 示例中找到。

## I.1. 上下文

CUDA 上下文类似于 CPU 进程。在驱动程序 API 中执行的所有资源和操作都封装在 CUDA 上下文中，系统会在销毁上下文时自动清理这些资源。除了模块和纹理或表面引用等对象之外，每个上下文都有其自身独立的地址空间。因此，不同上下文中的 `CUdeviceptr` 值引用不同的内存位置。

主机线程同一时间只能有一个当前设备上下文。使用 `cuCtxCreate()` 创建上下文时，它会成为调用主机线程的当前上下文。在上下文中操作的 CUDA 函数（大多数不涉及设备枚举或上下文管理的函数）如果线程没有当前有效上下文，将返回 `CUDA_ERROR_INVALID_CONTEXT`。

每个主机线程都有一个当前上下文栈。`cuCtxCreate()` 将新上下文压入栈顶。可以调用 `cuCtxPopCurrent()` 将上下文从主机线程分离。此时上下文处于“浮动”状态，并可作为任何主机线程的当前上下文压入栈中。`cuCtxPopCurrent()` 还会恢复之前的当前上下文（如果有）。

每个上下文还维护一个引用计数。`cuCtxCreate()` 创建引用计数为 1 的上下文。`cuCtxAttach()` 增加引用计数，`cuCtxDetach()` 减少引用计数。当调用 `cuCtxDetach()`（或 `cuCtxDestroy()`）时，如果引用计数降至 0，则销毁上下文。

驱动程序 API 与运行时互操作，可以通过 `cuDevicePrimaryCtxRetain()` 从驱动程序 API 访问运行时管理的 `primary context`（参见初始化）。

引用计数有助于在同一上下文中运行的第三方代码之间实现互操作。例如，如果加载了三个库来使用同一上下文，则每个库在使用完上下文时都会调用 `cuCtxAttach()` 增加引用计数，并调用 `cuCtxDetach()` 减少引用计数。对于大多数库，预期应用程序会在加载或初始化库之前创建上下文；这样，应用程序可以使用自己的启发式方法创建上下文，而库只需在传递给它的上下文上操作。希望自行创建上下文（其 API 客户端可能或可能未创建自己的上下文，对此一无所知）的库，将使用 `cuCtxPushCurrent()` 和 `cuCtxPopCurrent()`，如图 21 所示。

### 图 21 库上下文管理

![](img/c13b0ff67eed8f2c7b32afa2a587a8d6_316_0.png)

## I.2. 模块

模块是由 nvcc 输出的可动态加载的设备代码和数据包，类似于 Windows 中的 DLL（参见使用 NVCC 进行编译）。所有符号（包括函数、全局变量以及纹理或表面引用）的名称均在模块作用域中维护，以便独立第三方编写的模块可以在同一 CUDA 上下文中互操作。

此代码示例加载模块并获取某个内核的句柄：

```
CUmodule cuModule;
cuModuleLoad(&cuModule, "mymodule.ptx");
cuFunction myKernel;
cuModuleGetFunction(&myKernel, cuModule, "MyKernel");
```

此代码示例从 PTX 代码编译并加载新模块，并解析编译错误：

```
#define BUFFER_SIZE 8192
CUmodule cuModule;
CUjit_option options[3];
void* values[3];
char error_log[BUFFER_SIZE];
char error_name[BUFFER_SIZE];
int err;
options[0] = CU_JIT_ERROR_LOG_BUFFER;
values[0] = (void*)error_log;
options[1] = CU_JIT_ERROR_LOG_BUFFER_SIZE_BYTES;
values[1] = (void*)BUFFER_SIZE;
options[2] = CU_JIT_TARGET_FROM_CUCONTEXT;
values[2] = 0;
err = cuModuleLoadDataEx(&cuModule, PTXCode, 3, options, values);
if (err == CUDA_SUCCESS)
   printf("Link error:\n%s\n", error_log);
```

