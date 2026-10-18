

```
1: for i = 1, T do
2:     for j = 1, T do
3:         Set C_i,j to 0.
4:         for s = 1, T do
5:             cblas_dgemm(A_i,s, B_s,j, C_i,j);
6:         end for
7:     end for
8: end for
```

## FIGURE 15.3

Tiled matrix multiplication algorithm.

并发度由 T² 给出。这是因为 C 矩阵的每个分块都可以独立于彼此计算。任务总数由 T³ 给出，因为计算 C 矩阵的每个分块需要 T 次对 cblas_dgemm 的调用。

虽然将矩阵乘法分解为更小的任务可以用少数且简单的任务间依赖关系来完成，但对于其他算法，任务图可能更复杂。依赖关系越多，任务图中的平均并发度往往越低。并发度倾向于随着分块程度的增加而增加。图 15.4 显示了随着分块程度增加，平均并发度和总任务数的增加，以及从 Cholesky 到 LU 再到矩阵乘法的并发度增加，后者具有越来越少的依赖关系。性能也相应增加，部分原因就是并发度的增加。本章后面描述了 Cholesky 的算法和任务图（有关 Cholesky 任务图的参考见图 15.20）。对于并发度的此图，我们仅考虑计算并发度，即有多少计算任务可以并行执行。更广义的并发概念还考虑数据传输。此外

![](img/16cb41208935c5f22dd1044f03f2e31b_324_0.png)

## FIGURE 15.4

Concurrency of computes. Cholesky, LU, and matrix multiply have an increasing amount of total tasks and average concurrency, which correlates to performance, shown in parentheses. GFlops/sec (GFl/s) numbers are given for input matrix size of 16,000.

计算的并发度。Cholesky、LU 和矩阵乘法具有不断增加的总任务数和平均并发度，这与性能相关，性能以括号显示。GFlops/sec（GFl/s）数值对应于输入矩阵大小为 16,000。

计算。此外，这种类型的并发度也随着分块数量的增加而增加，因为我们可以将对矩阵 A 和 B 的某些输入分块的数据传输与对矩阵 C 的某些输出分块的计算重叠。下面，我们介绍流的概念，该概念使我们能够利用各种并发形式来提高性能。

我们接下来描述 hStreams 的一些关键特性，通过这些特性可以利用科学问题中可用的各种并发形式，仍然以矩阵乘法示例为例。我们将在介绍过程中介绍 hStreams 的各个方面，而 hStreams 部分后面将详细描述 hStreams 的特性。

## HETEROGENEOUS STREAMING: CONCURRENCY AMONG COMPUTING DOMAINS

一旦对矩阵乘法应用分块，我们就有了任务并发。如果存在不同的计算域，例如通过网络连接的多核处理器或更新的 Intel Xeon 处理器，或通过 PCIe 连接的多核协处理器，其能力更强，但将数据移入移出会产生成本呢？我们已经看到，对于边长为 N 的方阵，计算负载为 O(N³)。但由于元素数量仅为 O(N²)，一旦计算能力的优势超过分配远程空间和来回移动数据的成本，将计算转移到另一个计算域执行是值得的，这发生在 N 足够大时。关于 N 的值何时变得如此有利的详细分析，作为数据传输速率和相对计算效率的函数，可以在本书网站上的 hStreams 资源中找到（http://lotsof cores.com/hStreams）。我们将用于管理特定计算资源子集上发生的工作的、数据传输、计算和同步操作的机制称为流。hStreams 和 Intel 编译器的 Offload Streams 功能都支持这种流式传输。两者之间的差异在相关工作部分中描述。

将工作从一个计算域转移到另一个计算域可能会提高效率。通过在源计算域和卸载端点同时执行任务来实现并发。hStreams 允许使用单一统一的流抽象来在任何一组资源上传输、完成和同步工作，而不必使使用的抽象取决于工作发生的位置。图 15.7 显示了当卸载到协处理器上的元素边长超过约 1200 时性能更好。图 15.20 对 Cholesky 显示了类似的结果。这些结果将在后面详细讨论。我们在本章中呈现的所有性能测试所使用的机器配置在图 15.5 中给出。

## PIPELINING WITHIN A STREAM

如果我们将要在另一个计算域中执行的任务孤立处理，我们必须传输数据、执行工作，然后在处理下一个任务之前传输数据回来。这是一个串行、同步的序列。如果我们有多个这样的任务，并且不孤立处理它们，我们可以在流内使用流水线来重叠甚至隐藏大部分通信在计算之后。那就创造了计算与通信（数据传输）之间的并发。我们将在下面展示流水线和流并发的影响。

| Specification | Intel Xeon Processor E5-2697v2 | Intel Xeon Phi Coprocessor 7120A |
|---|---|---|
| Sockets × cores × SMT | 2 × 12 × 2 | 1 × 61 × 4 |
| Clock (GHz) | 2.7 | 1.33 (turbo-on) |
| RAM | 64 GB DDR3-1600 MHz | 16 GB GDDR5 |
| L1 data cache (kB) | 32 | 32 |
| L1 instruction cache (kB) | 32 | 32 |
| L2 cache (kB) | 256 | 512 |
| L3 cache (kB) | 30,000 (shared, per socket) | – |
| OS | RHEL 6.4 | Linux |
| Compiler | Intel 15.0.1 | Intel 15.0.1 |
| MPSS | MPSS 3.5 | MPSS 3.5 |

