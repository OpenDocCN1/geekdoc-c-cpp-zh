

给定内核的最佳启动边界通常会因主要架构版本而异。示例代码展示了如何在设备代码中使用在应用程序兼容性中引入的 `__CUDA_ARCH__` 宏来处理此问题。

```cpp
#define THREADS_PER_BLOCK 256
#if CUDA_ARCH >= 200
#define MY_KERNEL_MAX_THREADS (2 * THREADS_PER_BLOCK)
#define MY_KERNEL_MIN_BLOCKS 3
#else
#define MY_KERNEL_MAX_THREADS THREADS_PER_BLOCK
#define MY_KERNEL_MIN_BLOCKS 2
#endif

// Device code
__global__ void
__launch_bounds__(MY_KERNEL_MAX_THREADS, MY_KERNEL_MIN_BLOCKS)
MyKernel(...)
{
    ...
}
```

在常见情况下，当 `MyKernel` 使用每块最大线程数（即 `__launch_bounds__()` 的第一个参数）被调用时，很诱人在执行配置中使用 `MY_KERNEL_MAX_THREADS` 作为每块线程数：

```cpp
// Host code
MyKernel<<<blocksPerGrid, MY_KERNEL_MAX_THREADS>>>(...);
```

然而，这行不通，因为正如在应用程序兼容性中所述，`__CUDA_ARCH__` 在主机代码中未定义，因此即使 `__CUDA_ARCH__` 大于或等于 200，`MyKernel` 也将以每块 256 个线程启动。相反，每块线程数应通过以下方式确定：

- 要么在编译时使用不依赖于 `__CUDA_ARCH__` 的宏，例如

```cpp
// Host code
MyKernel<<<blocksPerGrid, THREADS_PER_BLOCK>>>(...);
```

- 要么在运行时根据计算能力确定

```cpp
// Host code
cudaGetDeviceProperties(&deviceProp, device);
int threadsPerBlock =
    (deviceProp.major >= 2 ? THREADS_PER_BLOCK : THREADS_PER_BLOCK);
MyKernel<<<blocksPerGrid, threadsPerBlock>>>(...);
```

寄存器用量由 **--ptxas options=-v** 编译器选项报告。常驻块数量可根据 CUDA 分析器报告的占用率推导（有关占用率的定义，请参见设备内存访问）。

还可以使用 **maxrregcount** 编译器选项控制文件中所有 `__global__` 函数的寄存器用量。对于带有启动边界的函数，**maxrregcount** 的值将被忽略。

## B.24. #pragma unroll

默认情况下，编译器会展开已知行程计数的小循环。然而，`#pragma unroll` 指令可用于控制任何给定循环的展开。它必须紧跟在循环之前，且仅适用于该循环。其后可选地跟一个积分常量表达式（ICE）。如果没有 ICE，且循环行程计数为常量，则循环将被完全展开。如果 ICE 的值为 1，编译器将不展开循环。如果 ICE 的值为非正整数或大于 `int` 数据类型可表示的最大值的整数，则该 pragma 将被忽略。

### 示例：

```cpp
struct S1 { static const int value = 4; };
template <int X, typename T2>
__device__ void foo(int *p1, int *p2) {
// no argument specified, loop will be completely unrolled
#pragma unroll
for (int i = 0; i < 12; ++i)
p1[i] += p2[i]*2;

// unroll value = 8
#pragma unroll 8
for (int i = 0; i < 12; ++i)
p1[i] += p2[i]*4;

// unroll value = 1, loop unrolling disabled
#pragma unroll 1
for (int i = 0; i < 12; ++i)
p1[i] += p2[i]*8;

// unroll value = 4
#pragma unroll (T2::value)
for (int i = 0; i < 12; ++i)
p1[i] += p2[i]*16;
}

__global__ void bar(int *p1, int *p2) {
Foo<7, SI_T<x>(p1, p2);
}
```

9 有关积分常量表达式的定义，请参见 C++ 标准。

## B.25. SIMD 视频指令

PTX ISA 3.0 版包含 SIMD（单指令流、多数据流）视频指令，这些指令用于对 16 位值的成对和 8 位值的四元组进行操作。这些指令可用于计算能力为 3.0 的设备。

SIMD 视频指令如下：

- vadd2, vadd4
- vsub2, vsub4
- vavrg2, vavrg4
- vabsdiff2, vabsdiff4
- vmin2, vmin4
- vmax2, vmax4
- vset2, vset4

