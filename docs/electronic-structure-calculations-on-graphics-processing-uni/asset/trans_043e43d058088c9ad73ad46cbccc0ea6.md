

### 分析频率计算的耗时与加速比

![](img/255d48531d66773aa863436a333dac7d_140_0.png)

图 5.4 使用 B3LYP/TZ2P 和冻核设置“small”以及 ADF 中“good”的 Becke 网格质量，对布德索尼德分子（C$_{25}$H$_{34}$O$_4$）进行分析频率计算时黑森矩阵元素计算的耗时与加速比。

图 5.4 显示了使用 TZ2P 基组对布德索尼德分子（C$_{25}$H$_{34}$O$_4$）进行分析频率计算的耗时和加速比。使用了 GGA BLYP 泛函、冻核“small”设置以及 ADF 中“good”的 Becke 网格质量。该计算仅对 65 个原子中的 3 个进行，生成一个部分黑森矩阵，且图 5.4 仅显示了对原子核循环的耗时，因为该循环将占完整黑森矩阵总计算时间的 ~98%。因此，这些耗时对完整频率计算具有代表性。图 5.4 显示，仅使用 2 个 CPU 核心（每个 GPU 6 个 CPU 核心）时可实现 2.16x 加速比，使用 12 个 CPU 核心（每个 GPU 6 个核心）时可实现 1.70x 加速比。

频率代码中的计算采用与第 5.3.3 节中解释的相同的混合方案进行加速。唯一的区别是网格上数值积分与算子及基函数（导数）值计算之间的比率，对于 flu1_a1_gqa 例程约为 4:1。这给出了可能的 5 倍加速因子，与 flocky 例程相比略高。但是，共享一个 GPU 的 CPU 核心数量需要较低；否则，数值积分无法隐藏在 CPU 工作之后，从而降低可能的加速比。

flu1_a1_gqa 例程的耗时和加速比如图 5.5 所示。当仅使用两个 CPU 核心时，两个 GPU 上执行的所有数值积分工作都隐藏在其他 CPU 工作之后，从而实现 4.43x 加速比。预计的 5 倍可能加速比未能实现，原因是包装例程的开销增加，该例程在将数据发送到 GPU 之前会在 CPU 上重新排序输入数组。这是为了在数值积分内核中启用从全局内存进行合并数据读取所必需的，而使用 ADF 梯度代码中的当前数据结构，否则很难实现这一点。当使用 12 个 CPU 核心时，加速比降至 2.66x，表明当前 GPU 加速方案仍有改进空间。

将辅助矩阵方案引入 GPU 将是减少每个积分网格批次所需操作数量并同时解决数据结构问题的一个好方法。

### f1u1_ai_gaa 例程的耗时与加速比

![](img/255d48531d66773aa863436a333dac7d_141_0.png)

**图 5.5** 分析频率计算所需的 Fock 矩阵导数矩阵元素计算（例程 f1u1_ai_gaa）的耗时与加速比。测试系统为使用 B3LYP/TZ2P 和冻核设置“small”以及 ADF 中“good”的 Becke 网格质量的布德索尼德分子（C25H34O5）。

## 5.4 结论

ADF 软件包中使用 STO 实现的 DFT 计算，通过针对 Fock 矩阵元素数值积分的低延迟 CUDA 内核进行了加速，旨在为相对较小的问题规模获得良好性能。该内核在 Tesla Fermi 架构上实现了近 50% 的 DGEMM 性能（134 GFLOPS），并且具有足够的可移植性，在 K20 上运行速度快两倍（262 GFLOPS），在 K40 上快三倍（408 GFLOPS）。

开发了一种混合计算模型，将繁重的数值工作卸载到 GPU，同时保持 CPU 工作。如果每个 GPU 的 CPU 核心数量不过大，CPU 和 GPU 之间的工作负载平衡会使数值积分瓶颈消失。加速后的 ADF 代码在单点计算中显示出 1.45–1.89 倍的加速（取决于网格精度设置），在频率计算中显示出 1.70–2.16 倍的加速（取决于 CPU 核心与 GPU 设备的比例）。

像 ADF 这样拥有大量旧代码的软件包，GPU 加速可能是一个困难的目标，因为在合理的时间内无法将它们完全移植到 GPU。这里描述的混合方案可以成为此类情况的良好解决方案，在提供不错的加速比的同时，不牺牲使代码独特的任何功能。

ADF 中的 GPU 加速仍在进行中，有大量改进空间。在不久的将来，我们希望优化频率代码，并将加速扩展到超越 GGA 的泛函以及其他性质计算。

## 参考文献

