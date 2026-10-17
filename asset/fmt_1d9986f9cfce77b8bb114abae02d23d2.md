
## 表 5.12 gmem 性能分析器数值（续）

| 全局内存冗余存储 (%) | 此值显示了在执行全局内存存储事务时访问的冗余数据百分比。理想情况下，当内核请求的全局内存吞吐量等于 L2 缓存吞吐量时，将实现 0% 的冗余存储，即内核在存储操作中请求的字节数等于硬件在内核执行期间为服务该内核而实际访问的字节数。如果此统计值较高，则意味着存储的访问模式没有合并（coalesced），并且在内核执行期间访问了许多额外字节。其计算公式为 100 * (100 - 内核请求的全局内存吞吐量/L2 写吞吐量) |
| 峰值全局内存吞吐量 (GB/s) | 这是当前 CUDA 设备上可以达到的内存内存吞吐量或带宽。这是一个设备属性，内核实现的内存吞吐量应尽可能接近此峰值。 |
| 全局内存重放 (%) | 由全局内存访问导致的重放指令百分比。其计算公式为 100 * (L1 加载缺失)/发射指令数。 |

### 总结

CUDA 为程序员提供了各种硬件空间。鉴于各种 CUDA 内存类型之间带宽存在三个数量级的差异（从 8 TB/s 的寄存器带宽到受 PCIe 限制的映射内存的 8 GB/s），CUDA 程序员充分利用这些可用内存空间至关重要。未能这样做可能会导致性能低下。

CUDA 提供了许多优秀的测量和派生分析信息，以追踪内存瓶颈。理解每种内存类型的特性是精通 CUDA 编程的前提。CUDA 性能分析器的自动分析可以引导开发者走向正确的方向。如何读取性能分析器的输出是创建高性能应用程序的核心技能。否则，寻找应用程序瓶颈将变成一种猜测。同样，CUDA 内存检查器可以帮助发现内存使用中的错误。

## 高效使用 GPU 内存

高效使用 GPU 内存的重要性不言而喻。由于最快的片上寄存器内存与必须跨越 PCIe 总线的映射主机内存之间速度存在大约三个数量级的差异，熟的 CUDA 开发者必须理解使用内存最高效的方法。通过 ILP（指令级并行）或 TLP（线程级并行）隐藏延迟对于应用性能至关重要。预取（Prefetching）可以保持更多的内存事务在进行中，将数据移动到快速内存，并加速受带宽限制的归约操作。不规则数据结构对于当前的 GPU 技术来说是一个挑战，但某些技术即使在随机内存访问时也能保持性能。然而，随着支持图和稀疏矩阵等不规则数据结构的新库出现，寻找利用 GPU 内存更好的方法是一个活跃的研究领域。

在本章结束，读者将对以下内容有基本的理解：

- 使用预取利用全局内存。
- 在基于 ILP 的归约内核中高效使用寄存器、共享内存和全局内存。
- 如何编写利用函数的通用方法。
- 加速具有不规则和随机内存访问问题的技术。
- 针对稀疏矩阵的通用方法和库。
- 图形中心性指标和可以提供 10 到 50 倍加速的代码。
- 使用 SoA 的性能原因。
- 模板（Stencils）和块（Tiles）。

### 归约（REDUCTION）

归约操作执行诸如寻找向量最小值、最大值或和等常见任务。为 GPU 计算编写高性能的归约操作异常地复杂，因为它要求对 CUDA 内存空间和执行模型有深入的理解。

`Thrust` API 提供了一个简单的接口，隐藏了归约的所有复杂性，使其既灵活又易用。`Thrust` 使用了 NVIDIA Mark Harris 设计的归约算法。演示各种归约优化的示例和代码包含在 NVIDIA SDK 的 `reduction` 目录中。建议阅读相关论文和代码。

本章提供了一个归约示例，该示例将前几个章节中的许多讨论内容结合在一起，并扩展了 Mark Harris 的归约：

- C++ 模板扩展了归约代码的通用性，可以使用定义的类型作为浮点数、双精度浮点数、整数、长整数等。
- 新功能...

```cpp
myVal = initVal;

// Use fastest memory first.

const int gridSize = blockDim.x*gridDim.x;

for(int i=n-1; i>=0; i-=blockDim.x+threadIdx.x)
  myVal = fcn(fcn(i),
```

通过其他线程。从寄存器到共享内存的传输发生在示例 6.5 所示的第 2 步。这是一个并行传输，将每个线程块中的所有线程传输到每个 SM 的共享内存变量 `smem`。