## FIGURE 15.5

Machine configuration.

机器配置。

## STREAM CONCURRENCY WITHIN A COMPUTING DOMAIN

使用 hStreams，异构流不限于每个计算域一个。任何给定的计算域都可以细分，其中流与资源子集相关联。如图 15.6 所示，使用多个流，每个流具有较少数量的核心，可提高协处理器上独立 dgemm 任务的整体原生（非卸载）吞吐量。对于此图，执行的独立并发 dgemm 的数量为 60/核心数。例如，如果每个 dgemm 仅使用 2 个核心，则执行 30 个并发 dgemm 任务。虽然这些数据与原生

![](img/16cb41208935c5f22dd1044f03f2e31b_326_0.png)

## FIGURE 15.6

Native compute efficiency versus concurrency. As the number of cores per dgemm task decreases, the number of concurrent dgemms increases, bringing increasing throughput performance for independent native dgemms up to a small number of cores per task. The benefits are greater for smaller matrices, though the overall performance is lower for smaller sizes. Performance is measured relative to peak efficiency. Performance can fall off at the right, where the number of independent dgemms is very large.

原生计算效率与并发度。随着每个 dgemm 任务的核心数减少，并发 dgemm 的数量增加，从而使独立原生 dgemm 的吞吐量性能不断提高，直到每个任务的核心数很小。收益对于较小的矩阵更大，尽管较小尺寸的整体性能较低。性能相对于峰值效率进行测量。性能可能在右侧下降，在那里独立 dgemm 的数量非常大。

执行有关，但同样的原理也适用于卸载使用。如果将传输、计算和同步操作流式传输到并发地传输到异构平台中不同计算域中分布的多个资源子集，您可能能够提高整体性能。

## TRADE-OFFS IN PIPELINING, TILING, AND OFFLOAD

hStreams 的一个关键价值在于它使探索优化空间变得更容易，在该空间中存在许多权衡需要做出。首先，我们强调流水线、分块和卸载中的权衡；接下来，我们将研究分块程度和流数量的权衡。让我们看看矩阵乘法性能，以 GFlops/s 为单位，作为矩阵大小的函数，使用 MKL cblas_dgemm 函数，如图 15.7a 所示。在此图中，我们显示了主机与协处理器、协处理器仅计算与卸载、2 × 2 分块与未分块、流水线与非流水线、一个流与四个流的影响。图 15.7b 显示了矩阵大小小于 2000 的放大图。协处理器仅计算是指使用编译器卸载 dgemm 但仅测量协处理器上的计算时间，而忽略向/从协处理器传输数据的传输时间。编译器卸载是指使用编译器卸载 dgemm 并测量向/从协处理器传输数据的时间以及协处理器上的计算时间。两者都是未分块、未流水线且无并发。分块 hStreams 卸载是指我们在图 15.11 中描述的程序，该程序默认分块、流水线并在流之间具有并发。对于 2 × 2 矩阵分块，评估了具有一个流和四个流的两种情况。对于一个流，报告了流水线以及非流水线（顺序）情况下的结果。最后，还报告了具有一个流的未分块 hStreams 卸载情况。

所有卸载情况下的性能都低于协处理器仅计算，因为它们包括额外的传输开销。唯一的例外是具有一个流的未分块 hStreams 卸载情况，对于最小的矩阵大小 400 和 600，其性能优于协处理器仅计算情况。具有一个流的未分块 hStreams 卸载与矩阵大小大于约 3000 的未分块编译器卸载相匹配，并且性能与共享通用基础设施的编译器 Offload Streams 相似。对于较小的矩阵大小，具有一个流的未分块 hStreams 卸载在卸载程序中性能最佳。流水线的影响显示为一个流和 2 × 2 分块的非流水线和流水线 hStreams 线之间的差异。在非并发一个流的情况下，2 × 2 分块的性能低于未分块编译器卸载情况，直到矩阵边长接近 12,000。最后，具有四个流水线流和 2 × 2 分块的分块 hStreams 优于编译器卸载的未分块矩阵，除非是一些非常小的尺寸。卸载在除非常小的尺寸外的所有情况下都优于主机性能，因为协处理器提供更高的性能。对于具有单个流的未分块情况，流水线没有任何区别，因为传输和计算任务之间存在依赖关系，因此未显示。

## Small matrix performance

为了了解分块 hStreams 在何处以及为何具有性能优势和劣势，我们更仔细地查看图 15.8 中小尺寸发生的情况。小尺寸时的关键性能因素是（1）异步传输的固定开销，（2）接收端的分块效率，以及（3）覆盖传输时间的机会。实线显示了与未分块编译器卸载相比，2 × 2 分块 hStreams 具有四个流水线流的相对性能。该线几乎始终保持在 0 以上，唯一例外是矩阵大小为 800，并且在此范围内通常高出 25% 或更多。它跟踪了

