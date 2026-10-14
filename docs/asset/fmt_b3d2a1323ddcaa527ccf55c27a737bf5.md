
### 1. 概述

- 1. 首先，`Lp(ℝd)`（`1 ≤ p ≤ ∞`）连续嵌入 `S0'(ℝd)`；因此，对于这些函数空间中的任何一个（实际上，对于任何在平移和调制下等距不变的分布 Banach 空间），Fourier 变换都是良定义的，因为 `S0'(ℝᵈ)` 是该族中的最大空间。非常遗憾的是，众所周知的 `Lₚ` 空间在 Fourier 变换下表现不佳。这尤其是 Fourier 分析被视为分析学中一个非常深奥分支的原因之一；

- 2. 测试函数空间 `S0(ℝ)` 也与许多经典问题相关。它提供了理想的可和性核（summability kernels）储备库，所有已知的（好的）可和性核（Dirichlet 核除外）都属于 `S0(ℝ)`（参见 F. Weisz 的工作，例如 [47, 48]）；

- 3. 空间 `S0(ℝᵈ)` 也是 Poisson 公式成立的合适定义域，这一点已在 [49] 中得到证明；Y. Katznelson 的著作（[50]）以及后来在 [51] 中更全面地描述的唯一反例出现在 `S0(ℝᵈ)` “之外”，即在 `f` 和 `ˆf` 上的组合（弱）衰减条件不足以保证 `f ∈ S0(ℝᵈ)` 的情形，另见 [39]；

- 4. 从分布的观点来看，Poisson 公式等价于如下事实：作为 `S0'(ℝᵈ)` 的元素，Dirac 梳状函数 `Ш_Λ` 在（广义）Fourier 变换下映射到 `Ш_Λ⊥*`。因此，与 `Ш_Λ` 的点态乘法转化为与 `Ш_Λ⊥` 的卷积，而这等同于周期化。这是 Shannon 采样定理在 `Lᵖ` 空间背景下数学上严格证明的基础，而该定理又是数字信号处理的基石之一。它可用于解释为什么 CD 每秒存储 44100 个采样点，并且对（平滑）图像的子采样也有用；

- 5. 对于任意一对 `Lᵖ` 空间，平移不变算子空间可以用来自 `S0(ℝᵈ)` 的某些元素通过卷积来刻画，至少在它们作用于测试函数 `k ∈ S0(ℝᵈ)` 时是这样；

- 6. 这些卷积核或冲激响应分布显然具有 Fourier 变换，因此任何这样的算子都与一个传递函数唯一对应；

- 7. 核定理允许通过某个分布核 `σ ∈ S0'(ℝ²ᵈ)` 来描述从 `S0(ℝᵈ)` 到 `S0'(ℝᵈ)` 的任何算子（例如参见 [52, 38]）；

- 8. 还有进一步的表示，例如给定线性算子的扩展函数（spreading functions）或 Kohn–Nirenberg 符号，它们是分析给定算子（例如伪微分算子）性质的非常有用的方式。缓变算子理论可以用欠扩展算子（underspread operators）的概念很好地描述。这些算子可以粗略地描述为局部行为非常类似于卷积算子的线性算子，但其卷积核（或滑动平均剖面）在待平滑信号上移动时是缓慢变化的；

- 9. Banach Gelfand 三元组 `(S0, L², S0')(ℝᵈ)` 的分布框架对 Gabor 分析和时频分析非常有用，这些空间正是最先展现其有用性的领域。即使对于一般 `L²(ℝᵈ)` 函数的 Gabor 框架算子的描述，也只能给出一个从 `S0(ℝᵈ)` 到 `S0'(ℝᵈ)` 的有界算子，而要拥有所谓的“Bessel 族”，还需要对所使用窗函数提出额外性质，参见 [53, 46]；

- 10. 有许多充分的理由说明为什么应该只使用来自 `S0(ℝᵈ)` 的 Gabor 窗口（或 Gabor 原子）（在[39]中描述为调制空间 `M¹(ℝᵈ)`），其中之一是，对于一般格点，这保证了具有此类窗口的 Gabor 系统具有 Bessel 性质。这也是讨论抖动误差尤其是格点变化（[54, 55]）的基础；

- 11. Larsen 关于乘子的著作 [56] 使用由 Gaudry [57, 58, 59] 引入的准测度，描述了从 `Lᵖ(ℝᵈ)` 到 `Lᵠ(ℝᵈ)`（`1 ≤ p, q < ∞`）的卷积算子（以及相应的传递函数）。但准测度的（不受限的）全局结构（也可以等价地视该空间为 `ℱLₗₒc^∞(ℝᵈ)`）。空间 `S0(ℝᵈ)` 的引入帮助我们回到预期的表述：传递函数是冲激响应的傅里叶变换（反之亦然）；

- 12. L. Argabright 和 J. Gil de Lamadrid 提出了可变换测度理论，例如在他们的论文 [60, 61, 62] 中。这也可以在我们的背景下得到很好的处理。

