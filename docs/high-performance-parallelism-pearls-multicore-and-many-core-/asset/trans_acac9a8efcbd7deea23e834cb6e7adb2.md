

Advisor 以用户友好的视图显示编译器生成的优化信息，并在此基础上扩展了其他指标，包括循环 **trip counts**、CPU 时间、**memory access patterns**，以及针对优化的 **recommendations**。Vectorization Advisor 在应用于使用 Intel 编译器编译的用户应用程序时效率最高。然而，对于使用其他编译器构建的二进制文件，也可获得一部分指标。

Intel C++ 和 Fortran 编译器使用复杂的代码转换技术和静态架构分析来生成优化代码。优化引擎所做的决策通常不会考虑你正在开发的应用程序的运行时行为。这种缺乏运行时知识的一个后果是，生成的二进制文件可能运行不佳，除非你使用配置文件引导反馈机制。有了 Vectorization Advisor，我们无需使用配置文件引导反馈，并且可以获得交互式建议和丰富的动态二进制配置文件（甚至可以在多节点集群环境中获得）的优势。

Intel Vectorization Advisor Survey 功能通过结合静态和动态分析，以及嵌入编译器生成二进制文件中的优化信息，弥合了编译时决策与运行时行为之间的差距。

为了了解 SIMD 和线程并行潜力，通常需要了解循环“call counts”和“trip counts”（循环被调用的次数和循环体执行的次数）等知识。Advisor 技术使得能够使用“Trip Counts”功能获得这些信息。该功能依赖于对正在运行的应用程序进行动态检测；这种分析的一个副作用是，应用程序的运行速度会慢 2× 到 3×。

Advisor 技术平台的最后一个（但并非最不重要的）组成部分是一组 *memory profiling* 工具，使用条件内存访问 load 和 store 指令跟踪实现，提供了一种独特的 (a) 识别 Vectorized 和 Scalar 代码中使用的内存访问模式（MAP 功能）和 (b) 动态表征标量循环中的真实循环携带依赖关系（Loop Dependencies 功能）的能力。

## A LIFE CYCLE FOR EXPERIMENTATION

在尝试提高代码性能时，你几乎肯定会想尝试不同的“实验”。也许你会先在代码中添加一两个 pragma，然后也许会编辑代码以在已取得的成功基础上继续改进。经过一系列编辑和实验后，你甚至可能会决定回到原始代码并重新开始！

在进行此类实验时，我们建议你采用图 23.3 所示的生命周期。图中括号中显示的步骤是可选的。

- Profile & Diagnose
  - 首先，构建应用程序的 **optimized version**（即 Release Mode），同时记得使用 -g（Linux）或 /Zi（Windows）标志生成调试信息。构建应用程序后，后续步骤中通常应使用相同的二进制文件。
  - 运行 **Survey** 分析以查找热点。结果将包括每个循环运行所需的时间、任何编译器优化消息、使用的矢量化类型，以及在适当的情况下， advice 面板中的一个或多个建议。
- Analyze and Advise

![](img/16cb41208935c5f22dd1044f03f2e31b_495_0.png)

## FIGURE 23.3

A life cycle for experimentation.

- 可选地运行 **Trip Count** 分析以查看特定循环运行了多少次。
- 可选地运行 **Dependencies** 分析以查看是否存在任何循环携带依赖关系。
- 可选地运行 **Memory Access Patterns (MAP)** 分析以查看你的代码如何遍历内存。
- 对结果进行 **Snapshot**

Dependencies 分析和 MAP 分析用于对特定循环的工作原理进行“深入研究”。在运行分析之前，你必须首先选择感兴趣的循环——这可以很容易地从 Survey 结果窗口中完成。你还应尝试减少应用程序的工作量，因为这些步骤会显著增加运行时开销和内存使用量。最后，snapshot 会存储：

- Survey Report（包括 Trip Count）
- Refinement Reports（包括 Dependencies 和 MAP）
- 用户源代码的选择性快照
- 各种日志信息

这种生命周期的一个好处不仅在于你的分析结果保存在 snapshot 中，而且更重要的是，你所做的代码更改也被保存了。

## ANALYZING THE LATTICE BOLTZMANN CODE

图 23.4 显示了使用 Intel Advisor XE 的 vectorization advisor survey 功能对 DL_MESO 代码进行的初始分析。根据输入数据集的特征，例如流体数量或碰撞方案类型，热点的分布会显著变化。

热点的分布呈现“flat profile”模式，这对于物理模拟代码来说相当常见，并且包含大量热点，每个热点仅占时间的 3-5%。优化这种“平坦配置文件”的程序可能耗时，因为你必须单独分析并开发许多热点。

通常，当你开始任何优化工作时，你应该处理对运行时贡献最大的代码部分。那就是最大的热点，但在我们的例子中，我们选择按相反顺序进行，因为我们希望在章节中逐步引入 Vectorization Advisor 的不同功能。事实上，我们甚至跳过了 fGetSpeedSite 中的第三个热点，因为第四个热点更符合我们的目的。

在本章中，我们查看四个最热循环中的三个：

- lbpSUB:744 in fGetEquilibriumF 计算可压缩流体的平衡
- lbpGET:42 in fGetOneMassSite 计算质量密度
- lbpSUB:1247 in fPropogationSwap 将粒子移动到相邻网格点

## OPTIMIZING THE COMPUTE EQUILIBRIUM LOOP (lbpSUB:744)

在本节中，我们使用 Advisor Survey Analysis 查看 fGetEquilibriumF 中循环的构成部分，然后通过填充一些数据结构来修复矢量化效率低下的问题。

![](img/16cb41208935c5f22dd1044f03f2e31b_496_0.png)

FIGURE 23.4

The results of an initial analysis.

## FIGURE 23.6

Analysis results of the loop at line 744 of lbpSUB.cpp: body – peel – remainder break-down.

## Trip count analysis

分析循环时有用的另一条额外信息是循环体被迭代的确切次数以及循环被调用的次数。你可以使用 Vectorization Advisor 中的 Trip Count 分析来查找这些值。运行 Trip Count 分析时，应预期程序的运行速度比 Advisor Survey 慢两到三倍。

在我们给定的例子中，由于我们对代码有所了解，我们已经知道此循环的 Trip Count 为 19，但最好通过运行分析来检查 Trip Counts 和 Call Counts 数据。

## Fixing the problem

Scalar Remainder 是矢量化引入的不必要的开销，在我们的例子中，它约占循环总时间的 25%。这种剩余循环的存在对并行效率有不利影响——即可能实现的最高加速比。

## Note

你应该始终调查任何在标量、剩余或剥离循环中花费了循环运行时很大比例的代码——这表明矢量并行效率不是最优的，并且可能存在优化机会。

函数 fGetEquilibriumF 中较大的剩余“开销”实际上是由循环（trip）计数不是 Vector Length（VL）的倍数引起的。当编译器矢量化循环时，它会生成矢量化体，在我们的例子中，该体执行迭代 0–15。剩余的三个迭代，16–18，由标量剩余代码执行。

由于总循环计数相当小，因此剩余的三个迭代成为循环经过时间的重要部分。在理想优化的循环中，尤其是那些 trip count 较低的循环，不应存在剩余代码。

