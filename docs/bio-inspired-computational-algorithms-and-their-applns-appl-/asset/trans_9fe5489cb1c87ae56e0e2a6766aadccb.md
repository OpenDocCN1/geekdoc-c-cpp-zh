
突变率。通常，但并非总是如此，突变会翻转单个位。事实上，与此相反，GenJam 的突变算子比翻转一位更为复杂。它们采用了几种标准的旋律发展技术，例如移调、倒行、旋转、反转、排序和倒行-反转。因为这些算子在音乐上都有意义，所以它们在事件层面上操作，而非在单个位上（Biles, 2001）。

### 4.4 替换

经过选择、交叉和突变过程后，当前种群将被新种群取代。每代中成功的个体更有可能在下一代中存活，而不成功的个体则不太可能存活。在我们的 GA 中，我们使用增量替换方法（参见 Beasley 等，1993），即只有适应度值优于当前个体的新个体才会被替换。因此，适应度最好的个体始终保留在种群中。

### 4.5 终止

一般而言，遗传算法在达到指定代数或适应度值收敛后终止。我们的 GA 在最佳解在 100 次迭代中没有改进时终止。

## 5. 混合 Benders/遗传算法

混合整数线性问题 Benders 分区算法的基本思想是将原问题分解为纯整数主问题和一个或多个连续变量的子问题，然后在这两个问题之间迭代。如果主问题的最优解的目标函数值等于子问题的目标函数值，则算法以原混合整数问题的最优解终止。否则，我们一次向主问题添加一个约束，称为 Benders 割，并重复求解，直到满足终止条件为止。这种分解的主要困难在于主问题的求解，这是一个“困难”的问题，计算成本高。

对于所研究的 CPL 问题，约束仅在子问题中明确，而主问题没有明确的约束。因此，主问题更适合用 GA 求解。

Lai 等（2010）引入了一种混合 Benders/遗传算法，这是一种 Benders 算法的变体，使用遗传算法为得到“良好”的子问题解提供主问题。Lai 和 Sohn（2011）进行了一项研究，将混合 Benders/遗传算法应用于车辆路径问题。下面是对混合算法的详细描述，并如图 1 所示。

- 1. **初始化。** 我们将迭代计数器 k 初始化为零，选择二进制变量向量 Y 的初始试验值，该向量用于选择要开放的工厂。
- 2. **原问题子系统。** 我们通过求解一个可行域与 Y 无关的运输线性规划问题来评估 r(Y) 的值。

Step 3. 生成 Benders 割。我们使用运输子问题的对偶解计算新的线性支撑，并将 k 增加 1。

Step 4. 通过 GA 的原问题主系统。要计算的试验选址方案 Y 是通过实现一个 GA 来计算的，其解同时提供一个可行的投资计划和等价程序最小成本的下界。

4a. 初始化。我们将变量 Y 初始化为二进制位串，其中位置 #i 对应工厂 #i。我们生成初始种群并同样对其适应度函数进行评估。

4b. 遗传操作。我们执行标准的单点交叉方法。还执行突变操作以保证种群的多样性。当前种群通过增量替换方法被新种群取代。

4c. 终止。如果在 100 次迭代内没有改进，我们终止 GA。

![](img/b6b7f8aebd1f88cc16a4011cc646fc4d_423_0.png)

Fig. 1. 混合 Benders/遗传算法的流程图

这种混合算法将避免其他传统搜索方法，即用于主问题的分支定界。它将以并行方式搜索解空间并利用适应度函数的“易于”评估。

## 6. 示例

为了说明前面章节讨论的混合算法，我们使用一个随机生成的包含 20 个工厂选址和 50 个客户的问题。五十个点在一个正方形区域内

![](img/b6b7f8aebd1f88cc16a4011cc646fc4d_425_0.png)

Fig. 3. Benders 算法（BD-Opt）提供的上界和下界。

![](img/b6b7f8aebd1f88cc16a4011cc646fc4d_425_1.png)

Fig. 4. Benders 算法（BD-Opt）找到的当前解。

最后，算法再次重启，50 个试验解由子问题评估，这次使用遗传算法，以便主问题再次被子优化以生成试验解。每个主问题在找到 40 个优于当前解的试验解后终止（或在最多 100 代后），此时所有优于当前解的解都会被评估。（在每个子问题之后，试验解使用更新的主问题成本函数，v̂(Y)，重新评估，只有成本小于当前解的解才会被子问题评估。）

