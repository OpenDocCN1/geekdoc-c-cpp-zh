
第 9 章。提供了一个基于本章框架的实时视频流识别示例。它是为教学设计的，因此很容易修改用于平视显示器（HUD）的数据融合。

第 10 章。为了教授可扩展性和性能，第 3 章的示例被扩展为使用 MPI（消息传递接口）。

第 11 章。没有任何书能涵盖 CUDA 的所有方面。这是一个综述章节，指向其他为各种技术提供运行源代码的项目，包括支持向量机（SVM）、多维缩放（MDS）、互信息和力导向布局。

第 12 章。本章聚焦于实时视频流识别。提供了一个运行示例，只需要一个廉价的摄像头或视频文件，即可进行实时视觉处理。

# 前100个 NVIDIA CUDA应用展示加速比

(最小 100，最大 2600，中位数 1350)

![](img/4468c911ce4bde7a67079b9c80978769_18_0.png)

**图 1**

前 100 个 NVIDIA 应用的加速比。

通过提高时钟频率来实现加速。传统处理器制造商诱导客户升级新电脑的唯一方法，是通过双核和四核处理器的并行性提供两到四倍的加速。多核并行是具有颠覆性的，因为它要求重写现有软件以利用这些额外的内核。当计算机和研究行业重新调整工具以利用并行硬件时，请加入软件应用开发和研究的最前沿！学习 CUDA，并加入这一绝佳机会。

## 第一个程序以及如何在 CUDA 中进行思考

本章的目的是向读者介绍 CUDA（由 NVIDIA 开发的并行计算架构），并将 CUDA 与编程传统的单核和多核处理器区分开来。示例程序和指令将向读者展示如何编译和运行程序，以及如何将其调整以适应自己的需求。我们将使用并讨论 CUDA Thrust 和运行时 API（应用程序编程接口）。我们将引入三个 GPU 编程规则，并类似于阿姆达法则，区分数据并行编程和任务并行编程。我们将介绍一些基本的 GPU 调试工具，但在大多数情况下，NVIDIA 使调试代码与调试任何其他 C 或 C++ 完全相同。在适当的情况下，将提供介绍性材料以帮助帮助读者。在本章结束，读者将能够编写和调试同步并行程序，在单个应用程序中同时利用 GPU 和主机处理器处理海量的执行线程。

在本章结束，读者将对以下内容有基本的理解：

- 如何创建、构建和运行 CUDA 应用。
- 决定使用哪种 CUDA API 的标准。
- 阿姆达法则以及它与 GPU 计算的关系。
- 高性能 GPU 计算的三条规则。
- 大 O 表示法和数据传输的影响。
- 任务并行与数据并行编程之间的区别。
- Linux、Mac 和 Windows CUDA 调试器的某些 GPU 特定功能。
- CUDA 内存检查器以及如何发现越界和未对齐的内存错误。

# 第 1 章：第一个程序以及如何在 CUDA 中进行思考

### 源代码与维基

书书中所有示例的源代码可以从 `http://booksite.mkp.com/9780123884268` 下载。提供了一个维基（一个由用户社区协作开发的网站）用于共享信息、评论和查找教学材料；可以通过以下任何一个别名访问：`gpucomputing.net`:

- 我的名字：`http://gpucomputing.net/RobFarber`
- 本书标题的单词形式：`http://gpucomputing.net/CUDAapplicationdesignanddevelopment`
- 我系列丛的名字：`http://gpucomputing.net/supercomputingforthemmasses`

### 通过简单示例区分 CUDA 与传统编程

为顺序处理器编写程序需要编写一个程序，指定计算某些结果所需的每项任务。参见示例 1.1，“`seqSerial.cpp`，一个顺序执行的 C++ 程序”：

#### 示例 1.1

