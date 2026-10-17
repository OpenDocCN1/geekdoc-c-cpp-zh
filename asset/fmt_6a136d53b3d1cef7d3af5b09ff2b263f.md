
在内核驱动的事件上，所有数据结构都将失效，处于脏状态的从系统内存传输到加速器。不需要返回数据，从而减少了开销。这种方法有两个优点：(1) 只有由 CPU 修改的数据会被传输到加速器；(2) 只有来自加速器的数据结构会被传输到系统内存，这在批量更新策略具有性能收益的应用中，以及在 GPU 上执行的代码处理加速器上执行的代码使用或产生的部分数据时，性能得到了提高。

滚动更新是一种混合“写-失效”协议。系统内存块不会失效，与批量更新和延迟更新一样，内存保留了一个共享地址列表和分配对象的尺寸。此列表中的每个元素都是共享对象，它是相应共享内存范围的一部分。如果共享对象小于默认内存块大小，它将包含较大的值。使用与之前相同的保护机制。这里使用对脏和只读数据结构的内存访问来检测和写、以及只读块。该协议仅允许加速器上固定数量的块处于脏状态。当一个块变为脏状态时，它会失效并从系统内存传输到加速器内存，并且该块被标记为只读。为了减少开销，我们使用自适应方法来设置滚动大小：每个新的内存结构都按一个倍数增加（默认值为 2 块）。这种方法利用了同时使用所有分配数据结构的转换特性。在……之间创建差异

## 5. 实验结果

本节展示了在具有双核心 SMP 上对 GPU 进行实验评估。我们的实验使用频率为 3GHz 的 AMD Dual-Core 2200 核心以及 8GB 内存。具有 1GB 设备显存的 NVIDIA G280 GPU 卡通过 PCIe 2.0 16x 总线连接。

### 5.1 一致性协议

![](img/03d0eb09047dbcab29ca9be26a1a08a3_367_0.png)

![](img/03d0eb09047dbcab29ca9be26a1a08a3_367_1.png)

**图 7.** 针对不同 CUDA 版本，`Parboil` 基准测试不同 `GMAC` 版本的减速情况。

**图 9.** 不同卷大小下 `3-Stencil` 计算的执行时间。

![](img/03d0eb09047dbcab29ca9be26a1a08a3_367_2.png)

**图 8.** `Data-batch` 基准测试中不同输入卷大小和内存块大小下通过不同协议传输的数据。随着卷的增加，`rolling-update` 带来的收益大于延迟带来的影响。`3-Stencil` 计算在每个时间步都需要在目标卷上引入源数据，这往往导致零重叠。它代表了位于某点的较小局部内存。在该空间内，CPU 执行处理源数据的代码。`rolling-update` 在传输由 CPU 获取的内存块之前，需要整个卷的数据。这是 `rolling-update` 延迟性能提升的主要来源。

使用惰性更新（`lazy-update`）和滚动更新（`rolling-update`）实现了与原始 `CUDA` 实现相同的性能。

图 8 显示了通过惰性更新和批量更新（`batch-update`）传输的数据。批量更新的一致性导致从系统内存到加速器创新的内存上产生了较长的执行时间。这说明了第一种收益：由运行系统自动管理数据传输。程序员倾向于采用过于保守的方法，即使在不需要数据时也传输数据。以数据为中心的编程模型允许数据管理，从而避免了不必要的数据传输。

图 9 展示了传输数据量与过量带宽使用的关系。该图显示，内存块大小为 32KB 和 1KB 时执行时间较长，但对于较大的块大小，差异可以忽略不计。源数据的引入只需访问一个内存块，因此数据量取决于内存块的大小。`3-Stencil` 计算还需要将数据写入输出端，因此必须从加速器内存中传输整个卷。

