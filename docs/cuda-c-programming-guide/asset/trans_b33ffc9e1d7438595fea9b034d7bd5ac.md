

例如，源文件 test.cu 中的以下程序

```
#include <assert.h>

__global__ void testAssert(void)
{
    int is_one = 1;
    int should_be_one = 0;
    // This will have no effect
    assert(is_one);
    // This will halt kernel execution
    assert(should_be_one);
}

int main(int argc, char* argv[])
{
    testAssert<<<1,1>>>();
    cudaDeviceSynchronize();
    return 0;
}
```

将输出：

```
test.cu:19: void testAssert(): block: [0,0,0], thread: [0,0,0] Assertion
'should_be_one' failed.
```

断言用于调试目的。它们可能会影响性能，因此建议在生产代码中禁用它们。可以在编译时通过在包含 `assert.h` 之前定义 **NDEBUG** 预处理器宏来禁用它们。请注意，**表达式** 不应是带有副作用的表达式（例如 `++i > 0`），否则禁用断言将影响代码的功能。

## B.20. 格式化输出

格式化输出仅受计算能力 2.x 及更高版本的设备支持。

```
int printf(const char *format, arg, ...);
```

从内核向主机端输出流打印格式化输出。

内核中的 **printf()** 函数的行为与标准 C 库 printf() 函数类似，有关 **printf()** 行为的完整描述，请参阅主机系统的手册页。本质上，作为 `format` 传递的字符串将输出到主机上的流中，并在遇到格式说明符时从参数列表中进行替换。支持的格式说明符如下所示。

**printf()** 命令的执行方式与其他设备端函数相同：按线程，并在调用线程的上下文中执行。对于多线程内核，这意味着对 **printf()** 的直接调用将由每个线程执行，并使用该线程的指定数据。然后，输出字符串的多个版本将出现在主机流中，每个遇到 **printf()** 的线程出现一次。

如果只需要单个输出字符串，则由程序员将输出限制为单个线程（有关示例说明，请参见 Examples）。

与 C 标准 `printf()` 不同，后者返回打印的字符数，CUDA 的 `printf()` 返回解析的参数数量。如果格式字符串后面没有参数，则返回 0。如果格式字符串为 NULL，则返回 -1。如果发生内部错误，则返回 -2。

### B.20.1. 格式说明符

与标准 `printf()` 类似，格式说明符的形式为：`% [flags] [width] [.precision] [size] type`

支持以下字段（有关所有行为的完整描述，请参阅广泛可用的文档）：

- 标志：'#' ' ' '0' '+' '-' ''
- 宽度：'*' '0'-'9'
- 精度：'0'-'9'
- 大小：'h' 'l' 'll'
- 类型："%diousXxEeFgGaAs"

请注意，CUDA 的 `printf()` 将接受标志、宽度、精度、大小和类型的任何组合，无论它们整体是否构成有效的格式说明符。换句话说，"%hd" 将被接受，并且 printf 将在参数列表的相应位置期望一个双精度变量。

### B.20.2. 局限性

`printf()` 输出的最终格式化在主机系统上进行。这意味着格式字符串必须由主机系统的编译器和 C 库理解。已尽一切努力确保 CUDA printf 函数支持的格式说明符构成最常见主机编译器的通用子集，但确切行为将取决于主机操作系统。

如格式说明符中所述，`printf()` 将接受有效标志和类型的 *全部* 组合。这是因为它无法确定在最终输出格式化的主机系统上什么有效、什么无效。其影响是，如果程序发出包含无效组合的格式字符串，输出可能是未定义的。

`printf()` 命令除了格式字符串外最多可接受 32 个参数。超过此数量的其他参数将被忽略，格式说明符将原样输出。

由于 64 位 Windows 平台上 `long` 类型的大小不同（64 位 Windows 平台上为四个字节，其他 64 位平台上为八个字节），因此在非 Windows 64 位机器上编译但在 win64 机器上运行的内核，对于包含 "%ld" 的所有格式字符串都会看到损坏的输出。建议编译平台与执行平台匹配以确保安全。

`printf()` 的输出缓冲区在内核启动前设置为固定大小（请参阅关联的主机端 API）。它是循环的，如果在内核执行期间产生的输出超过缓冲区可容纳的大小，则较旧的输出会被覆盖。仅在执行以下操作之一时才会刷新：

- 通过 `<<<>>>` 或 `cuLaunchKernel()` 启动内核（在启动开始时，以及如果 CUDA_LAUNCH_BLOCKING 环境变量设置为 1，则在启动结束时也会刷新），
- 通过 `cudaDeviceSynchronize()`、`cuCtxSynchronize()`、`cudaStreamSynchronize()`、`cuStreamSynchronize()`、`cudaEventSynchronize()` 或 `cuEventSynchronize()` 进行同步，
- 通过任何阻塞版本的 `cudaMemcpy*()` 或 `cuMemcpy*()` 进行内存拷贝，
- 通过 `cuModuleLoad()` 或 `cuModuleUnload()` 进行模块加载/卸载，
- 通过 `cudaDeviceReset()` 或 `cuCtxDestroy()` 进行上下文销毁。
- 在执行由 `cudaStreamAddCallback` 或 `cuStreamAddCallback` 添加的流回调之前。

