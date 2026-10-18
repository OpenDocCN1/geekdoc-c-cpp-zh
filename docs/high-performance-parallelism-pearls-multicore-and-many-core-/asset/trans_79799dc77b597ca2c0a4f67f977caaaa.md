

分析此基准测试中的 Triad 内核性能，该内核执行了 Copy、Scale 和 Add 内核操作的组合。

## SMITH-WATERMAN

Smith-Waterman 算法执行局部序列比对，用于确定两个字符串之间的相似区域，并在基因组应用中用于找出核苷酸或氨基酸序列之间的结构或功能相似性。

在本研究中，我们使用了一段高度优化的代码，该代码使用内在函数充分利用协处理器的向量单元。这些内在函数特定于首次出现在 Intel Xeon Phi 协处理器上的 512 位宽向量；我们的内在函数应可轻松适配支持 AVX-512 的 Intel Xeon Phi 处理器（Knights Landing）和支持 AVX-512 的 Intel Xeon 处理器（Skylake）。该应用的两个热点循环位于 `SmithWatermanMIC()` 中 `SmithWaterman.cpp` 的 Smith-Waterman 源代码中大约第 134 行和第 148 行。

## SHOC MD

SHOC 基准测试套件中的 MD 基准测试是一个基于 Lennard-Jones 势的分子动力学内核。它通过迭代更新系统中的所有力来模拟附近原子或分子之间的相互作用。

该应用的内核为 `compute_lj_force()`，位于 MD.cpp 中。该函数的精简版本显示在图 21.4 中。

注意该函数中的三个嵌套循环。最外层的循环（k）运行模拟参数所需的迭代次数。下一个内层循环（i）遍历原子，最内层的循环（j）遍历每个原子的邻居。在此循环的主体中，基于原子与其邻居之间的距离计算每个原子上的力。

请注意，邻居位置的值（`jposx`、`jposy`、`jposz`）来自 *间接数组访问*，即使用第二个“索引数组”（`neighList[]`）的值作为 `position[]` 数组的索引。这意味着 `position[]` 的元素不一定按顺序访问；访问顺序取决于 `neighList[]` 中的值。因此，编译器很难预测预取的内存访问模式。

在每次迭代中，都会访问 `position[neighList[j + i * maxNeighbors]]` 处的值。这需要两次内存访问，首先获取本次迭代的 `neighList[]` 值，然后使用该值作为索引进行第二次对数组 `position[]` 的内存访问。如果对该数组的访问遵循顺序或步长模式，则很容易预测。然而，由于此代码使用索引数组，访问模式由 `neighList[]` 中的值决定。索引数组问题的示意图显示在图 21.5 中。手动预取这些位置可以帮助将内存访问的延迟与之前迭代的计算重叠。

## TUNING PREFETCHING

在以下各节中，我们演示了使用三个示例应用调优预取的策略。调优应用的第一步应是确定占用大部分运行时间的热点函数或循环。此分析可使用 Intel® VTune™ Amplifier 等工具为处理器和协处理器提供。

![](img/16cb41208935c5f22dd1044f03f2e31b_457_0.png)

## FIGURE 21.5

使用索引数组对数据数组进行间接访问可能导致不可预测的访问模式。

## PREFETCH DISTANCE TUNING ON THE COPROCESSOR

一个关键的成功参数是预取“距离”，即在数据使用之前我们提前多少次迭代发出预取指令。要检查编译器自动使用的预取距离，我们可以使用编译器优化报告。循环优化是使用 -qopt-report-phase=loop 编译器选项生成的（Intel C Compiler 2015）。要生成最高级别的详细信息，我们使用选项 -qopt-report=5。

有时手动调优预取距离比依赖编译器确定它更有用。这是通过使用 -qopt-prefetch-distance=n1,n2 编译器选项完成的。n1 表示从内存预取到 L2 的距离，而 n2 表示从 L2 预取到 L1 的距离。要为单个循环调优距离，可以使用编译器指令 #pragma prefetch var: hint:distance。

## RESULTS—PREFETCH TUNING EXAMPLES ON A COPROCESSOR

使用 Stream Triad、Smith-Waterman 和 MD 作为示例，我们将展示如何调优软件预取以提高协处理器上的性能。

## PREFETCHING METRICS FOR STREAM TRIAD

为了说明预取如何影响性能，我们可以查看硬件性能计数器，这些计数器可以使用 Intel VTune Amplifier 收集。我们使用这些计数器的值来开发预取有效性的两个低级指标：覆盖率和效率。有用的预取是在程序的关键路径上消除未命中，通过在数据使用之前将其带入缓存。

覆盖率衡量预取在执行中替换需求未命中的程度，这应带来更高的性能。换句话说，完美的覆盖率意味着所有使用的数据都被预取到缓存中，程序没有经历未命中（除预取外）。覆盖率计算如下：

Coverage = (MissesNoPrefetching − MissesWithPrefetching) / MissesNoPrefetching = SavedMisses / TotalMisses

效率衡量预取的成本。如果发出大量无用的预取，预取的成本可能会超过收益。效率也会影响性能，因为大量无用的预取可能会污染缓存并浪费内存带宽。我们按如下方式计算实际有益的预取百分比：

$$\text{Efficiency} = \frac{\text{Misses}_{\text{NoPrefetching}} - \text{Misses}_{\text{WithPrefetching}}}{\text{TotalPrefetches}} = \frac{\text{Good Prefetches}}{\text{TotalPrefetches}}$$

有关如何使用硬件事件计数器计算这些指标的更多详细信息，请参阅有用协处理器硬件事件计数器部分。

我们在 Intel Xeon Phi 协处理器上测量了 Stream 的性能，并使用 VTune 收集了硬件事件计数器。为了比较预取的性能，我们多次运行应用程序，并启用或禁用不同的预取器。请注意，软件预取只能通过重新编译源代码来禁用。三种预取设置组合下的总未命中数和 resulting 性能显示在图 21.6 中。请注意，“无预取”不是现实的设置，因为很难禁用硬件预取，并且禁用所有预取会导致大多数工作负载性能不佳。在这里，我们将其用于比较以显示预取的好处。在大多数系统中，应保持硬件预取开启。

与无预取相比，硬件预取将性能提高了 6.8×，而硬件和软件预取的组合将性能提高了近 9×。在硬件预取始终启用的更现实的设置中，硬件和软件预取的组合比单独使用软件预取提高了 1.3×。

两种启用预取的配置下每种类型的预取次数显示在图 21.7 中。仅硬件情况下的少量软件预取来自相关代码（如库）中已存在的预取，而不是来自编译器。请注意，在组合情况下，即使硬件预取器已启用，已发出的硬件预取也少得多。这是因为硬件预取器不会对其训练在已被软件预取过滤掉的未命中流上。

![](img/16cb41208935c5f22dd1044f03f2e31b_458_0.png)

## FIGURE 21.6

在协处理器上使用三种预取配置实现的总未命中数和性能。每个配置的结果都是通过多次运行应用程序并启用或禁用每种类型的预取获得的。

