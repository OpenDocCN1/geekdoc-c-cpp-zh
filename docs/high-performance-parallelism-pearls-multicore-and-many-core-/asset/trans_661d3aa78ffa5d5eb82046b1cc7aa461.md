

- *选择性：* 这种亲和模式根据 *n*t 和 *nThreads* 的值，将控制线程绑定到逻辑核心 240、241、242、243 或 0 之一。任务执行线程可以在控制线程之前的任意逻辑核心上运行。

为了便于使用 *紧凑型*、*分散型* 和 *选择性* 亲和模式探索第 61 个核心，使用多个 *nThreads* 值来递增第 61 个核心上使用的逻辑核心数量，从 0 到 *n*t。例如，*nThreads* = 180 和 *n*t = 3 的运行配置在第 61 个核心上使用 0 个逻辑核心。考虑到这一点，控制线程会被绑定到给定模式使用的最后一个逻辑核心。例如，*nThreads* = 180 和 *n*t = 3 的运行配置将控制线程绑定到逻辑核心 240。

## 使用 PTHREADS 的线程放置

上一节提到，OpenMP 用户可以使用环境变量来指定线程放置。这些环境变量包括 **KMP_PLACE_THREADS** 和 **KMP_AFFINITY**。要了解更多关于这些环境变量的信息，请参阅 Intel 相应编译器的 *用户与参考指南* 中的 **OpenMP 支持** 部分。

与 OpenMP 不同，PThreads 要求开发者手动实现亲和模式。这可以使用 **sched.h** 头文件中的 **CPU_ZERO()**、**CPU_SET()** 和 **sched_setaffinity()** 函数来实现。有了这些函数，**sched_setaffinity()** 中的 *mask* 参数是关键。这个位掩码决定线程有资格在哪些逻辑核心上运行。图 13.6 演示了如何将线程（由 *pid* 标识）绑定到单个逻辑核心（由 *logCore* 标识）。对于本章使用的 Uintah 版本，我们在图 13.6 中的代码使用可以在 **Thread_pthreads.cc** 的 **set_affinity()** 中找到。

然而，请注意，图 13.6 不足以允许线程在逻辑核心子集之间运行。要实现这一点，可以重复使用 **CPU_SET()** 来向位掩码添加额外的逻辑核心。图 13.7 演示了如何允许线程在逻辑核心子集之间运行

```
cpu_set_t mask;
unsigned int len = sizeof( mask );
CPU_ZERO( &mask );
CPU_SET( logCore, &mask );
sched_setaffinity( pid, len, &mask );
```

### 图 13.6

指定一对一的线程绑定。

```
cpu_set_t mask;
unsigned int len = sizeof( mask );
CPU_ZERO( &mask );
for ( int logCore = 1; logCore < nThreads; logCore++ ) {
    CPU_SET( logCore, &mask );
}
sched_setaffinity( pid, len, &mask );
```

### 图 13.7

指定一对多的线程绑定。

（具体来说，即逻辑核心 1 到 nThreads-1 之间的任意位置）。对于本章使用的 Uintah 版本，我们在图 13.7 中的代码使用可以在 Thread_pthreads.cc 的 set_affinityMICMainOnly() 中找到。

### 注意

如果没有显式更改，用户定义的掩码将持续适用于随后启动的线程。在实现选择性线程绑定的亲和模式时，注意这一细节至关重要。这种情况需要结合图 13.6 和图 13.7 中描述的方法。

## 使用 PTHREADS 实现分散型亲和模式

分散型亲和模式比其他已讨论的模式需要更多的实现工作。因此，图 13.8 演示了如何使用 PThreads 实现分散型亲和模式。此示例假设每个线程由 threadID 唯一标识，并调用 scatterAffinity() 来表示它有资格在哪个逻辑核心上运行。注意，图 13.8 支持 threadID 从 0 到 243 的值，其中 threadID = 0 映射到逻辑核心 0。

对于本章使用的 Uintah 版本，我们在图 13.8 中的代码使用可以在 ThreadedMPIScheduler.cc 的 run() 中找到。注意，我们的实现与图 13.8 略有不同。具体来说，我们的实现将第 61 个核心作为特例处理，仅将线程分布在物理核心 1 到 60 上。这样做是为了支持我们对第 61 个核心的探索。