原始 `CUDA`、`lazy-update` 和 `rolling-update` 方法的执行时间相等。在某些基准测试中，这对 `GMAC` 来说是小幅加速。这显示了 `GMAC` 的第二种收益：使用编程编写手工调优内核的应用程序产生更好的效果。`rolling-update` 对共享对象的细粒度处理避免了不必要的数据传输（图 8 中的 mi-ri 和 ri-q）。通过 `3-Stencil` 计算说明了 `rolling-update` 的性能优势。图 9 显示了……的执行时间。

从大内存块写入磁盘写入可以更高效地利用互连带宽。随着块大小的增加，写入对输出时间的贡献变得更加重要，因此，较大的内存块大小减少了写入操作。

图 7 和 8 显示了传输数据量与执行时间之间的关系。批量更新最大的减速出现在向硬件支持或从硬件支持传输大量数据的基准测试中。

图 10 显示了所有使用 `rolling-update` 的基准测试的执行时间分解。大部分执行时间花在 CPU 或 GPU 上。在需要从读取或写入数据的基准测试中，I/O 操作是所有基准测试中次要耗费资源的操作。内存访问耗时最少。我们对检测不存在和只读内存块访问的处理微乎其微，低于总执行时间的 2%。图 10 还显示了基准测试（mi-ri 和 ri-q）

![](img/03d0eb09047dbcab29ca9be26a1a08a3_368_0.png)

图 10. `Parbench` 基准测试的执行时间图，具有高水平的 I/O 读取活动，并从不支持 peer DMA 的硬件中获益。

### 5.2 内存大小

内存块大小是滚动协议的关键设计参数。内存块大小越大，处理器触发的页错误就越少。然而，较小的内存块大小对于轻松从系统传输数据到加速器以及避免从加速器内存进行非阻塞数据读取至关重要。

我们使用不同内存块大小运行 `Parbench` 基准测试的首次实验结果显示，`Parbench` 基准测试的执行时间没有明显差异，这是由于 CPU 代码访问托管数据对总执行时间的贡献很小。

我们使用一个微基准测试（累加 800 万个元素）来展示执行时间如何随不同的内存块值变化。图 11 显示了不同内存块大小的执行时间。我们还绘制了每个块大小的传输带宽。传输带宽随块大小增加而增加，在块大小为 32MB 时达到最大值。数据传输时间随块大小增加而减少。从 4KB 到 8KB 以及从 8KB 到 16KB，数据传输带宽的执行时间减少更多。较小的内存块大小有利于产生和消耗数据集。在页上，`GMAC` 搜索错误块以修改权限和状态。`GMAC` 检查加速器缓存中的块。对于固定数据大小的对象，小块大小需要更多元素进入平衡二叉树；然而，由于搜索时间的原因，它变成了互连网络的瓶颈，并由于页错误减少了提供 CPU 的带宽。

图 1 中 64KB 块存在异常。该内存块大小小于其他块大小。原因是 CPU 的激进数据传输（eager data transfer）。内存块大小小于其他块大小。原因是 CPU 的激进数据传输。内存块大小小于其他块大小。原因是 CPU 的激进数据传输。

![](img/03d0eb09047dbcab29ca9be26a1a08a3_368_1.png)

图 11. 不同向量和块大小下向量加法的执行时间（折线）和最大传输带宽（框）。

基准测试中，当块大小从 4KB 增长到 64KB 时，传输块到加速器所需的时间超过初始化 CPU 并等待上次传输完成的时间。因此，较小的块大小对于将数据传输与计算叠加至关重要。

### 5.3 滚动大小（Rolling Size）

在实验中，我们使用滚动大小（脏状态内存块的最大数量）。滚动大小以两种方式影响应用程序性能。滚动大小越小，传输到加速器内存的数据越多，然而传输与计算的重叠越少。其次，内存块只有在从块缓存中逐出时才是只读的。每个逐出的块都会触发对逐出块内存位置的写入以及块逐出。对于所有 `Parbench` 基准测试，故障持续存在。