共享内存是一项宝贵的资源，因此只分配最少量。根据第 4 章对 ILP（指令级并行性）的讨论，仅一个 warp（线程束）的并行性是将每个 SM 上的 `N_THREADS` 个部分值归约为每个 SM 的 `WARP_SIZE` 个部分值。寄存器变量 `myVal` 已经包含了第一个 warp 的正确值。因此，共享寄存器内存只需要包含 `threadIdx.x` 大于或等于 `WARP_SIZE` 的线程中的 `myVal` 寄存器内容。结果是，`smem` 的分配元素可以比 `N_THREADS` 少。

由于从寄存器到共享内存的传输是并行发生的，因此在赋值后必须调用 CUDA `__syncthreads()` 方法以确保 `smem` 的所有元素都已写入。所有这些都发生在示例 6.5 的几行代码中，“functionReduce.h 的第 5 部分”。

### 示例 6.5

```cpp
// 2) 在 warp 中以最快的内存（共享内存）
// 以同步方式进行。
// 为每个线程块的归约创建共享内存。
// 重用第一个 warp 中的寄存器。
volatile __shared__ smem[N_THREADS-WARP_SIZE];

// 将所有寄存器值放入共享内存
if(threadIdx.x > WARP_SIZE) smem[threadIdx.x - WARP_SIZE]=myVal;
__syncthreads(); // 等待所有线程完成。
```

在内核的此点，没有理由使用比一个 warp 线程数更多的线程，因为 SM只能向每个 warp 发射单条指令。由于没有未解决的数据依赖，单个 warp 就足够让 SM 忙于将每个 SM 的共享内存内容从 `(N_THREADS - WARP_SIZE)` 个元素归约为 `WARP_SIZE` 个部分值了。这就是为什么使用条件判断来只保持 `threadIdx.x` 小于 `WARP_SIZE` 的线程处于激活状态。参见示例 6.6，“functionReduce.h 的第 6 部分”。

### 示例 6.6

```cpp
if(threadIdx.x < WARP_SIZE)
// 现在只使用一个 warp。SM 每次只能运行一个 warp
```

> 取决于计算代，SM 可能能够对半 warp（half-warp）发射指令。

## 第 6 章：高效使用 GPU 内存

```cpp
#pragma unroll
for(int i=threadIdx.x; i < (N_THREADS-WARP_SIZE); i += WARP_SIZE)
myVal = fcn(myVal,T(smem[i]));
smem[threadIdx.x]-=myVal; // 将此 warp 中的 myVal 保存到开头
semem;
```

剩余的是将每个 SM 上 warp 中的值归约为单一个值。这等同于 `N_BLOCKS` 个部分值，因为 `N_BLOCKS` 被定义为每个 SM 使用一个块。值得注意的是，此时 warp 内部的并行性对性能没有贡献，因为在示例 6.7 中进行了五次 `fcn(1)` 调用。

另一种实现可以使用在单个线程上运行（例如当 `threadIdx.x == 0` 时）的关于 `WARP_SIZE` 的简单循环来为每个 SM 创建单个部分值。如果 `fcn(1)` 是（加法）函数，这个串行版本将只执行 27 次加法，消耗极少的额外时间——大约 100 纳秒。因此，没有必要利用系统中的所有并行性。并行代码将非常简单，并且可能在未来的计算代中对我们有利，因此我们使用示例 6.7 中的实现，“functionReduce.h 的第 7 部分”

```cpp
示例 6.7
// 归约共享内存。
if (threadIdx.x < 16)
nsmem[threadIdx.x] = fcn(T(smem[threadIdx.x]),T(smem[threadIdx.x+16]));
if (threadIdx.x < 8)
nsmem[threadIdx.x] = fcn(T(smem[threadIdx.x]),T(smem[threadIdx.x+8]));
if (threadIdx.x < 4)
nsmem[threadIdx.x] = fcn(T(smem[threadIdx.x]),T(smem[threadIdx.x+4]));
if (threadIdx.x < 2)
nsmem[threadIdx.x] = fcn(T(smem[threadIdx.x]),T(smem[threadIdx.x+2]));
if (threadIdx.x < 1)
nsmem[threadIdx.x] = fcn(T(smem[threadIdx.x]),T(smem[threadIdx.x+1]));
```

最后的任务是将剩余的 `N_BLOCKS` 个部分值归约为单一个值以完成归约。在此处，代码可以：

- 将 `N_BLOCKS`（此例中为 14）个部分值传输到主机（host），那里将进行最后的归约。
- 利用 NVIDIA CUDA 编程指南 B.5 节描述的原子操作，确保在完成归约之前所有部分值都已写入全局内存。

由于两种实现都需要为 `N_BLOCKS` 个部分值分配临时空间，示例 6.8，“functionReduce.h 的第 8 部分”执行到主机的传输，因为它演示了在主机和设备上同时使用 `fcn1()`：