请注意，程序退出时缓冲区不会自动刷新。用户必须显式调用 `cudaDeviceReset()` 或 `cuCtxDestroy()`，如下面的示例所示。

在内部，`printf()` 使用共享数据结构，因此调用 `printf()` 可能会更改线程的执行顺序。特别是，调用 `printf()` 的线程可能比不调用 `printf()` 的线程走更长的执行路径，而该路径长度取决于 `printf()` 的参数。但是，请注意，CUDA 除了在显式 `__syncthreads()` 屏障处外，不保证线程执行顺序，因此无法判断执行顺序是被 `printf()` 修改还是由硬件中的其他调度行为修改。

### B.20.3. 关联的主机端 API

以下 API 函数用于获取和设置用于将 `printf()` 参数和内部元数据传输到主机的缓冲区大小（默认值为 1 兆字节）：

- `cudaDeviceGetLimit(size_t* size, cudaLimitPrintfFifoSize)`
- `cudaDeviceSetLimit(cudaLimitPrintfFifoSize, size_t size)`

### B.20.4. 示例

以下代码示例：

```
#include <stdio.h>

__global__ void helloCUDA(float f)
{
    printf("Hello thread %d, f=%f\n", threadIdx.x, f);
}

int main()
{
    helloCUDA<<<1, 5>>>(1.2345f);
    cudaDeviceSynchronize();
    return 0;
}
```

将输出：

```
Hello thread 2, f=1.2345
Hello thread 1, f=1.2345
Hello thread 4, f=1.2345
Hello thread 0, f=1.2345
Hello thread 3, f=1.2345
```

请注意，每个线程都会遇到 **printf()** 命令，因此输出行数与网格中启动的线程数相同。如预期，全局值（即 **float f**）在所有线程之间是共享的，而局部值（即 **threadIdx.x**）则因线程而异。

以下代码示例：

```
#include <stdio.h>

__global__ void helloCUDA(float f)
{
    if (threadIdx.x == 0)
        printf("Hello thread %d, f=%f\n", threadIdx.x, f);
}

int main()
{
    helloCUDA<<<1, 5>>>(1.2345f);
    cudaDeviceSynchronize();
    return 0;
}
```

将输出：

```
Hello thread 0, f=1.2345
```

显然，**if()** 语句限制了哪些线程会调用 **printf**，因此只能看到一行输出。

## B.21. 动态全局内存分配和操作

动态全局内存分配和操作仅受计算能力 2.x 及更高版本的设备支持。

```
__host__ __device__ void* malloc(size_t size);
__device__ void* __nv_aligned_device_malloc(size_t size, size_t align);
__host__ __device__ void free(void* ptr);
```

从全局内存中的固定大小堆动态分配和释放内存。

```
__host__ __device__ void* memcpy(void* dest, const void* src, size_t size);
```

将从 src 指向的内存位置到 dest 指向的内存位置的 size 字节进行拷贝。

```
__host__ __device__ void* memset(void* ptr, int value, size_t size);
```

将 ptr 指向的内存块的 size 字节设置为 value（解释为无符号字符）。

CUDA 内核中的 malloc() 函数从设备堆分配至少 size 个字节，并返回指向分配内存的指针，如果内存不足以满足请求，则返回 NULL。返回的指针保证按 16 字节边界对齐。

CUDA 内核中的 __nv_aligned_device_malloc() 函数从设备堆分配至少 size 个字节，并返回指向分配内存的指针，如果内存不足以满足请求的大小或对齐，则返回 NULL。分配内存的地址将是 align 的倍数。align 必须是非零的 2 的幂。

CUDA 内核中的 free() 函数释放 ptr 指向的内存，该内存必须之前由 malloc() 或 __nv_aligned_device_malloc() 返回。如果 ptr 为 NULL，则忽略对 free() 的调用。对同一 ptr 重复调用 free() 具有未定义行为。

通过特定 CUDA 线程使用 malloc() 或 __nv_aligned_device_malloc() 分配的内存将保持分配状态，直到 CUDA 上下文生命周期结束，或通过调用 free() 显式释放为止。即使来自后续内核启动，任何其他 CUDA 线程也可以使用它。任何 CUDA 线程都可以释放由另一个线程分配的内存，但应注意确保同一指针不会被释放多次。

### B.21.1. 堆内存分配

设备内存堆具有固定大小，必须在使用 malloc()、__nv_aligned_device_malloc() 或 free() 的任何程序加载到