![](img/b6b7f8aebd1f88cc16a4011cc646fc4d_426_0.png)

![](img/b6b7f8aebd1f88cc16a4011cc646fc4d_426_1.png)

![](img/b6b7f8aebd1f88cc16a4011cc646fc4d_427_0.png)

Fig. 7. Benders 算法（混合 BD/GA）变体 3 的当前解 试验 1。

![](img/b6b7f8aebd1f88cc16a4011cc646fc4d_427_1.png)

Fig. 8. Benders 算法（混合 BD/GA）变体 3 的当前解 试验 2。

在这种情况下，生成 50 个试验解仅需要 7 个主问题。（使用了规模为 50 的种群，交叉概率为 75%，突变概率为 1%。）

Canadian Journal of Operational Research and Information Processing, Vol. 37, pp. 194-225.

Geoffrion, A. M. & Graves, G.W. (1974). 用 Benders 分解进行多商品配送系统设计。 Management science, Vol. 20, No. 5, pp. 822-844.

Goldberg, D. E. (1989). 遗传算法在搜索、优化和机器学习中的应用, Addison-Wesley Professional, ISBN 978-0201157673, Boston, MA, USA.

Goldberg, D. E. & Lingle, R. J. (1985). 等位基因、基因座与旅行商问题, Proceedings of the 1st International Conference on Genetic Algorithms, pp. 154-159, ISBN 0-8058-0426-9, Pittsburgh, PA, USA, July, 1985.

He, S.; Chaudhry, S. & Chaudhry, P. (2003). 使用遗传算法求解一类设施选址问题。 Expert Systems, Vol. 20, No. 2, pp. 86-91.

Heragu, S. S. & Chen, J. (1998). 单元制造系统设计的优化解：Benders 分解方法。 European journal of operational research, Vol. 107, pp. 175-192.

Holland, J. H. (1992). 自然与人工系统中的适应：生物学、控制和人工智能应用的初步分析, A Bradford Book, ISBN 978-0262518110, Cambridge, MA, USA

Holmberg, K. & Ling, J. (1997). 阶梯成本设施选址问题的拉格朗日启发式方法。 European journal of operational research, Vol. 97, No. 1, pp. 63-74.

Kennington, J. L. & Whitler J. E. (1999). 优化电信网络备用容量的高效分解算法。 INFORMS Journal on computing, Vol. 11, No. 2, pp. 149-160.

Kershenbaum, A. (1997). 遗传算法何时效果最佳。 INFORMS Journal on computing, Vol. 9, No. 3, pp. 254-255.

Kim, H.; Sohn, H. & Bricker, D.L. (2011). 使用 Benders 分解和广义网络的发电扩建规划。 International Journal of Industrial Engineering, Vol. 18, No. 1, pp. 25-39.

Kratica, J.; Tosic, D.; Filipovic, V. & Ljubic, I. (2001). 用遗传算法求解简单工厂选址问题。 RAIRO Operations Research, Vol. 35, pp. 127-142.

Levine, D. (1997). 遗传算法：实践者的观点。 INFORMS Journal on computing, Vol. 9, No. 3, pp. 256-259.

Lai, M.; Sohn, H.; Tseng, T. & Chiang, C. (2010). 容量受限工厂选址问题的混合算法。 Expert Systems with Applications, Vol. 37, pp. 8599-8605.

Lai, M. & Sohn, H. 车辆路径问题的混合算法。 (2011) working paper.

Liepins, G. E. & Hilliard, M. R. (1989). 遗传算法：基础与应用。 Annals of operations research, Vol. 21, pp. 31-58.

Michalewicz, Z. (1998). 遗传算法 + 数据结构 = 进化程序, Springer, ISBN 978-3540606765, New York, USA

Oliver, I. M.; Smith, D. J. & Holland, J. R. (1987). 旅行商问题上置换交叉算子的研究。 Proceedings of the 2nd International Conference on Genetic Algorithms, pp. 224-230, ISBN 0-8058-0158-8, Hillsdale, NJ, USA, July, 1985.

Randazzo, C.; Luna, H. & Mahey, P. (2001). 双技术本地接入网络设计的 Benders 分解。 Discrete mathematics and theoretical computer science, Vol. 4, pp. 235-246.