### 示例 6.8

```cpp
// 3) 作为最后的手段使用全局内存将结果传输到主机
// 将每个块的结果写入全局内存
if (threadIdx.x == 0) g_data[blockIdx.x] = smem[0];
// 如果需要，可以跨 SM 进行最终归约。
```

主机方法 `Reduce()` 在需要时分配部分和，而示例 6.9，“functionReduce.h 的第 8 部分”中的 CUDA 内核：

### 示例 6.9

```cpp
template<typename T, typename UnaryFunction, typename BinaryFunction>
inline void Reduce(int n, T** d_partialVals, T initVal,
UnaryFunction& fcn, BinaryFunction& fcn1)
if(*d_partialVals == NULL)
cudaMalloc(d_partialVals, (N_BLOCKS+1) * sizeof(T));
Reduce<T>(N_BLOCKS, N_THREADS>(d_partialVals, initVal, fcn1);
```

如示例 6.10，“functionReduce.h 的第 9 部分”所示，在完成归约之前，部分值从 GPU 传输到主机，并在那里进行最终归约。在 `functionReduce.h` 中，使用 `ifdef` 来保护归约。参见示例 6.10：

```cpp
template<typename T, typename UnaryFunction, typename BinaryFunction>
inline void Reduce(int n, T** d_partialVals, T initVal,
UnaryFunction& fcn, BinaryFunction& fcn1)
if(*d_partialVals == NULL)
cudaMalloc(d_partialVals, (N_BLOCKS+1) * sizeof(T));
Reduce<T>(N_BLOCKS, N_THREADS>(d_partialVals, initVal, fcn1);
if(*d_partialVals == NULL) {
    cerr << "cudaMalloc failed!" << endl;
    exit(1);
}
T val = initVal;
for(int i=0; i<N_BLOCKS; i++) {
val = fcn1(val,,_
}
}
```

## 第 6 章：高效使用 GPU 内存

```
T1 operator()(T2 i) {
    return data[i];
}
```

此测试利用了基于随机数最低位的 0 和1 随机序列。这些数字是通过代码中的函数对象创建的：

# 示例 6.14：随机数生成器

```
// 一个并行随机数生成器
// http://groups.google.com/group/thrust-users/browse_thread/thread/dca23bf67869a5
struct parallel_random_generator {
    unsigned int _device;
    unsigned int operator()(const unsigned int n) const {
        thrust::default_random_engine rng;
        // 丢弃数字以避免相关性
        rng.discard(n);
        // 返回随机数
        return rng() & 0x01;
    }
}
```

`dTest()` 例程是标准的 C++ 代码。指向临时空间的指针 `d_partialVals` 被设置为 NULL，这意味着第一次调用 `functionReduce()` 将分配所需的空间。设备向量 `d_data` 通过 thrust API 根据传递给此方法的变量 `nData` 的大小进行分配。

变量 `op` 选择将执行的测试。0 指定不使用预取（prefetching）；1 选择预取测试。任何其他值均指定调用 thrust 归约方法。参见示例 6.15，“testPrecu 的第 4 部分”。

# 示例 6.15：测试例程

```cpp
#define NTEST 100
template<typename T>
void doTest(const int nData, int op)
{
T* d_partialVals=NULL;
thrust::device_vector<I> d_data(nData);
// 用随机数（0 或 1）填充 d_data
thrust::counting_iterator<int> index_sequence_begin(0);
thrust::transform(index_sequence_begin,
    index_sequence_begin + nData,
    d_data.begin(), parallel_random_generator());
cudaThreadSynchronize(); // 等待所有队列任务完成
thrust::FCNLT<T> fcn;
double startTime, endTime;
T d_sum;
int initVal = 0;
switch(op) {
    case 0:
        memFetch<T, int> fcn(thrust::raw_pointer_cast(&d_data[0]));
        startTime=omp_get_wtime();
        for(int loops=0; loops < NTEST; loops++)
            d_sum = functionReduce<T>(nData, &d_partialVals, initVal,
                fcn, fcn);
        endTime=omp_get_wtime();
        cout << "NO prefetch ";
        break;
    case 1:
        prefetch<T, int> fcn(thrust::raw_pointer_cast(&d_data[0]));
        startTime=omp_get_wtime();
        for(int loops=0; loops < NTEST; loops++)
            d_sum = functionReduce<T>(nData, &d_partialVals, initVal,
                fcn, fcn);
        endTime=omp_get_wtime();
        cout << "Using prefetch ";
        break;
    default:
        startTime=omp_get_wtime();
        for(int loops=0; loops < NTEST; loops++)