```
void scatterAffinity( int threadID ) {
    int scatterPhysCores = 61;
    int logCoresPerPhysCore = 4;
    int logCoreIndex = 0;
    int physCoreIndex = 0;
    int overallIndex = 0;

    // Determine whether the thread will be bound to the 1st, 2nd,
    // 3rd, or 4th logical core in a given physical core
    logCoreIndex = floor(( threadID-1 ) / scatterPhysCores ) + 1;

    // Determine which physical core the thread will be bound to
    physCoreIndex = ( threadID - (( logCoreIndex-1 ) * scatterPhysCores ));

    // Determine the specific logical core the thread will be bound to
    overallIndex = logCoreIndex + ( physCoreIndex-1 ) * logCoresPerPhysCore;

    // Bind the thread to its corresponding logical core
    cpu_set_t mask;
    unsigned int len = sizeof( mask );
    CPU_ZERO( &mask );
    CPU_SET( overallIndex, &mask );
    sched_setaffinity( 0, len, &mask );
}
```

### 图 13.8

基于 PThreads 的分散型亲和模式实现。

## 实验讨论

本节描述我们的实验设置，最后讨论实验结果。

### 机器配置

这些实验在单节点机器上执行，使用一个 MPI 进程和双精度浮点数。

主机端模拟使用 32 个线程分布在 16 个物理核心上启动。这通过双插槽配置中的两个 Intel Xeon E5-2680 处理器实现。

协处理器端模拟使用多达 244 个线程分布在 61 个物理核心上启动。这通过一个 16 GB Intel Xeon Phi 7110P 协处理器实现。

### 模拟配置

以下是协处理器端探索的关键参数：

- 三种物理核心使用级别（2、3 和 4 个硬件 TPPC）：
  - 对于 2 个硬件 TPPC，使用 3 个线程数来为第 61 个核心分配 0-2 个线程（120-122 个线程）。
  - 对于 3 个硬件 TPPC，使用 4 个线程数来为第 61 个核心分配 0-3 个线程（180-183 个线程）。
  - 对于 4 个硬件 TPPC，使用 5 个线程数来为第 61 个核心分配 0-4 个线程（240-244 个线程）。
- 四种亲和模式（*紧凑型*、*无*、*分散型* 和 *选择性*亲和）。
- 四种网格补丁数量（支持每线程 1、2、4 和 8 个补丁 [PPT] 的比率）。

关于模拟配置的说明如下：

- 模拟网格被分解为由单个单元组成的网格补丁。
- 任务由绑定到逻辑核心的线程执行。
- 任务驻留在网格补丁上，并使用单个线程串行计算。
- 可以使用不同的线程来计算特定网格补丁上的任务。
- 任务被分配给空闲线程，而不考虑它们访问的网格补丁数据的空间局部性。
- 模拟使用单级 128³ 模拟网格执行，因为这是协处理器支持的最大网格。
- 辐射建模计算在连续 10 个时间步上执行。
- 在每个计算时间步，模拟网格使用每单元 100 条射线进行采样。
- 主机端模拟探索了使用 32 个线程以及上述亲和模式和网格补丁数量的情况。

### 协处理器端结果

图 13.9 至 13.12 可视化了在协处理器端执行的 192 次模拟的结果。以下是关于协处理器端结果的说明：

- 标记对应每个计算时间步的平均执行时间（秒）。
- TPPC 对应每个物理核心使用的硬件线程数。
- 保留核心使用率（RCU）对应保留核心上使用的硬件线程数。为清晰起见，每个 RCU 值列举如下：
  - RCU = 0 对应使用 120、180 和 240 个线程，分别支持 2、3 和 4 个硬件 TPPC。
  - RCU = 1 对应使用 121、181 和 241 个线程，分别支持 2、3 和 4 个硬件 TPPC。
  - RCU = 2 对应使用 122、182 和 242 个线程，分别支持 2、3 和 4 个硬件 TPPC。
  - RCU = 3 对应使用 183 和 243 个线程，分别支持 3 和 4 个硬件 TPPC。
  - RCU = 4 对应使用 244 个线程，支持 4 个硬件 TPPC。
- PPT 对应网格补丁与线程的比率。注意，不能保证每个线程都计算这个数量的网格补丁。
- 在 10 次相同的协处理器端模拟中，两次相同运行之间的性能差异不超过 4.29%。
- 在 2、3 和 4 个硬件 TPPC 下，最快和最慢运行配置之间的性能差异分别为 30.14%、42.60% 和 149.33%。

![](img/16cb41208935c5f22dd1044f03f2e31b_288_0.png)

### 图 13.9

紧凑型亲和模式的协处理器端结果。