- 13. 多维空间上测度的另一种推广是所谓的双测度（bimeasures），它们出现在以下论文 [63, 64, 65, 66, 67, 68, 69, 70, 71] 中。它们也能在我们的背景下找到自然的解释；

- 14. 除了确定性的函数与信号世界之外，随机信号处理中产生的问题也可以在 Banach Gelfand 三元组的背景下得到很好的处理。广义函数可以描述时间上的平均值，而随机过程则定义统计性质随时间的变化。因此，广义随机过程以统一的方式结合了这两个特征。下表概括了这一观点的要点。

| Toward Generalized Stochastic Processes |
|---|---|
| Ordinary Functions on `ℝᵈ` | Stochastic Processes on `ℝᵈ` |
| `ℝᵈ ↦ ℂ` | `ℝᵈ ↦ 𝔛` |
| `t ↦ f(t)` | `t ↦ X(t, ω) ∈ L²(Ω, Σ, P)` |
| Generalized Functions | Generalized Stochastic Processes |
| `C_c(ℝᵈ) ↦ ℂ` | `ρ : S0(ℝᵈ) ↦ 𝔛 : f ↦ ρ(f)` |
| `k ↦ σ(f) := ∫_{ℝᵈ} k(x)f(x)dx` | 例如，`f ↦ ∫_{ℝᵈ} X(t, ω)k(t)dt` |

让我们给出这方面的一些参考文献：[72]、[73]，最近的一篇综述见[74]，或[75]、[76]，特别是 P. Wahlberg 的论文：[77]、[78, 79, 80] 和 [81]。

### 1.13 总结

我们确信分布理论是信号处理任何数学基础的核心部分。毕竟，在几乎所有具体情况下，信号都是可测量的事物。物理过程并不太是数学意义上逐点（几乎处处）定义的函数，即使使用像 `$(L^2(\mathbb{R}^d),\|\cdot\|_2)$` 这样的函数空间建模能提供数学上令人满意的答案。但它是否真的能很好地描述例如用高质量麦克风录制的一段长音乐的实际物理现实呢？

在技术层面上，信号向量空间显然不仅仅是有限维的，因此不可能通过普通的线性代数（使用（有限）矩阵或所涉及函数空间的基）来描述例如线性系统。这再次表明需要使用（线性）泛函分析的方法，正如我们所看到的那样。我们重复提示：具体材料可以在 NuHAG 网页（`www.nuhag.eu`）上找到，进一步的材料也可以通过发送电子邮件至 `hans.feichtinger@univie.ac.at` 直接向作者索取。

基于这一认识，我们试图以近乎实用的方式勾勒出设计一门课程所需的要素，这门课程将为信号处理中出现的数学问题的进一步研究提供良好基础。

本着概念调和分析的精神，这种方法并不将考虑限制在通常使用“离散或连续”、“周期或非周期”* 等类别描述的一系列情境中，而是要求利用分布收敛对不同情境之间的转换进行数学上正确的描述。最有趣的方面与这样一个问题有关：如何基于 FFT，以数值方式近似计算光滑函数的普通（称为积分变换的）傅里叶变换。

我们预计，在未来几年中，利用各种函数空间范数（参见[82, 23]）来关注许多不同算子或过程的构造性实现的定量估计将变得重要。本章应鼓励读者思考总体背景，并找到一些建议，希望能帮助他们使用一套合适的工具，并为他们的学生为今后的此类任务做好准备。

在这个意义上，我们想向读者传达，调和分析不应被视为纯数学中一个抽象的、无生气的、也许是深奥的学科，在这个学科中很难找到有趣的数学问题，或者只能找到那些由早期数学家遗留下来的问题，或者需要重型工具的问题。相反，在线性代数方法、以 MATLAB® 等数值软件为支撑的系统性重新组合，加上良好的泛函分析基础（包括某些函数空间集合，主要是巴拿赫空间（根据我们的愿景）），很快就会引出许多有趣的问题，这些问题不仅具有数学挑战性，而且对应用科学家也很重要。

## 致谢

在撰写本章期间，作者先后在慕尼黑工业大学理论信息科学研究所（2018年春季）和捷克共和国布拉格查理大学数学研究所（2018年秋季）任职。

## 参考文献

- 1. H. G. Feichtinger. Banach Gelfand triples for applications in physics and engineering. Volume 1146 of AIP Conf. Proc., pages 189–228. Am. Inst. Phys., 2009.

- 2. L. Schwartz. Théorie des Distributions. (Distribution Theory). Nouveau Tirage. 1. Hermann, Paris, xii, 420p., 1957.

- 3. L. Hörmander. Linear Partial Differential Operators. 4th Printing. Springer, Berlin, Heidelberg, New York, 1976.

- 4. A. Weil. L'intégration dans les Groupes Topologiques et ses Applications. Hermann and Cie, Paris, 1940.

- 5. G. Cariolaro. Unified Signal Theory. Springer, London, 2011.

