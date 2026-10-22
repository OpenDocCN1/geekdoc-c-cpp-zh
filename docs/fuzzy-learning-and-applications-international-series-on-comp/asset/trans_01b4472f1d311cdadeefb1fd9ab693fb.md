

## 8.8.2 基于 Szu 能量函数的 TSP

基于模糊逻辑的算法被应用于一个具有 15 个城市、城市间距离随机的 TSP 问题。

该场景中的最小距离为 0.05，因此 LowerBound 设为 0.75。Tolerance 设为 10，δ 设为 5，ε 设为 0.01。

IterDelta、IterMaxGood 和 PercIterMaxGood 的取值集合与 (8.26) 中所示相同。这样选择是为了评估 IterDelta 对解质量的影响，正如上一节所做的那样。

基于这组参数，模糊逻辑算法得到的 HC 如下：

```
HCs = { A = B = 317
        C = 888
        D = 766 } (8.31)
```

遗憾的是，文献 [5] 中 Szu 并未说明他在其能量函数中使用的 HC 集合。因此，我们无法像上一节中使用 Hopfield 和 Tank 的解那样，将利用 (8.31) 得到的解与 Szu 原始工作在相同场景下给出的解进行比较。两种方法的比较只能基于在具有特定城市数量的 TSP 中所获得的最优解百分比，因为 Szu 的工作 [5] 和文献 [35] 中仅提供了这一信息。

![](img/ffb89ef8c668ade3e6e47a9ee7de70e5_285_0.png)

## 图 8.12 解的质量

图 8.12 展示了使用系数集 (8.31) 所获得的最优解百分比，其中考虑了具有 5、10、15、20、25、30 和 40 个城市的 TSP。

如上一节所述，对每个 TSP（即每个城市数量）考虑了 10 个不同的随机距离场景，并且对每个距离场景找到了 10 个连续的神经解。对于每个 TSP，图 8.12 显示了在 10 次连续神经迭代中找到的最优解的平均百分比。由于 TSP 是一个 NP 难优化问题，对于城市数量大于 15 的非常复杂的问题，无法计算最优解。因此，对于城市数量大于 15 的 TSP，Hopfield 网络所提供解的优劣是根据观测到的最小路径长度来评估的，如文献 [36] 中所定义。

从图 8.12 可以看出，与图 8.11 中显示的值相比，现在最优解百分比的平均值更高，这凸显了能量函数所起的重要作用。

从图 8.12 可以清楚地看出，最优解百分比范围为 60% 到 90%，对于非常复杂的问题（20–40 个城市）也具有较高值。这是一个非常显著的结果，尤其是考虑到针对大型 TSP 所获得的高百分比值。对于类似的复杂问题，Szu 的方法很少能给出接近最优的解，如文献 [5] 和 [35] 所报告的那样。

## 8.8.3 FMS 性能优化

文献中没有任何关于使用 Hopfield 神经网络解决 FMS 性能优化问题的实例。因此，作者无法将使用模糊方法找到的系数所得到的神经解的性能，与使用其他系数集所得到的性能进行比较。可以说明的是，HC 值的选择非常困难。通过使用启发式方法（即手动改变系数），作者无法找到一组保证有效解的系数。而使用上一节所述的模糊方法，则能够确定一组保证高比例有效解的系数。找到的系数集为

```
HCs = { A = 80
B = 385
C = 295 } (8.32)
```

其中有效且最优解的比例可评估为约 25%。

## 8.9 结论

本章介绍了使用模糊推理来自动确定与待求解问题周围条件相关的能量函数系数。迄今为止，已知的调整方法只有手动启发式搜索，其本质上依赖于操作人员的经验知识。这种方法不仅非常耗时，而且不能保证最优解。事实上，所确定的系数集可能提供的解与问题的最优解相去甚远。

本章重点讨论了使用自动 HC 搜索算法实现两个不同目标的可能性。正如所强调的那样，实际上可以迫使自动搜索朝向提供鲁棒解或高质量解的系数。

这一特性特别有趣，因为它使我们能够满足使用优化方法时出现的不同需求。我们可以找到提供最优解的 HC，或者找到能够提供良好但质量不那么高的解、但计算开销较低的系数。

