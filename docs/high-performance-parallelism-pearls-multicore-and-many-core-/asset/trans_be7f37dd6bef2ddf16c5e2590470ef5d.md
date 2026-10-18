

![](img/16cb41208935c5f22dd1044f03f2e31b_237_0.png)

## FIGURE 10.19

在 Intel Xeon Phi 协处理器上，不同嵌套并行方法在多种问题规模下的运行时间比较。

对于小规模问题，嵌套 OpenMP 区域与其他方法之间存在明显的性能差异。虽然使用热团队对性能有显著改善，但并不能完全消除所有线程创建/销毁开销——运行时仍必须遵守 OpenMP 语义（例如私有变量的数据移动），并且运行时必须能够处理在任何嵌套层级请求任意数量的线程。有趣的是，对于最大问题规模，不同方法之间的差距几乎缩小到零，因为开销能够被分摊到分配给每个线程的增加的工作量上。

Intel OpenMP 运行时还支持一个环境变量（KMP_BLOCKTIME），用于控制线程在 OpenMP 区域结束时在进入睡眠前自旋的时间。图 10.20 中的图表显示了热团队性能受该变量三个不同值的影响：200 ms（默认值）；0（导致线程立即睡眠并释放核心资源）；以及无限（导致线程无限自旋，确保在遇到下一个并行区域时保持唤醒）。由于我们预计会连续快速遇到多个并行区域，将阻塞时间设置为无限应产生最大效果，这在我们的结果中得到了体现。正确设置 KMP_BLOCKTIME 将嵌套并行区域与手动嵌套之间的性能差距缩小到 601 问题，速度提升 2×，但仍不足以挽救较小的问题规模。

图 10.21 中的表格从可用性和对程序员的友好性角度比较了不同的嵌套并行方法。由于这些指标并非客观，它们基于我们使用 miniModal 的经验得出的观点——读者完全可以不同意！我们认为目前最好的选择是本章介绍的手动嵌套方法，因为它达到了“最佳平衡点”，始终

在 OpenMP 规范迭代若干次之前，它才准备好用于生产代码。具体而言，无法为团队设置亲和性可能会对其他运行时的性能产生负面影响，而无法在目标区域之外使用团队则显著降低了其实用性。最后，根据我们的结果，很难推荐在没有热团队的情况下使用嵌套 OpenMP 并行区域！

## SUMMARY

在本章中，我们逐步介绍了对 miniModal 的一系列更改，miniModal 是 COSMOS 用于分析 CMB 辐射的 Modal3D 应用的代理代码。这些更改将性能提升了接近 100 倍，适用于 Intel Xeon 处理器和 Intel Xeon Phi 协处理器，并且 resulting 代码适合在由处理器、协处理器或两者组合构成的系统上运行。

本章中应用于优化代码的许多技术（例如负载平衡、缓存分块、调优预取距离）对任何高性能应用的开发者来说都应很熟悉，这进一步证明了“新异构”并行编程方法（即在异构系统上使用单一编程模型）的优势。然而，miniModal 最大的性能提升无疑来自于将 Intel MKL 中的三次样条积分例程替换为自定义数值积分例程，这凸显了分析和最终替换不合适的算法的必要性，使代码现代化并能够在宽 SIMD 向量和众多核心上扩展。

虽然高效的数值积分例程可能不直接适用于其他代码，但它完美地说明了依赖“黑盒”例程在所有情况下都表现最优的固有危险。通过使用嵌套并行性，我们的积分例程能够利用领域和硬件知识，在能够执行每个核心多个硬件线程的微架构上减少内存占用和不必要的缓存流量。此外，我们表明，与普遍看法相反，只要有足够的工作量来隐藏线程创建和销毁开销，纯基于 pragma 的实现可以与手动实现相匹配的性能。我们有信心，未来的 OpenMP 标准迭代和/或 Intel OpenMP 运行时的改进将能够进一步提高这些基于 pragma 解决方案的性能和可用性。

## FOR MORE INFORMATION

以下是我们推荐与本章相关的一些额外阅读材料：

- Fergusson, J.R., et al., 2010. General CMB and primordial bispectrum estimation: mode expansion, map making, and measures of F NL. Phys. Rev. D 82 (2), 023502.
- Fergusson, J.R., et al., 2007. Primordial non-Gaussianity and the CMB bispectrum. Phys. Rev. D 76 (8), 083523.
- Cosmic Microwave Background image. www.csa.int.
- Bispectrum integration domain image. Planck 2015 results. XVII. Constraints on primordial non-Gaussianity. http://arxiv.org/abs/1502.01592.
- OpenMP 4.0 Application Program Interface Version 4.0. http://www.openmp.org/mp-documents/OpenMP4.0.0.pdf.
- Dempsey, J., 2014. Plesiochronous phasing barriers. In: High Performance Parallelism Pearls: Multicore and Many-Core Programming Approaches. Morgan Kaufmann, Waltham, MA, pp. 87-115.
- Speedometer. https://01.org/simple-performance-tools
- The Stephen Hawking Centre for Theoretical Cosmology. http://www.ctc.cam.ac.uk/

下载本章及其他章节的代码。 http://lotsof cores.com.

## VISUAL SEARCH OPTIMIZATION 11

Prashanth Thinakaran*, Diana Guttman*, Mahmut Taylan Kandemir*, Meenakshi Arunachalam†, Rahul Khanna†, Praveen Yedlapalli*, Narayan Ranganathan†

Pennsylvania State University, USA* Intel Corporation, USA†

我们正处于数字数据呈指数级增长的时代，数据形式为文本、图像和视频，通过多个渠道产生，其中这些数据的实时分析正成为更大的挑战。由于这些基于分析的应用具有固有的数据级并行性，像 Intel® Xeon Phi™ 协处理器这样具有多个 SIMD 核心的计算加速器，通过满足这些应用的实时需求来提供帮助。

图像匹配是一个重要的应用，其中一组图像与大型图像数据库进行比较以寻找特征相似性。图像匹配有许多应用。许多多媒体系统，如互联网搜索引擎、多媒体内容分析软件和图像数据库分类工具，都将图像匹配用作中间步骤，使其成为性能和功耗优化的关键目标。

现有关于图像匹配的研究主要集中在探索算法技术和处理实时处理约束。随着新兴的架构趋势，例如多核协处理器、非易失性存储器和 3D 堆叠，研究图像匹配应用对这些计算平台的影响变得越来越重要。需要调查的关键问题包括：（1）图像映射应用表现出的不同类型的并行性；（2）这些应用映射到多核协处理器时如何扩展；（3）它们是否需要定制的代码并行化技术和/或数据布局优化以利用多核特定特性，例如多个内存通道、片上网络和宽 SIMD 单元；（4）鉴于 Intel Xeon Phi 协处理器计算核心上 GDDR 内存提供的高内存带宽，加速内核是数据并行的，它们能否利用 3D 堆叠和非易失性存储器。

本章主要关注前两个问题，并代表了理解特定图像匹配应用（面部检测和识别的机器感知）行为迈出的一步，通过研究其在基于 Intel Xeon Phi 协处理器的系统上映射时的性能。

在本章中，我们提出了一个客户端-服务器应用，用于使用快速近似最近邻库（FLANN）作为底层搜索算法对给定数据集执行图像分类。我们讨论了该应用在协处理器平台上的不同并行化技术。特别是，研究了三个重要参数（DBThreads、FLANNThreads 和 K 维（KD）树）对性能的影响。在协处理器系统上使用三个不同数据库展示实验结果。我们的结果表明，虽然树创建