- 6. J. Cooley and J. W. Tukey. An algorithm for the machine calculation of complex Fourier series. Math. Comp., 19:297–301, 1965.

- 7. M. Frigo and S. Johnson. FFTW User's Manual. Massachusetts Institute of Technology, 1999.

- 8. N. Kaiblinger. Approximation of the Fourier transform and the dual Gabor window. J. Fourier Anal. Appl., 11(1):25–42, 2005.

- 9. H. G. Feichtinger and N. Kaiblinger. Quasi-interpolation in the Fourier algebra. J. Approx. Theory, 144(1):103–118, 2007.

- 10. R. P. Kanwal. Generalized Functions. Theory and Applications, 3rd Revised ed. Birkhäuser, MA, 2004.

- 11. A. Zygmund. Trigonometrical Series, 2nd ed. Dover Publications Inc., New York. 1955.

- 12. N. Wiener. Generalized harmonic analysis. Acta Math., 55(1):117–258, 1930.

- 13. N. Wiener. The Fourier Integral and Certain of Its Applications. Cambridge University Press, Cambridge, 1933.

- 14. Gröchenig, K., Y. Lyubarskii, and K. Seip, eds. Operator-Related Function Theory and Time-Frequency Analysis: The Abel Symposium 2012. Vol. 9. Springer, 2014.

- 15. H. Reiter. Classical Harmonic Analysis and Locally Compact Groups. Clarendon Press, Oxford, 1968.

- 16. H. Reiter and J. D. Stegeman. Classical Harmonic Analysis and Locally Compact Groups, 2nd ed. Clarendon Press, Oxford, 2000.

- 17. L. Loomis. The spectral characterization of a class of almost periodic functions. Ann. of Math. 72:362–368, 1960.

- 18. E. Hewitt and K. A. Ross. Abstract Harmonic Analysis I. Number 115 in Grundlehren Math. Wiss. Springer, Berlin, 1963.

- 19. E. Hewitt and K. A. Ross. Abstract Harmonic Analysis. Vol. II: Structure and Analysis for Compact Groups. Analysis on Locally Compact Abelian Groups. Springer, Berlin, Heidelberg, New York, 1970.

- 20. W. Kozek. On the transfer function calculus for underspread LTV channels. IEEE Trans. Signal Process., 45(1):219–223, January 1997.

- 21. M. Dörfler and B. Torresani. Representation of operators in the time-frequency domain and generalized Gabor multipliers. J. Fourier Anal. Appl., 16(2):261–293, 2010.

- 22. M. Dörfler and B. Torrésani. Representation of operators by sampling in the time-frequency domain. Sampl. Theory Signal Image Process., 10(1–2):171–190, 2011.

- 23. H. G. Feichtinger. Choosing Function Spaces in Harmonic Analysis. Volume 4 of The February Fourier Talks at the Norbert Wiener Center, Appl. Numer. Harmon. Anal., pages 65–101. Birkhäuser/ Springer, Cham, 2015.

- 24. H. G. Feichtinger. Thoughts on numerical and conceptual harmonic analysis. In A. Aldroubi, C. Cabrelli, S. Jaffard, and U. Molter, editors, New Trends in Applied Harmonic Analysis. Sparse Representations, Compressed Sensing, and Multifractal Analysis, Applied and Numerical Harmonic Analysis, pages 301–329. Birkhäuser, Cham, 301–329, 2016.

- 25. J. V. Fischer. On the duality of discrete and periodic functions. Mathematics, 3(2):299–318, 2015.

- 26. J. V. Fischer. On the duality of regular and local functions. Mathematics, 5(41), 2017.

- 27. J. Fischer. 傅里叶变换的四个特例。*Mathematics*, 12(6):335, 2018.

- 28. J. Horvath. *拓扑向量空间与分布*. 卷 I. Addison-Wesley, Reading, 1966.

- 29. F. Treves. *拓扑向量空间、分布与核*. 纯粹与应用数学第 25 号. Academic Press, New York, 1967.

- 30. A. H. Zemanian. *分布理论与变换分析. 广义函数导论及其应用. 重印，略有修正*. Dover Publications, Inc., New York, 1987.

- 31. E. Cordero, H. G. Feichtinger, and F. Luef. Banach Gelfand 三元组用于 Gabor 分析. In *伪微分算子*, volume 1949 of *数学讲义*, pages 1–33. Springer, Berlin, 2008.

- 32. H. G. Feichtinger, F. Luef, and T. Werther. 从线性代数到 Gabor 分析基础的引导之旅. In *Gabor 与小波框架*, volume 10 of *Lect. Notes Ser. Inst. Math. Sci. Natl. Univ. Singap.*, pages 1–49. World Sci. Publ., Hackensack, NJ, 2007.

- 33. H. G. Feichtinger, W. Kozek, and F. Luef. 有限阿贝尔群上的 Gabor 分析. *Appl. Comput. Harmon. Anal.*, 26(2):230–248, 2009.
