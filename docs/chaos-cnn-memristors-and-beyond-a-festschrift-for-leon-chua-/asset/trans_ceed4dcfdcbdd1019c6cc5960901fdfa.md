

![](img/039e7d3c23390584a66737067db8b75b_111_0.png)

图 10. 参数 $A_{st}=0.05$, $\tau=0.5$ 时网络中建立的体制：(a) 突触激活的时空图；(b) 突触的实现；(c) 神经元的实现。

network. 然而，平均而言，神经元网络的激活也发生在时间尺度 $T_1$ 的倍数时刻。

第二种可能的体制如图 10 所示。我们看到，该体制下突触激活的时空有序性（见图 10(a),(b)）与 CA 的吸引子 $A_1$ 的情况有很好的一致性。从图 10(c) 也可以得到，神经元放电的顺序与通过突触 CA 方法得到的结果完全一致。

吸引子 $A_1$ 定义了放电模式 $1 \to 2 \to 3,4$ 等，而吸引子 $A_2$ 则定义了放电模式 $1 \to 2 \to 4 \to 3$ 等。将结果与对原始网络的直接数值研究进行比较表明，CA 能够很好地描述网络的时空动力学（突触激活顺序和神经元放电顺序）。

## 6. 结论

我们给出了将突触 CA 方法应用于由四个 Morris-Lecar 神经元通过具有短期可塑性的化学突触耦合而成的兴奋性神经网络的一个例子。已表明，对应的 CA 具有两个非平凡的吸引子——$A_1$ 和 $A_2$。它们对应于网络突触激活的不同情景，从而定义了神经元的不同放电模式。

## 致谢

本工作得到俄罗斯联邦教育部和科学部政府合同 No. 14.740.11.0348 的资助，俄罗斯基础研究基金会资助项目编号 10-02-00643、12-02-00526，部分得到俄罗斯联邦政府拨款 No. 11.G34.31.0057 的支持，并得到 LATNA 实验室、俄罗斯高等经济大学国家研究大学的支持。

## 参考文献

[1] E.R. Kandel, J.H. Schwartz, T.H. Jessell, *Principles of neural science.* (Prentice-Hall Int. Inc., London, 1991).

[2] D. Terman, S. Ahn, X. Wang, W. Just, Reducing neuronal networks to discrete dynamics, *Physica D* **237** (3), 324–338, (2008).

[3] W. Just, S. Ahn, D. Terman, Minimal attractors in digraph system models of neuronal networks, *Physica D* **237** (24), 3186–3196, (2008).

[4] S. Ahn, B.H. Smith, A. Borisyuk, D. Terman, Analyzing neuronal networks using discrete-time dynamics, *Physica D* **239** (9), 515–528, (2010).

[5] E. Izhikevich, *Dynamical systems in neuroscience.* (MIT Press, Cambridge, MA, 2007).

[6] C. Morris, H. Lecar, Voltage oscillations in the barnacle giant muscle fiber, *Biophys. J.* **35** (1), 193–213, (1981).

[7] R.S. Zucker, W.G. Regehr, Short-term synaptic plasticity, *Annu. Rev. Physiol.* **64**, 355–405, (2002).

[8] V. I. Nekorkin, A. S. Dmitrichev, D. V. Kasatkin, V. S. Afraimovich, Relating the sequential dynamics of excitatory neural networks to synaptic cellular automata, *Chaos* **21** (4), 043124-1–13, (2011).

[9] M. W. Hirsch, C. C. Pugh, M. Shub, *Invariant manifolds. Lecture Notes in Mathematics.* (Springer-Verlag, 1977).

## 第 8 章：沃尔夫拉姆细胞自动机的动力系统视角

M. COURBAGE

*Laboratoire Matière et Systèmes Complexes (MSC),*
*UMR 7057 CNRS and Université Paris 7 — Denis Diderot,*
*Case 7056, Bâtiment Condorcet, 10, rue Alice Domon et Léonie Duquet 75205 Paris Cedex 13, France*
*maurice.courbage@univ-paris-diderot.fr*

B. KAMINSKI

*Faculty of Mathematics and Computer Science,*
*Nicolaus Copernicus University,*
*Chopina 12/18, 87-100 Torun, Poland*
*bkam@mat.uni.torun.pl*

Leon Chua 遵循 Wolfram 的做法，致力于从非线性动力学家的角度深入理解所有一维初等细胞自动机规则所蕴含的复杂性财富。在此，我们通过动力系统视角来完善这一观点，将其扩展到无限多个位点的极限。

- 1. Chua Odyssey Through Cellular Automata ........................................ 101
- 2. Cellular Automata as Dynamical Systems .......................................... 102
- 3. Instability, Invariant Measures and Entropy ...................................... 104
- 4. Cellular Automata as Space-time Dynamical Systems .............................. 106
- References ........................................................................ 107

### 1. Chua Odyssey Through Cellular Automata

八十年代，关于一维细胞自动机的一般理论写了许多论文。但由于局部规则数量众多以及长期行为类型繁多，需要进行特殊的分类工作，以便更清晰地看清这一丛林。Wolfram [21] 尝试了这种动力学分类，并对范围为