`Parbench` 基准测试的执行时间说明了可以通过滚动大小管理的病态。当滚动大小为 1、2 和 4 时，故障时间随块大小增加而减少。对于滚动大小为 1 和 2 的情况，小内存块大小，数据从系统内存传输到加速器内存。故障时间随滚动大小增加。因此，共享对象的内存块仅在 CPU 将状态设置为只读之前被写入并传输到加速器内存。随着内存块大小的增加，故障减少，但故障执行时间增加。当内存块大小达到临界值（2MB-2 和 4MB-1）时，内存块在随后的逐出之前就会触发。滚动大小下输入数据集的执行时间由于不必要的更新而急剧增加。

## 相关工作

### 编程模型

大多数针对大规模并行系统的编程模型都处理机器集群上的数据分布和调度。数组 [37] 提供了定义分布式系统上访问的语义。在以数据为中心的编程模型中，加速器内存持有内核（`kernel`）所需的所有数据，如果数据跨内核之间使用，则不需要进行数据分布。数组被标记为以数据为中心的编程模型，如果数组的执行是在加速器之间进行分布的，则可能会被使用。[42] 将程序分解为组件，程序员必须通过共享内存对这些组件进行管理和通信。这些数据依赖信息被 `ASIST` 运行时用于在不同处理器上调度模型的执行。这种以数据为中心的编程模型减少了向计算单元传输的数据量。

`Darlington` [14] 使用骨架函数（`skeleton functions`）将并行算法映射到硬件上，这应用于特定类的应用程序。这种方法例如 `STAPI`，它构建在编程语言之上，其中骨架被标记为接口，并选择变体（`variant`）运行在加速器上。`ADM` 系统可以简化程序其他部分与加速器之间的数据传输。

针对商用加速器的软件开发，如运行时管理库 [25] 或 NVIDIA `CUDA` [38]，要求程序员在使用这些系统执行任何计算之前，显式地定义数据移动和同步点。`OpenCL` 规范 [1] 同样使用了系统内不同处理器之间的显式数据传输。本文提出的编程模型消除了显式的……

![](img/03d0eb09047dbcab29ca9be26a1a08a3_369_0.png)

图 12. 使用不同内存模型和滚动尺寸的时间消耗

### 共享内存

存在硬件和软件 `DSM`（分布式共享内存）系统，它们在物理分布的机器之上实现了共享地址空间。本文提出的 `ADM` 系统为程序提供了共享地址空间的幻觉，然而，只有少数处理器可以直接访问共享空间，而其他处理器（例如 GPU 或加速器）只能访问显式移动到它们内存内存。这种差异要求 `ADM` 系统最小化不一致性。

硬件 `DSM` 系统实现了维护缓存一致性以及访问共享数据的必要逻辑。硬件 `DSM` 系统实现了基于失效（invalidation-based）的协议、基于释放（release-based）的粒度 [16, 18, 20, 23, 34]。还有方法实现数据复制 [10] 或支持一致性协议 [12]（后者将共享数据虚拟化）。在这项工作中，我们展示了一种基于软件的 `ADM` 实现，它实现了释放一致性（release consistency）[33] 并使用更大的粒度来最小化数据传输的开销。

软件 `DSM` 可以基于编译器或运行时系统。编译器 `DSM` 系统使用编程语言的注解来声明共享数据结构，并为每次对共享数据的访问生成同步和一致性代码 [3, 5]。本文提出的编程模型要求程序员显式地定义这些数据结构以及检测对共享数据访问、一致性或同步操作的机制。

运行时 `DSM` 实现需要 API 来获取共享数据结构。运行时系统使用内存保护硬件访问共享数据并执行必要的一致性和同步操作。运行时系统管理操作系统 [15, 17] 或作为用户级库 [8, 12, 13, 35] 来管理系统内存资源（例如在数据传输时阻塞进程），但需要更大的实现工作。

## 参考文献

- [1] The OpenCL Specification, 2009.

- [2] A. Agarwal, R. Bianchi, D. Chaiken, K. J. Johnson, D. Kranz., J. Kwiatkowski, B.-H. L. Kim, K. Mackenzie, and D. Young. The mit architecture and coherence in franca. In *ISA*, 95, 5–23, New York, NY, USA, 1995. ACM.

