

![](img/ffb89ef8c668ade3e6e47a9ee7de70e5_250_0.png)

## 图 7.8 功率一致性的隶属函数

![](img/ffb89ef8c668ade3e6e47a9ee7de70e5_250_1.png)

## 图 7.9 输入空间获得的划分

![](img/ffb89ef8c668ade3e6e47a9ee7de70e5_251_0.png)

图 7.10 总工作量的隶属函数

![](img/ffb89ef8c668ade3e6e47a9ee7de70e5_251_1.png)

图 7.11 功率均匀性的隶属函数

## 7.7 参考文献

- [1] T. Takagi and M. Sugeno, “Fuzzy Identification of Systems and Its Applications to Modeling and Control”, IEEE Trans. on Syst., Man, and Cybern., Vol.15, No.1, pp.116–132, 1985.
- [2] S. Horikawa, T. Furuhashi and Y. Uchikawa, “On Fuzzy Modeling Using Fuzzy Neural Networks with the Back-Propagation Algorithm”, IEEE Trans. on Neural Networks, Vol.3, No.5, 801–806, 1992.
- [3] K. Tachibana and T. Furuhashi, “A Hierarchical Fuzzy Modeling Using Fuzzy Neural Networks which Enable Uneven Division of Input Space”, The 14th Fuzzy System Symposium, pp.305–308, 1998.
- [4] R. Smith and W. L. Spinks, “Discriminant Analysis of Biomechanical Differences between Novice, Good and Elite Rowers”, Journal of Sports Sciences, 13, pp.377–385, 1995.

## 8

## Hopfield 系数确定的新颖模糊方法

Salvatore Cavalieri
Institute of Informatic and Telecommunications, University of Catania, V.le A.Doria 6, 95125 Catania, Italy. E-mail: cavalieri@iit.unicit.it

Marco Russo
M.Russo is with INFN Section of Catania - ITALY and with the Dept. of Physics, Univ. of Messina, Contrada Papardo, Salita Sperone 31, 98166 ME - ITALY. E-mails: marco.russo@ai.unime.it, marco.russo@ct.infn.it, marco.russo@ieee.org

- Abstract.................................................... 242
- 8.1 Introduction............................................ 242
- 8.2 Hopfield-Type Neural Network................... 244
- 8.3 Fuzzy Logic ............................................ 245
- 8.4 The Fuzzy Tuning of Hopfield Coefficients................... 248
- A Detailed Description of the Algorithm for Coefficient Determination • Membership Function Tuning
- 8.5 Examples of Application of the Proposed Method ................... 258
- The Traveling Salesman Problem • Flexible Manufacturing System Performance Optimization
- 8.6 Remarks on the Tuning of the Parameters ................... 267
- 8.7 Description of the Fuzzy Inferences trained ................... 268
- 8.8 Fuzzy Approach versus Heuristic Determination of HCs ................... 270
- TSP by Hopfield and Tank's Original Energy Function • TSP by Szu's Energy Function • FMS Performance Optimization
- 8.9 Conclusions ................................... 275
- 8.10 References ................................... 276

## Hopfield 系数确定的新颖模糊方法

## 摘要

Hopfield 型神经模型是解决具有 NP-hard 计算复杂度的优化问题的合适工具。使用 Hopfield 模型解决此类问题需要确定与优化问题本身的周围条件相关的一定数量系数值。确定这些值相当困难，因为需要进行启发式搜索。这不仅耗时，而且可能导致确定一组系数，该系数提供的神经解远离最优，甚至是非法的。到目前为止，文献中尚未报道任何关于搜索系数的通用方法的研究，该方法将保证最优或接近最优的解。本章提出了一种方法，可以自动确定 Hopfield 系数。可获得的结果可以由用户定义。事实上，可以指定用户希望高质量的解，还是更喜欢更大的鲁棒性，即更高的有效解百分比。

### 8.1 引言

在文献中存在一类组合问题，由于需要探索所有可能的解，因此极其复杂。

因此通常更喜欢启发式解；尽管它们不总是保证最优解，但所涉及的计算时间有限。

Hopfield [1] 提出的自联想记忆模型作为解决困难优化问题的方法引起了相当大的兴趣。其特别能够在很短时间内解决 NP-hard 组合问题的能力，已导致 Hopfield 网络成功应用于大量实际问题 [2–8]。