r = 1 且字母表为两态的 256 条规则进行了首次系统研究，也称为初等细胞自动机 (ECA)。与自旋系统的统计力学类似，位点数应趋于无穷大。

不久之后，拓扑和遍历动力系统领域的许多论文开始出现，关注一般和抽象性质，并以案例研究为例。

坚持具体观点，Leon Chua [2] 从非线性动力学的角度重新研究了这 256 条规则中的每一条，其中自动机作用于有限环。通过对称性和引入新标准，他筛选了每条规则，以便整体理解这一族。

Chua 研究了作用于圆 $C_l$ 上的有限词（在 Chua 语言中称为“位串”）的 1-D Wolfram 细胞自动机，其中 $C_l$ 的长度为 $l$，即整数模 $l$ 的环，$(\mathbb{Z}/l\mathbb{Z})$。它们是有限动力系统 $X = (X, f)$，使得构型空间 $X = S^{C_l}$，$S = \{0,1\}$ 且 $f : X \to X$ 是一个变换，定义为

$(fx)_n = F(x_{n-r},\ldots,x_{n+r})$,
$x = (x_i) \in X$, $n \in C_l$.

$F$ 称为局部规则，$r$ 称为细胞自动机映射 $f$ 的范围。在 $r = 1$ 的情况下，有 256 种可能的规则，使用众所周知的二进制 Wolfram 编号进行编号。除了 $f$ 之外，考虑左移变换 $\sigma : X \to X$ 定义如下。

$(\sigma x)_n = x_{n+1}$,   $x \in X$,  $n \in C_l$.

研究每条规则的吸引子时，Chua 观察到，在一类较大的规则中，动力学映射 $f^n$ 最终表现为一个移位 $\sigma$，或更一般地表现为 $k$ 步移位 $\sigma^k$。他称此类规则为 Bernoulli 移位。这种研究遇到了 [5,8,9] 中关于 $\mathbb{Z}$ 上细胞自动机中行波存在性的另一项研究，其中一种方法允许识别那些初始构型 $x \in S^{\mathbb{Z}}$ 使得 $f(x) = \sigma^k(x)$，表明这些构型对所有大于 $r$ 的 $k$ 都是空间周期性的。当 $k \le r$ 时存在许多非周期行波 [20]。利用 $\{0,1\}^{\mathbb{Z}}$ 与区间 $[0,1]$ 之间的同构，Chua 等人将每个细胞自动机与该区间到自身的映射相关联。他们对 Wolfram CA 映射的盆地的显式研究是最完整、最更新的研究，提供了一个详尽的分类，包括不变性和分形性质、绝大多数规则中伊甸岛的丰富性、无标度性质以及一些新的经验拟遍历性。

### 2. 作为动力系统的细胞自动机

从现在开始，我们用 $\mathbb{Z}$ 扩展上述定义来代替 $C_l$。CA 映射是一个玩具空间扩展系统的例子，因为物理扩展动力系统由大空间中的 PDE 给出。然而，这里使用的一些概念可以推广到格点动力系统。

扩展动力系统的空间模式的复杂动力学与自由度较少的系统的动力学相比非常丰富。Lyapunov 指数、拓扑和 Kolmogorov-Sinai 熵的概念被重新表述，以便考虑到时空相互作用。其中一个新概念是熵的空间密度（参见 [3]），它与空间平移和时间演化的两个参数群相关联。通常，当该熵密度非零时，时间演化群的熵是无限的。

细胞自动机动力系统是在无限格点上具有有限熵的最简单的空间扩展玩具系统。为了区分平凡的 CA 如移位与更复杂的 CA，Milnor（[15,16]）引入了方向熵的概念，展示了一类 CA，其与移位不同，在许多方向上具有正熵。最近，还引入了方向 Lyapunov 指数的概念（[7]）。让我们从 Lyapunov 指数开始。M. A. Shereshevsky 在 Wolfram（[21]）之后引入了所谓的 Lyapunov 指数的严格定义（[17]）。根据 Wolfram，这些指数旨在描述一维 CA 中初始模式“局部扰动”向右或向左传播的速度。事实上，局部修改空间构型可能导致扰动无限扩展或被遏制。在第一种情况下，对初始构型的不稳定性对应于正的 Lyapunov 指数。在时空图中观察 Lyapunov 指数是观察此类系统内在不稳定性的最佳方式。

让我们首先介绍一些符号，遵循 Shereshevsky。对于给定的构型 $x = (x_i)$，用 $W_s^+(x)$ 表示通过仅在位点 $s \in \mathbb{Z}$ 的左侧修改 $x$ 而得到的所有构型 $y$ 的集合。换句话说，$y_i = x_i$ 对所有 $i \ge s$ 成立，其余任意。$W_s^-(x)$ 类似地是位点 $(-s)$ 右侧的扰动构型集合。让我们计算在位点 0 左侧的扰动构型 $y \in W_0^+(x)$ 的演化，该构型将在 CA 映射的作用下开始与 $x$ 不同，$f(y)$，$f^2(y)$ 等。通过使用公式

$f(y)_0 = F(y_{-1}, y_0, y_1)$   (1)

以及事实：$y_0 = x_0$, $y_1 = x_1$，我们看到

$f(y)_0 = F(y_{-1}, x_0, x_1)$   (2)