```cpp
//seqSerial.cpp
#include <iostream>
#include <vector>
using namespace std;
int main() {
    const int N=50000;
    // 任务1: 创建数组
    vector<int> a(N);
    // 任务2: 填充数组
    for(int i=0; i < N; i++) a[i]=i;
    // 任务3: 计算数组之和
    int sumA=0;
    for(int i=0; i < N; i++) sumA += a[i];
    // 任务4: 计算 0 .. N-1 之和
    int sumCheck=0;
    for(int i=0; i < N; i++) sumCheck += i;
    // 任务5: 检查结果是否一致
    if(sumA == sumCheck) cout << "Test Succeeded!" << endl;
}
```

### 通过简单示例区分 CUDA 与传统编程

```cpp
else cerr << "Test FAILED" << endl; return(1);
return(0);
```

示例 1.1 执行了五项任务：

1. 它创建了一个整数数组。
2. 一个 `for` 循环用从 0 到 `N-1` 的整数填充数组。
3. 计算数组中整数之和。
4. 另一个独立的 `for` 循环通过另一种方法计算整数之和。
5. 比较检查顺序执行和并行的结果是否相同，并报告测试结果。

注意，处理器一个接一个连续地运行每个任务。在任务 2-4 内部，处理器从第一个索引开始迭代循环。一旦所有任务完成，程序就会退出。这是一个单线程执行的示例，如图 1.1 中的任务 2 所示，一个单线程填充了数组 `a` 的前三个元素。

该程序可以使用以下命令编译和执行：

- Linux 和 Cygwin 用户（示例 1.2，“使用 `g++` 编译”）

示例 1.2

```bash
g++ seqSerial.cpp -o seqSerial
./seqSerial
```

Microsoft Visual Studio 用户利用命令行界面（示例 1.3，“使用 Visual Studio 命令行接口编译”）

示例 1.3

```bash
c1.exe seqSerial.cpp -o seqSerial.exe
seqSerial.exe
```

![](img/4468c911ce4bde7a67079b9c80978769_22_0.png)

图 1.1

单线程执行。

# 第 1 章：第一个程序以及如何在 CUDA 中进行思考

当然，所有的 CUDA 用户（Linux, Windows, MacOS, Cygwin）都可以使用 NVIDIA 编译器（示例 1.4，“使用 `nvcc` 编译”）

#### 示例 1.4

```bash
nvcc seqSerial.cpp -o seqSerial
./seqSerial
```

在所有情况下，程序都会打印“Test succeeded!”

为了对比，让我们创建并运行第一个 CUDA 程序 `seqCuda.cu`。（注意：以下示例使用了 CUDA Thrust API（前缀为 `thrust:`），CUDA 代码与顺序 C++ 代码几乎相同。参见示例 1.5，“使用 Thrust API 的大规模并行代码”）

#### 示例 1.5

```cpp
//seqCuda.cu
#include <iostream>
using namespace std;

#include <thrust/reduce.h>
#include <thrust/sequence.h>
#include <thrust/host_vector.h>
#include <thrust/device_vector.h>

int main() {
    const int N=50000;
    // 任务1: 创建数组
    thrust::device_vector<int> a(N);
    // 任务2: 填充数组
    thrust::sequence(a.begin(), a.end(), 0);
    // 任务3: 计算数组之和
    int sumA = thrust::reduce(a.begin(),a.end(), 0);
    // 任务4: 计算 0..N-1 之和
    int sumCheck=0;
    for(int i=0; i<N; i++) sumCheck += i;
    // 任务5: 检查结果是否一致
    if(sumA == sumCheck) cout << "Test Succeeded!" << endl;
    else cerr << "Test FAILED!" << endl; return(1);
    return(0);
}
```

### 选择 CUDA API

时间 0

数组 a | 0 | 1 | 2 | 3 | 4

#### 1.2 并行线程

的执行。

与图 1.1 中的单线程执行不同，示例 1.5 中的代码利用许多线程来执行大量的并发操作，如图 1.2 中任务 2 填充数组 `a` 所示。

无论应用程序中使用何种 API 或 API 的组合，CUDA 都可以从其他高级语言（如 Python、Java、FORTRAN 等）调用。调用约定和所需的细节随每种语言而不同。

### 选择 CUDA API

CUDA 为编程提供了多个 API 供使用。从高层到低层如下：