- [3] S. Ahuja, N. Carillo, and D. Geiderman. Introduction to jee. *IEEE Journal*, 9(8), 45–56, Aug. 2008.

- [4] P. An, J. Sula, S. Saiders, S. Smith, G. Thomas, N. Mato, and L. Rachwer. STAGNAP: A generic approach to C++. *IJCCAS*, 195–203.

- [5] H. Hell. Distributed programming with shared memory. In *IEEE Computer*, 31(8), 88–92, 1998.

- [6] K. J. Baker, K. Davis, A. Hoisie, D. J. Kerchman, M. Lang, and J. C. Santero. The architecture and performance of parallel programming system. In *SC '08*, 1–15, Piscataway, NY, 2008.

- [7] P. J. Sellers, M. R. Dijkstra, and J. Labella. A programming model for the cell in architecture. In *SC '06*, 96–85, New York, NY, USA, 2006.

- [8] B. Bershad, M. Meshczak, and W. Sawdon. The difficulty of shared memory in systems. In *Computer*, 93, 528–537, Feb 2000.

- [9] R. Bisian and A. Fornia. Multilarge framework for heterogeneous machines. *IEEE Transactions on Computers*, 37(8):930–945, Aug 1988.

- [10] R. Bisian and M. Wishankar. PLUSH: A shared-memory distributed programming framework. *ACM Graphics*, 18(2):115–120, 1995.

- [11] I. Buck. Using computing with NVIDIA. In *SIGGRAPH '07*, 46–6, New York, NY, USA, 2007. ACM.

- [12] J. J. Bert, K. Benner, and W. Weimelt. Modular design for parallel programming. In *SOOP '91*, 152–164, New York, NY, USA, 1991. ACM.

- [13] B.-C. Cheng and W. Wu. Modular hierarchical access protocols for parallel-processing systems. In *New York, NY, USA, 2006*, 497–506. IEEE.

- [14] J. Darlington, A. Field, P. G. Harris, H. J. Kelly, W. N. Sharp, and Q. Wu. Parallel programming using skeleton functions. In *PARLES '93*, 146–160, London, UK. 1993. Springer-Verlag.

- [15] P. Desjardins, J. Lebrun, R. Ma, and A. Ramachandran. Consistency models for shared-memory systems. *IEEE Transactions on Computers*, 24(14):2311–2344, nov 1995. IEEE.

- [16] G. Deli, S. Smith, and F. Terry. Analysis of an experiment-based approach to memory locking. In *SIGCOMM*, '88, 165–174, New York, NY, USA, 1988. ACM.

- [17] F. Blesch and G. Poock. Memory: A coherent shared memory design. In *OSP* '89*, 211–223, New York, NY, USA, 1989. IEEE.

- [18] S. Frank, I. Burhardt, and J. Rothie. The KSR 1: The

- [19] J. Huang, A. Kelim, R. Sy, S. Lam, N. Navarro, and W. Wu. CUDA: An architecture for processor-to-accelerator communication. In *OCS* '09*, 297–308, New York, NY, USA, 2008. ACM.

- [20] D. Johnson. The scalable cache interface, 12(1):10–22, 1992.

- [21] S. Hau, T. Ryu, W. Fry, M. H. Moller, and J. P. Kao. The chimaera configurable runtime. *IEEE Transactions on VLSI*, 12(2):206–217, 1994. IEEE.

- [22] J. R. Hauser and J. Wnerzyk. GRIPS: A processor model for reconfigurable processor. In *FCCM* '97, 12–21, Apr 1997. ACM.

- [23] M. Meinlich, J. Kusin, O. Petri, F. Heinlein, J. Baert, P. J. Singh, R. Simoni, G. Gharachloo, D. Nakashira, H. Horowitz, A. Gupta, M. Rosenberg, and J. Hendrickson. The performance impact of

## 7. 结论
