

在使用图 9.2 所示的方案时尤其有用。此外，这使得 3D 渲染器能更好地适配各种多核架构配置，并有助于生成现代视频游戏中常见的成千上万个绘制调用。

## 9.3 Parallel Models

3D 渲染器是并行化的有力候选者，因为每个绘制调用通常可以被视为一个独立的工作单元。这些任务中的每一个都将一块数据与用于操作该数据的逻辑配对，如下面的代码清单所示。

```
int TaskMain(...)
{
    const int sourceAddr = ...; // source address of
    const int count = ...; // number of elements
    const int dataSize = count * sizeof(gfxObject);
    // On some platforms like the PS3,
    // you may have to keep the data local to the ex
    gfxObject *buffer = (gfxObject *) Allocate(dataSize)
    DmaGet(buffer, sourceAddr, dataSize);
    DmaWait(...); // barrier to wait for the data
    // let's do some work
    for (int i = 0; i < count; ++i)
    {
        buffer[i]->update();
    }
    // On some platforms like the PS3,
    // you may have to store back the data to system
    DmaPut(buffer, sourceAddr, dataSize);
    DmaWait(...); // barrier to wait for the data
}
```

该模型提供了一种高效的并行范式，其中每个任务都可以排队并由可用的处理单元消耗，如图 9.5 所示。这也避免了更标准的多线程方法的一些问题，因为任务提供了更细粒度的细分，并能更容易地应对不均匀的计算，而多线程架构可能最终会等待某个子系统完成其任务。

![](img/7ba1225bb0e5a87be0fd35866408ffa7_241_0.png)

图 9.5：任务存储在队列中，并由可用的处理单元消耗。

## 9.4 Synchronizing the GPU and CPU

在多线程环境中，同步 GPU 和 CPU 更难处理，因为多个处理单元可能都想访问相同的数据。为了避免任何不一致和竞态条件，需要使用互斥锁或原子操作等同步原语。通常，GPU 可以在特定内存区域中报告其进度。例如，当 GPU 上的某个特定命令完成后，它可以将指定值或“报告”写入 CPU 可访问的位置以指示完成。根据架构，CPU 可以轮询报告值或接收某种系统回调。表 9.1 列出了一些可能的配置。

### 表 9.1：同步 GPU 和 CPU。

| CPU | CPU | 报告 | 注释 |
|---|---|---|---|
| ... | WaitReport(22) | 0 | GPU 等待报告被设置 |
| SetReport(22) | WaitReport(22) | 22 | GPU 现已解锁 |
| ... | ... | 22 | |
| WaitReport(33) | | | CPU 等待报告被设置 |
| WaitReport(33) | SetReport(33) | 33 | GPU 设置了报告并解锁 CPU |
| ... | ... | 33 | |
| SetReport(12) | SetReport(15) | ? | 竞态条件 |
| WaitReport(33) | WaitReport(22) | ? | 死锁 |

与任何多线程环境一样，需要特别小心以避免潜在的竞态条件或死锁，因为 CPU 和 GPU 都可能以不可预测的时序模式生成和消耗数据。

## 9.5 Using Additional Processing Resources

在许多游戏中，可用处理单元之间的处理负载并未完全平衡。在这种情况下，将一些通常在主 CPU 上执行的操作移至每帧可能有空闲时间的其他单元可能是有价值的。例如，对图形要求不高的应用程序可以使用 CUDA 等技术，利用 GPGPU（通用 GPU）代码将物理或 AI 模拟从 CPU 卸载。另一方面，致力于突破实时 3D 图形极限的游戏可能希望使用空闲 CPU 核心来执行一些图形操作。如果这些核心提供了带有 SIMD 指令的有趣 ISA（指令集架构），例如 Cell 处理器上的 SPU，那么就有可能为多种操作卸载 GPU，例如以下操作：

- 几何处理，包括用于创建地形、树木、贴花或细分曲面的过程式算法。
- 物理和粒子系统更新。
- 视锥体物体剔除或遮挡剔除。
- 软件渲染，特别是用于遮挡查询和后处理效果。

## 9.6 Reducing the Pressure on the Memory Bandwidth

CPU 和 GPU 的性能都在以非常快的速度提升，但内存速度并未遵循同样的曲线，因此内存带宽正成为越来越显著的瓶颈。因此，考虑任何有助于尽量减少对内存系统需求的技术都很重要，即使这意味着使用更多的 CPU 或 GPU 周期。可使用的技术包括打包着色器输入和输出属性，或在可用时使用 GPU 的细分单元。在 CPU 侧，特殊的几何剔除可以避免发送多达 70% 最终会被 GPU 丢弃的原始图元（背面、屏幕外、零尺寸和退化原始图元）。另一种技术是在软件中生成粗糙深度缓冲区以执行遮挡查询，而不是依赖 GPU [1]，因为后者可能涉及从显存读回，这通常是一条缓慢路径。

## 9.7 Performing Graphical Operations in Parallel

迄今为止，我们讨论了一些有助于提升整体性能的技术，但我们可以更进一步，允许不同的处理单元并行工作以生成一帧的最终图像。现代游戏在单帧中使用多个渲染目标，其中一些不会被 GPU 同时访问。例如，通常可以使用另一个处理单元（如 SPU）访问后台缓冲区以执行一些后处理效果，而 GPU 开始渲染下一帧。这最多可提供一整帧的时间来渲染效果，同时保持相同的帧率，但代价是增加一帧的延迟（参见图 9.6）。

![](img/7ba1225bb0e5a87be0fd35866408ffa7_246_0.png)

图 9.6：当辅助线程计算后处理效果时，GPU 开始渲染下一帧。

## 参考文献

- [1] Johan Andersson. "游戏引擎与 GPU 的交汇点：当前与未来". Graphics Hardware 2008.
- [2] Sebastien Schertenleib. "ABT 树的高效缓存无感知实现". Game Programming Gems 5, Charles River Media, 2005.

## 第 10 章：面向多线程渲染的以摄像机为中心的引擎设计

Colt McAnlis

Blizzard Entertainment

## 概述

现代图形 API 通过允许在独立线程上创建绘制命令，赋予了并行渲染的能力。因此，先进的引擎设计必须具备实际可扩展的能力，以便利用增加的核心数量进行渲染。要实现这一点，引擎必须解决如何正确拆分渲染任务以进行并行计算的问题，但要做到这一点，它首先必须考虑渲染子系统实际上在做什么。

现代图形引擎需要对同一场景进行多次渲染，以帮助最终图像的整体外观。例如，计算阴影映射、运行时反射、屏幕分块（用于某些游戏主机的抗锯齿）、冒充体生成和屏幕外粒子，都需要对场景进行单独渲染。因此，将“摄像机”视为与环境可见性直接相关的最粗粒度场景组织形式是合乎逻辑的，因为要可视化上述任何概念，首先必须定义视图位置、视图方向，最终还需要一个用于存储结果的渲染目标。由于场景的大多数视图可以相互独立地进行渲染，我们认为按摄像机视图分组渲染工作负载，能提供最佳的渲染工作负载组织方式，以充分利用多核渲染。

在本文中，我们介绍了一种引擎设计，该设计利用摄像机概念来分离并行渲染作业，从而实现对多核系统的扩展。为实现此目标，我们介绍了两个概念。第一个是创建可记录命令缓冲区的 API 无关方法，这一过程使我们能够在任何设备上使用并行渲染。第二个是关于如何根据将使用的摄像机，将命令缓冲区的创建分发到独立线程的观察。利用这两个简单而强大的概念，可以使您的引擎以最少的