1. 数据并行 `Thrust` API
2. 运行时 API，可以在 C 或 C++ 中使用
3. 驱动程序 API，可以在 C 或 C++ 中使用

### 第一章：第一个程序与 CUDA 思维

使用哪种 API 取决于开发者对 GPU 的控制程度。像 C++ `Thrust` API 这样高层的 API 是方便的，因为它们能为程序员完成许多工作，但它们也会代表程序员做出决策。通常情况下，`Thrust` 被证明可以提供更高的计算性能、通用性和便利性。它还能加速代码开发，并生成更易于读的代码，许多人会认为这种代码更具维护性。在不进行任何修改的情况下，用 `Thrust` 编写的程序大部分能够保持或提高性能。像规约（reduction）这样的 `Thrust` 方法执行了大量工作，这使得 `Thrust` API 开发者有充分的自由整合最新硬件中的特性来提高性能。`Thrust` 是一个设计良好的 API 示例，它既简单又通用，并且能够随着技术演进适应性能需求。

`Thrust` 这种高层 API 的缺点是它会将开发者与硬件隔离，并且仅暴露能力的子集。在某些情况下，C++ 接口可能会变得繁琐或冗长。特别是科学程序员可能会发现简单循环的清晰性在 C 语言语法中丢失。

首先使用高层接口，当你认为额外的编程工作将带来更大的性能提升，或者为了更好地支持你的应用而需要某些低层能力时，选择切换到低层 API。CUDA 运行时（runtime）特别设计用于通过对 C 语言进行一些简单、优雅且强大的语法增强，让开发者能够访问 GPGPU 的所有可特性。因此，CUDA 运行时代码有时可能是最简洁、最易读的 API；它可以运行得极其高效。最低级驱动接口的一个重要方面是，它可以对队列队列和数据传输提供非常精确的控制。

当使用低层接口时，预计代码量会增加，因为开发者必须进行更多的 API 调用和/或为每次调用指定更多参数。此外，开发者需要检查运行时错误和版本不兼容性。在许多使用低层 API 的情况下，应用程序代码中许多行关注 API 接口的细节而非任务的实际工作并不罕见。

幸运的是，现代 CUDA 开发者不再限制在应用程序中使用单一的 API，这在 2010 年 CUDA 3.2 发布之前是不可能的。现代版本的 CUDA 允许开发者根据需要随时在应用程序中使用三种 API 中的任何一种。因此，初始代码可以用 `Thrust` 等高层 API 编写，然后重构以使用运行时或驱动程序 API 的某些特殊特性。

### 选择 CUDA API

让我们利用这种混合不同层次 API调用的能力，来突出并更显式地展示之前示例中顺序填充任务（任务 2）的并行性质。示例 1.7 “使用 CUDA 运行时用顺序整数填充数组”也为我们提供了介绍 CUDA 运行时 API 的机会：

### 示例 1.7

```cpp
//seqRuntime.cu
#include <iostream>
using namespace std;
#include <thrust/reduce.h>
#include <thrust/sequence.h>
#include <thrust/host_vector.h>
#include <thrust/device_vector.h>

__global void fillKernel(int* a, int n) {
    int tid = blockIdx.x*blockDim.x + threadIdx.x;
    if (tid < n) a[tid] = -tid;
}

void fill(int* d, int n) {
    int nThreadsPerBlock = 512;
    int nBlocks = n/nThreadsPerBlock + (n%nThreadsPerBlock)?1:0;
    fillKernel<<<nBlocks, nThreadsPerBlock>>>(d_a, n);
}

int main() {
    const int N=50000;
    // task 1: 创建数组
    thrust::device_vector<int> a(N);
    // task 2: 使用运行时填充数组
    fill(thrust::raw_pointer_cast<int>(&a[0]), N);
    // task 3: 计算数组之和
    int sumA=thrust::reduce(a.begin(),a.end(), 0);
    // task 4: 计算 0 .. N-1 之和
    int sumCheck=0;
    for(int i=0; i<N; i++) sumCheck += i;
    // task 5: 检查结果一致
    if(sumA == sumCheck) cout << "Test Successful!" << endl;
    else cerr << "Test FAILED!" << endl; return(1);
    return(0);
}
```