许多研究人员研究了 Hopfield 网络用于解决优化问题的特性 [9,10]。通常发现，尽管这些网络确实产生了一些有用的结果，但一个很大的缺点是，在

取值范围在 0 到 1 之间，与同一神经元的输入 U_i 通过单调递增的 Sigmoid 函数 g_i 相关联。j-th 神经元输出与 i-th 神经元输入之间的每个反馈都有一个相关权重 w_ij，它决定了 j-th 神经元对 i-th 神经元的影响。然后向 i-th 神经元提供外部偏置电流 I_i。Hopfield 网络中第 i 个神经元 O_i 的动力学由以下描述：

```
dU_i/dt = -U_i/τ + Σ_j w_ij O_j + I_i  (8.1)
```

其中 τ 是用户选择的衰减常数。Hopfield [21] 证明了如果权重矩阵 W = [w_ij] 对称并且函数 g_i 是陡峭的曲线，则由 (8.1) 描述的神经元动力学遵循二次能量函数，也称为 Lyapunov 函数的梯度下降：

```
E = -1/2 Σ_{i,j} w_ij O_i O_j - Σ_i I_i O_i  (8.2)
```

在相同假设下，Hopfield [21] 证明了能量函数 (8.2) 的极小值与 O_i ∈ {0,1} 定义的超立方体的角点重合。

### 8.3 模糊逻辑

本节的目的是描述为自动修改 Hopfield 网络系数而训练模糊规则所采用的方法（见第 8.7 节）。

在经典集合论中，给定值 x ∈ X 和 X 的子集 A（A ⊆ X），元素 x 要么属于集合 A，要么不属于。因此可以为 X 的每个元素关联一个布尔数值（即属于集合 {0,1} 的值），指定其是否属于 A。

然而，人类的思维方式并不复制经典理论：在人类思维中，集合的轮廓要模糊得多。

例如，考虑一些常用的形容词，如高、聪明、疲倦、生病等，很明显它们的轮廓完全不清晰。问题在于我们不是以经典二值逻辑的术语来指代这些属性，而是以多值推广的术语来指代。

模糊集合的概念是这种推广的一步。如 Zadeh [22] 所引入，模糊集合是其隶属函数可以在闭区间 [0,1] ⊆ ℝ 内取任意值的集合。称为论域的模糊子集 A，具有隶属函数：

μ_A : X → [0, 1] (8.3)

它将 X 的每个元素 x 与一个介于 0 到 1 之间的数 μ_A(x) 相关联，表示 x 属于 A 的隶属程度。

一般来说，模糊条件规则由前提和结论组成：

if premise then conclusion (8.4)

前提由若干模糊谓词 P_i 组成（今后也称为前件），其一般形式为（Tom IS speed），最终被否定或由不同的算子如 AND 或 OR 组合，这些算子用 t-范数或 t-余范数计算（根据 Zadeh 分别是最小值和最大值）。

在后一个例子中，Tom 是在男性论域中定义的语言变量的值，speed 是语言变量的词集的名称之一（例如 slow, normal, speed）。

以下是使用此类算子的模糊条件规则示例：

if P₁ and P₂ or P₃ then P₄ (8.5)

其中，例如：

P₁=(car IS light),
P₂=(power IS medium),
P₃=(power IS high),
P₄=(car IS fast).

为了将推理方法应用于结论，首先需要通过评估每个谓词 P_i = (X_i IS A_i) 的隶属度 α_i 来评估前提的隶属度 θ。隶属度 α_i 是通过评估通用值 X_i 在模糊集 A_i 中的隶属度来计算的。如果 X_i 由模糊集组成，则其隶属度 α_i 是通过在 X_i 的模糊值与模糊集 A_i 之间进行交集并选择隶属度的最大值来确定的；如果 X_i 是精确值，则其在模糊集 A_i 中的隶属度由隶属函数在 X_i 处所取的值组成。因此，前提的隶属度 θ 可以通过对谓词进行模糊运算来计算。我们回顾，根据 Zadeh，算子 AND 对应于两个隶属度之间的最小运算，而 OR 对应于最大值。一旦知道 θ 的值，就可以应用推理方法来评估结论。

最后，获得输出模糊集后，进行去模糊化以将获得的模糊信息转换为数值。
