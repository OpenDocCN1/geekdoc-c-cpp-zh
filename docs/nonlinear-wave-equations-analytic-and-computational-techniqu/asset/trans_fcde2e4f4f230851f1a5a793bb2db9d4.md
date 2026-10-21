

- [16] M. Klaus 和 J. K. Shaw, *关于 Zakharov-Shabat 系统的特征值*, SIAM J. Math. Anal. **34** (2003), no. 4, 759–773, DOI 10.1137/S0036141002403067. MR1969601 (2004c:34260)

- [17] Jérôme Jp. Leon, *Dirac 逆谱变换：kinks 和 boomerons*, J. Math. Phys. **21** (1980), no. 10, 2572–2578, DOI 10.1063/1.524362. MR586340 (82d:81022)

- [18] C. J. Pethick 和 H. Smith, *稀薄气体中的玻色-爱因斯坦凝聚*, Cambridge University Press, Cambridge (2002).

- [19] A. Fratalocchi, C. Conti, G. Ruocco, 和 S. Trillo, *非相互作用非线性波粒子气体中的自由能转变*, Phys. Rev. Lett. **101**, 044101 (2008).

- [20] C. van der Mee, *可积类型的非线性演化模型*, 100 页, SIMAI e-Lecture Notes **11**, 2013.