![](img/4468c911ce4bde7a67079b9c80978769_26_0.png)

### 第一章：第一个程序与 CUDA 思维

代码中修改过的部分已加粗显示。为了尽量减少对 `main()` 结构的更改，对 `thrust::sequence()` 的调用替换为对 `fill()` 的调用，该函数是使用运行时 API 编写的。因为数组分配了 `thrust::device_vector`，所以需要使用 `thrust::raw_pointer_cast` 来获取 GPU 上的数据。CUDA 运行时代码有时是最简洁、最易读的 API；它可以运行得极其高效。良好的 C++ 实践将是传递 `int**；通过 `a.size()` 安全地确定 vector 中的元素数量；以及其他原因。

### 基础 CUDA 概念

在讨论运行时 `fill()` 子程序之前，理解一些 CUDA 概念很重要：

- 支持 CUDA 的 GPU 安装在主机上。在大多数情况下，GPGPU 通过 PCIe（外围部件连接）总线连接到主机系统。
- 二到四个 GPGPU 可以添加到工作站或集群节点中。数量取决于主机系统的能力，如 PCIe 插槽、电源和散热。每个 GPGPU 都是与主机异步运行的设备，这意味着主机和所有 GPGPU 可以同时忙于计算。PCIe 总线用于在设备之间传输数据和命令。CUDA 提供了各种传输机制，包括：
- 使用 `memcpy` 进行显式数据传输（最常用的运行时数据传输方法）。使用 Thrust 的可以通过赋值在向量之间移动数据（参见示例 1.8 “如何使用 Thrust 移动数据”）

示例 1.8

```cpp
//使用 thrust 将数据从主机移动到设备
d_a = h_a;

//从设备到主机
h_a = d_a;
```

### 基础 CUDA 概念

使用映射内存（mapped memory）进行隐式传输。这种接口保持主机内存区域与 GPU 内存区域的同步，且不需要程序员干预。例如，应用程序可以在主机上加载数据集，将其映射到 GPU，然后像已显式初始化过一样使用 GPU 上的数据。使用映射内存可以提高程序的效率，因为传输是异步的。某些低功耗 GPGPU 利用主机内存来节省成本和功率。这些设备上，使用映射内存会导致零拷贝操作，因为 GPU 将在没有任何任何拷贝操作的情况下访问数据。

在底层，主机和 GPGPU 硬件通过称为设备驱动程序的软件组件进行交互。驱动程序管理硬件接口，以便 GPU 和主机系统能够通信、计算和显示信息。它还支持许多操作，包括映射内存、缓冲、队列和同步。CUDA 软件栈的组件如图 1.3 所示。

GPGPU 运行在独立主机处理器的内存空间中。除了少数低端设备外，所有 GPGPU 都有自己的物理内存（例如 RAM），这些内存旨在提供远高于传统主机内存的带宽。许多当前的

图 1.3

软件栈的组件。

# 10 第1章：第一个程序与 CUDA 思维

GPGPU 内存系统的传输速度约为 160-200 GB/s（每秒十亿或字节），而传统的主机内存系统仅提供 8-20 GB/s。尽管 CUDA 4.0 提供了统一虚拟地址（UVA），将主机内存和 GPGPU 内存合并到单一的统一地址空间中，但不要忘记，访问另一个设备需要通过总线（即 GPGPU 之间）进行一些传输。然而，UVA 非常重要，因为它让运行在任何设备上的软件能够仅通过指针就访问另一个设备上的数据。

- CUDA 程序利用内核函数（kernels），这些是从主机端调用的、在 CUDA 设备上执行的子程序。需要注意的是，内核函数不是函数，它们不能返回值。大多数在 GPGPU 上运行良好的应用程序，其大部分时间都花在一个或几个计算例程中。将这些例程转换为 CUDA 内核函数是加速应用程序和利用 GPGPU 力的极佳方法。内核函数使用全局声明说明符定义，它告诉编译器该内核可以被主机处理器调用。