本章报道的结果有效地表明，所提出的方法的特点是搜索到的系数集能够保证有效解非常接近能量函数的全局最小值，或者保证非常鲁棒的解。所获得的鲁棒性和质量特征远高于经典启发式方法所提供的。

由于这种基于模糊逻辑的自动工具的内在特性，我们相信它极大地促进了 Hopfield 网络在求解非常复杂的优化问题中的实际应用。

*Networks*, vol. 7, no. 5, pp. 1272–1285, 1996.

[15] T.Yamakawa, “Stabilization of an Inverted Pendulum by a High-Speed Fuzzy Logic Controller Hardware System,” *Fuzzy Sets and Systems*, pp. 161–180, 1989.

[16] F.Beritelli, S.Casale, and M.Russo, “Robust Phase Reversal Tone Detection Using Soft Computing,” in *IEEE Proceedings of the Third International Symposium on Uncertainty Modeling Analysis and Annual Conference of the North American Fuzzy Information Processing Society, ISUMA-NAFIS ’95*, (College Park, Maryland, USA), pp. 589–594, Sept. 1995.

[17] M.Russo, *Metodi Hardware e Software per Logiche di Tipo non Tradizionale*. PhD thesis, University of Catania, Catania, Italy, Feb. 1996. Ph.D. thesis in Italian.

[18] V.Catania, N.Fiorito, M.Malgeri, and M.Russo, “A Framework for Codesign based on Fuzzy Logic and Genetic Algorithms,” in *Proceedings of the Eighth International Conference on Industrial and Engineering Applications of Artificial Intelligence and Expert Systems, IEA/AEI ’95*, (Melbourne, Australia), pp. 797–804, June 1995.

[19] M.A.Cohen and S.G.Grossberg, “Absolute Stability of Global Pattern Formation and Parallel Memory Storage by Competitive Neural Networks,” *IEEE Transactions on Systems, Man and Cybernetics*, vol. 13, pp. 915–926, 1983.

[20] R.Hecht and Nielsen, *Neurocomputing*. Reading, MA: Addison-Wesley, first ed., 1990.

[21] J.J.Hopfield, “Neurons with Graded Response Have Collective Computational Properties Like Those of Two-State Neurons,” in *National Academy of Science*, pp. 3088–2092, May 1984.

[22] L. A.Zadeh, “Fuzzy Sets,” *Information and Control*, pp. 338–353, 1965.

[23] Y.Lin and G.A.Cunningham III, “A New Approach to Fuzzy-Neural System Modeling,” *IEEE Transactions on Fuzzy Systems*, vol. 3, pp. 190–198, May 1995.

June 1996.
[28] S.Cavalieri, “Application of Neural Networks to Factory Automation Performance Optimization,” in *Computational Engineering in Systems Applications, CESA 96*, (Lille, France), pp. 240–245, June 1996.
[29] S.Cavalieri, “A Novel Neural Network Model for the Performance Evaluation of Flexible Manufacturing Systems,” in *22nd Annual International Conference on Industrial Applications, IECON96*, (Taipei, Taiwan), Aug. 1996.
[30] J.R.Pimentel, *Communication Networks for Manufacturing*. Prentice-Hall international Editors, 1990.
[31] J.H.P.Hillion, “Performance Evaluation of Job-Shop Systems using Timed Event Graphs,” *IEEE Transaction on Automatic Control*, vol. 34, no. 1, pp. 3–9, 1989.
[32] R.Zurawski, “Petri Nets and Industrial Application: A Tutorial,” *IEEE Transaction on Industrial Electronics*, vol. 41, no. 6, pp. 915–926, 1994.
[33] G.M.Ajmone, G.Conte, *Performance Models of Multiprocessor Systems*. Computer System Series, 1986.
[34] X.S.Lafti, J.M.Proth, “Optimization of Invariant Criteria for Event Graphs,” *IEEE Transaction on Automatic Control*, vol. 37, no. 5, pp. 547–555, 1992.
[35] NeuralWare, *Neural Computing: A Technology Handbook for Professional II/PLUS and NeuralWorks Explorer*, pp. 191–208. NeuralWare, Inc. Technical Publications Group, 202 Park West Drive, Pittsburg, PA 15275, USA: NeuralWare, Inc., 1995.
[36] E.Aarts and Jan Korst, *Simulated Annealing and Boltzmann Machines*, ch. 9, pp. 153–179. John Wiley & Sons, 1990.