诸如 SIMD 视频指令之类的 PTX 指令，可以通过汇编器 asm() 语句包含在 CUDA 程序中。

asm() 语句的基本语法如下：

```cpp
asm("template-string" : "constraint"(output) : "constraint"(input));
```

使用 vabsdiff4 PTX 指令的示例如下：

```cpp
asm("vabsdiff4.u32.u32.u32.add" %0, %1, %2, %3:: "=r"(result) : "r" (A), "r" (B), "r" (C));
```

这使用 vabsdiff4 指令来计算整数四字节 SIMD 绝对差之和。以 SIMD 方式，对无符号整数 A 和 B 的每个字节计算绝对差值。可选的累加操作（.add）用于对这些差值求和。

有关在代码中使用汇编语句的详细信息，请参阅文档“CUDA 中使用内联 PTX 汇编”。有关您所使用的 PTX 版本的 PTX 指令详细信息，请参阅 PTX ISA 文档（“Parallel Thread Execution ISA Version 3.0” 为例）。

## 附录 C. 协作组

### C.1. 简介

协作组是 CUDA 9 引入的 CUDA 编程模型扩展，用于组织通信线程组。协作组允许开发者表达线程通信的粒度，帮助他们表达更丰富、更高效的并行分解。

从历史上看，CUDA 编程模型为同步协作线程提供了单一而简单的构造：即通过 `__syncthreads()` 内置函数实现的跨线程块所有线程的屏障。然而，程序员希望在其他粒度上定义和同步线程组，以便以“集体”组范围函数接口的形式实现更高的性能、设计灵活性和软件复用性。为了表达更广泛的并行交互模式，许多面向性能的程序员不得不编写自己的临时且不安全的原语，用于在单个 warp 内或在单个 GPU 上运行的一组线程块之间同步线程。尽管所取得的性能改进通常很有价值，但这导致了一个不断增长的脆弱代码集合，这些代码在编写、调优和维护方面成本高昂，并且随时间和 GPU 代际而变化。协作组通过提供安全且面向未来的机制来解决此问题，以实现高性能代码。

协作组编程模型扩展描述了 CUDA 线程块内部和跨线程块的同步模式。它既提供了应用程序定义自身线程组的手段，也提供了同步它们的接口。它还提供了强制执行某些限制的新启动 API，因此可以保证同步生效。这些原语在 CUDA 中实现了新的协作并行模式，包括生产者-消费者并行、机会性并行以及整个 Grid 范围的全局同步。

将组作为一等程序对象执行，改善了软件组合性，因为集体函数可以接收表示参与线程组的显式对象。该对象还使程序员意图明确化，从而消除导致脆弱代码、对编译器优化施加不希望的限制以及与新一代 GPU 兼容性较差的不可靠架构假设。

协作组编程模型包含以下元素：

- 用于表示协作线程组的数据类型；
- 用于获取由 CUDA 启动 API 定义的内置组（例如线程块）的操作；
- 用于将现有组划分为新组的操作；
- 用于同步给定组的屏障操作；
- 以及用于检查组属性和组特定集体操作的操作。

## C.2. 块内组

本节介绍了在线程块内创建可同步和协作的线程组的功能。请注意，使用协作组跨线程块或设备进行同步需要一些额外的注意事项，如后文所述。

协作组需要 CUDA 9.0 或更高版本。要使用协作组，请包含头文件：

```cpp
#include <cooperative_groups.h>
```

并使用协作组命名空间：

```cpp
using namespace cooperative_groups;
```

然后，包含任何块内协作组功能的代码可以使用 nvcc 按正常方式编译。

### C.2.1. 线程组和线程块

任何 CUDA 程序员都已经熟悉某个线程组：线程块。协作组扩展引入了一种新数据类型 `thread_block`，以在内核中显式表示此概念。该组可以按如下方式初始化：

```cpp
thread_block g = this_thread_block();
```

`thread_block` 数据类型派生自更通用的 `thread_group` 数据类型，后者可用于表示更广泛的组类。`thread_group` 提供以下功能：

```cpp
void sync(); // Synchronize the threads in the group
unsigned size(); // Total number of threads in the group
unsigned thread_rank(); // Rank of the calling thread within [0, size)
bool is_valid(); // Whether the group violated any API constraints
```

而 `thread_block` 提供以下特定于块的其他功能：

```cpp
dim3 group_index(); // 3-dimensional block index within the grid
dim3 thread_index(); // 3-dimensional thread index within the block
```