- 1. Kohn, W., Becke, A.D. 和 Parr, R.G. (1996) 电子结构的密度泛函理论. Journal of Physical Chemistry A, 100 (31), 12974–12980.
- 2. Neese, F. (2009) 基于密度泛函理论的分子性质和分子光谱预测：从基本理论到交换耦合. Coordination Chemistry Reviews, 253 (5–6), 526–563.
- 3. Cohen, A.J., Mori-Sánchez, P. 和 Yang, W. (2012) 密度泛函理论面临的挑战. Chemical Reviews, 112 (1), 289–320.
- 4. Kutzelnigg, W. (2013) 高斯基组中的波函数展开。I. 局部与全局近似. International Journal of Quantum Chemistry, 113 (3), 203–217.
- 5. Güell, M., Luis, J.M., Solà, M. 和 Swart, M. (2008) 铁配合物自旋态能量学中基组的重要性. Journal of Physical Chemistry A, 112 (28), 6384–6391.
- 6. ADF2013, SCM, Theoretical Chemistry, Vrije Universiteit, Amsterdam, The Netherlands, http://www.scm.com (访问日期：2015 年 9 月 7 日).
- 7. Te Velde, G., Bickhaupt, F.M., Baerends, E.J. 等 (2001) 使用 ADF 进行化学研究. Journal of Computational Chemistry, 22 (9), 931–967.
- 8. Fonseca Guerra, C., Snijders, J., Te Velde, G. 和 Baerends, E. (1998) 迈向序列-N DFT 方法. Theoretical Chemistry Accounts, 99 (6), 391–403.
- 9. Atkins, P.J. (2004) 计算化学基础：理论与模型. John Wiley & Sons, 第 628 页.
- 10. Jensen, F. (2007) 计算化学导论，第 2 版. John Wiley & Sons, Chichester.
- 11. Fonseca Guerra, C., Visser, O., Snijders, J.G. te Velde, G. 和 Baerends, E.J. (1995) 阿姆斯特丹密度泛函程序的并行化. 在：计算化学的方法和技术，E. Clementi 和 C. Corongiu 编. 第 303–395 页，STEF, Cagliari. http://www.scm.com/Doc/metccc.pdf.
- 12. Wolf, S.K. (2005) 阿姆斯特丹密度泛函包中的解析二阶导数. International Journal of Quantum Chemistry, 104 (5), 645–659.
- 13. Nicu, V.P., Neugebauer, J., Wolff, S.K. 和 Baerends, E.J. (2008) 基于斯莱特型轨道密度泛函理论框架的振动圆二色性实现及其在六螺烯和七螺烯中的应用. Theoretical Chemistry Accounts, 119 (1-3), 245–263.
- 14. Franchini, M., Philipsen, P.H.T. 和 Visscher, L. (2013) 阿姆斯特丹密度泛函程序套件中的 Becke 模糊单元积分方案. Journal of Computational Chemistry, 34 (21), 1819–1827.
- 15. Volkov V. 2010 低占用率下的更好性能. GPU 技术会议论文集. GTC, http://people.cs.fsu.edu/~gerlebacher/gpus/better_performance_at_lower_occupancy_gtc2010_volkov.pdf.

## 6 大规模并行混合架构上的小波密度泛函理论

Luigi Genovese¹, Brice Videau², Damien Caliste¹, Jean-François Méhaut², Stefan Goedecker³ 和 Thierry Deutsch¹

¹Université Grenoble Alpes, INAC, F-38000 Grenoble, France, and CEA, INAC, F-38000 Grenoble, France
²Université Joseph Fourier – Laboratoire d’Informatique de Grenoble – INRIA, Grenoble, France
³Institut für Physik, Universität Basel, Basel, Switzerland

在本章中，我们描述了在 BigDFT 代码中实现的基于小波基组的密度泛函理论（DFT）计算的 GPU 加速。Daubechies 小波传统上未用于 DFT 计算，但我们展示了使它们既适用于精确又高效的 DFT 模拟的特性。在这里，我们解释了现有的 MPI 并行小波基 DFT 实现如何通过将数值密集型操作卸载到 GPU 来受益于 GPU 的计算能力。

### 6.1 关于密度泛函理论实现中小波基组的介绍性评论

量子力学和电磁学被广泛认为是通向材料和纳米系统“从头计算”方法的途径：给定适当的软件实现和足够强大的硬件，可以在不依赖任何可调参数的情况下计算性质。在 1980 年代，人们清楚地认识到，确实可以获得包括总能量、电子结构以及相关的动力学、介电、机械、磁性和振动性能在内的众多材料性质，其精度可被视为真正具有预测性。