- [21] V. E. Zakharov 和 A. B. Shabat, *二维自聚焦和非线性介质中一维自调制的精确理论* (俄文，附英文摘要), Ž. Èksper. Teoret. Fiz. **61** (1971), no. 1, 118–134; 英文译文, Soviet Physics JETP **34** (1972), no. 1, 62–69. MR0406174 (53 #9966)

- [22] V. E. Zakharov 和 A. B. Shabat, *稳定介质中孤子的相互作用*, Sov. Phys. JETP **37**, 823–828 (1973).

Università di Cagliari, Dip. Matematica e Informatica, Viale Merello 92, Cagliari
*E-mail address:* fdemontis@unica.it

Università di Cagliari, Dip. Matematica e Informatica, Viale Merello 92, Cagliari
*E-mail address:* cornelis@krein.unica.it

Università del Salento, Dip. Matematica e Fisica “E. De Giorgi”, Via per Arnesano, Lecce and Sezione INFN
*E-mail address:* federica.vitale@le.infn.it

## The Novikov-Veselov Equation: Theory and Computation

R. Croke, J. L. Mueller, M. Music, P. Perry, S. Siltanen, 和 A. Stahel

## Abstract

我们回顾了势在无穷远处衰减的 Novikov-Veselov (NV) 方程的理论和计算方面的最新进展，主要集中在零能情形。零能 NV 方程的逆散射方法在 Manakov 三元组框架下给出，并对电导率型初值进行了严格处理。给出了特殊的闭式解，包括多孤子、环形孤子和呼吸子。计算逆散射方法被用来研究零能例外点以及超临界、临界和亚临界势之间的关系。

*2010 Mathematics Subject Classification.* Primary 37K15; Secondary 35Q53, 65M32, 47J35, 70H06.

Michael Music 部分由 NSF 资助项目 DMS-1208778 支持。

Peter Perry 部分由 NSF 资助项目 DMS-1208778 支持。

Samuli Siltanen 部分由芬兰卓越中心逆问题研究 2012-2017 支持 (芬兰科学院 CoE 项目 250215)。

## Contents

- 1. Introduction
- 2. Background for the Zero-Energy NV Equation
- 3. Inverse Scattering via Manakov Triples
- 4. Special Solutions
- 5. Zero-energy exceptional points
- 6. Open Problems
- Appendix A. Some Useful Analysis
- References

## 1. Introduction

Novikov-Veselov (NV) 方程是完全可积的、非线性色散方程

```
(1.1)
q_t = 4 Re (4∂³ q + ∂ (q w) − E ∂ w)
\bar{∂} w = −3 ∂ q
```

这里 $E$ 是一个实参数，未知函数 $q$ 是两个空间变量和时间的实值函数，且算子 $\partial$ 和 $\overline{\partial}$ 由下式给出

```
$\partial = \frac{1}{2}\left(\partial_{x_1} - i\partial_{x_2}\right)$

$\overline{\partial} = \frac{1}{2}\left(\partial_{x_1} + i\partial_{x_2}\right).$
```

在零能 ($E = 0$) 时，经过平凡重标定后它也可以写成

```
(1.2) $q_t = -\partial_z^3 q - \overline{\partial}^3 q + 3\partial_z(q\nu) + 3\overline{\partial}_z(q\bar{\nu}),\quad \text{where } \overline{\partial}_z\nu = \partial_z q.$
```

NV 方程 (1.2) 将著名的 Korteweg-de Vries (KdV) 方程

```
$q_t = -6 q q_x - q_{xxx}$
```

推广了，因为如果 $q(x_1,t)$ 解 KdV 且 $\nu_{x_1}(x_1,t) = -3 q_{x_1}(x_1,t)$，则 $q(x_1,t)$ 解 NV。

NV 方程由 Novikov 和 Veselov 在 [64, 65] 中引入，作为生成固定能量 $E$ 下二维 Schrödinger 算子的等谱流的完全可积方程族之一。事实上，Novikov-Veselov 方程 (1.1) 允许 Manakov 三元组表示 [48]

```
(1.3) $\dot{L} = [A, L] - B L$
```

其中

```
$L = -\Delta + q - E,$

$A = 8\left(\partial^3 + \overline{\partial}^3\right) + 2\left(w\partial + \overline{w}\overline{\partial}\right),$

$B = -2\left(\partial w + \overline{\partial}\overline{w}\right).$
```

这里 $B$ 是函数 $2\left(\partial w + \overline{\partial}\overline{w}\right)$ 的乘法算子。即，一对 $(q,w)$ 解 NV 方程当且仅当算子方程 (1.3) 成立。

Manakov 三元组表示意味着 NV 方程在形式上至少是完全可积的。因此我们期望，对于固定能量 $E$ 下 $L$ 的“散射数据”的合适概念，相关的散射变换将线性化流。

对于非零能量 $E$ 且势 $q$ 在无穷远处消失的情形，散射变换和逆散射方法由 P. Grinevich、R. G. Novikov 和 S.-P. Novikov 发展 (参见 Kazeykina 的论文 [36] 提供了极好的综述，原始论文见 [23, 26–28])。粗略且非正式地说，存在一个散射变换 $\mathcal{T}$ 将势 $q$ 映射到散射数据，如果 $q$ 满足 NV 方程则该数据满足线性方程，并且存在逆散射变换 $\mathcal{Q}$ 逆转 $\mathcal{T}$，使得函数

```
(1.4) $q(x,\tau) = \mathcal{Q}\left[e^{i\tau\left(\partial^3 + \overline{\partial}^3\right)}\mathcal{T}(q_0)\right](x)$
```

解具有初值 $q_0$ 的 NV 方程。逆散射方法可由以下交换图可视化：

![](img/c92a9d81ba7f671c83a4c600d27389fb_39_0.png)

其中 $T$ 和 $Q$ 分别代表直接和逆非线性傅里叶变换，且函数 $t_\tau : \mathbb{C} \to \mathbb{C}$ 称为散射变换。在 $E = 0$ 的情形，逆散射方法由 Boiti 等 [9]、Tsai [89]、Nachman [58]、Lassas-Mueller-Siltanen [44]、Lassas-Mueller-Siltanen-Stahel [45, 46]、Music [54]、Music-Perry [55] 和 Perry [68] 研究。最近，Angelopoulos [1] 证明了 $E = 0$ 时的 Novikov-Veselov 方程在 Sobolev 空间 $H^s(\mathbb{R}^2)$ 中对 $s > 1/2$ 是局部适定的，为该方程的局部存在理论奠定了坚实基础。逆散射方法的潜在效用在于阐明解的全局行为。

$E = 0$ 的情形有些特殊，与二维 Schrödinger 算子 $L$ 在零能时的以下行为三分法密切相关。

**Definition 1.1.** 算子 $L = -\Delta + q$ 称为：

- (i) 亚临界，如果算子 $L$ 具有正的格林函数且方程 $L\psi = 0$ 具有严格正的分布解，
- (ii) 临界，如果 $L\psi = 0$ 具有有界严格正解但没有正的格林函数，且
- (iii) 超临界，否则。

这种区分最初出现在 Schrödinger 半群的研究中，即算子 $e^{-tL}$ 其中 $L = -\Delta + q$。Simon [79, 80] (参见 [81]) 研究了 $e^{-tL}$ 的 $L^p$-映射性质以及 $\|e^{-tL}\|_{p,p'}$ 的渐近性，其中 $\|\cdot\|_{p,p}$ 表示从 $L^p$ 到自身的算子范数。Simon 表明 $\alpha_p(q) = \lim_{t\to\infty} t^{-1} \ln \|e^{-tL}\|_{p,p}$ 与 $p \in [1,\infty]$ 无关。在 Schrödinger 半群的语言中，势 $q$ 是：

- (i) 亚临界，如果对某个 $\varepsilon > 0$ 有 $\alpha_\infty((1+\varepsilon)q) = 0$，
- (ii) 临界，如果 $\alpha_\infty(q) = 0$ 但对所有 $\varepsilon > 0$ 有 $\alpha_\infty((1+\varepsilon)q) > 0$，且
- (iii) 超临界，如果 $\alpha_\infty(q) > 0$。

显然，$L$ 具有负特征值的充分条件是 $q$ 为超临界。

在 [52] 中，Murata 表明，对于势 $q$ 满足 $q(x)$ 均匀 Hölder 连续且 $q(x) = O(|x|^{-4-\varepsilon})$ 对某个 $\varepsilon > 0$ 的二维 Schrödinger 算子，Schrödinger 半群的行为三分法等价于定义 1.1。Murata 在 [52] 中进一步研究了 Schrödinger 方程正解的存在性和性质，并表明对于他的势类，三分法可表征如下：势是

