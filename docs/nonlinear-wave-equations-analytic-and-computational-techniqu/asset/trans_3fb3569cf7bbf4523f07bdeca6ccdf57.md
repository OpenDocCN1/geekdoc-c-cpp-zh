

## 参考文献

[1] M. J. Ablowitz, A. S. Fokas, and Z. H. Musslimani, *关于水波的一种新的非局部表述*, J. Fluid Mech. **562** (2006), 313–343, DOI 10.1017/S0022112006001091. MR2263547 (2007k:76013)

[2] M. J. Ablowitz and T. S. Haut, *具有自由界面的两流体欧拉方程的光谱表述及长波约化*, Anal. Appl. (Singap.) **6** (2008), no. 4, 323–348, DOI 10.1142/S0219530508001213. MR2459114 (2010a:76016)

[3] C. T. Bishop and M. A. Donelan. 用压力传感器测量波浪. *Coastal Engineering*, 11:309–328, 1987.

[4] D. Clamond and A. Constantin, *由床面压力测量恢复定常周期波剖面*, J. Fluid Mech. **714** (2013), 463–475, DOI 10.1017/jfm.2012.490. MR3008068

[5] R. R. Coifman and Yves Meyer, *非线性调和分析与解析依赖性*, Pseudodifferential operators and applications (Notre Dame, Ind., 1984), Proc. Sympos. Pure Math. vol. 43, Amer. Math. Soc., Providence, RI, 1985, pp. 71–78, DOI 10.1090/pspum/043/812284. MR812284

[6] A. Constantin, *由压力测量恢复孤立波剖面*, J. Fluid Mech. **699** (2012), 376–384, DOI 10.1017/jfm.2012.114. MR2923684

[7] Adrian Constantin, Joachim Escher, and Hung-Chu Hsu, *孤立水波下的压力：数学理论与实验*, Arch. Ration. Mech. Anal. **201** (2011), no. 1, 251–269, DOI 10.1007/s00205-011-0396-0. MR2807138 (2012f:76032)

[8] Walter Craig and David P. Nicholls, *行进的二维和三维毛细重力水波*, SIAM J. Math. Anal. **32** (2000), no. 2, 323–359, DOI 10.1137/S0036141099354181. MR1781220 (2002c:76016)

[9] W. Craig and C. Sulem, 数值模拟重力波, J. Comput. Phys. **108** (1993), no. 1, 73–83, DOI 10.1006/jcph.1993.1164. MR1239970 (94h:76064)

[10] Bernard Deconinck and Katie Oliveras, *周期表面重力波的不稳定性*, J. Fluid Mech. **675** (2011), 141–167, DOI 10.1017/S0022112011000073. MR2801039 (2012j:76057)

[11] B. Deconinck, K. L. Oliveras, and V. Vasan, *水波问题中底部压力与表面高程的关系*, J. Nonlinear Math. Phys. **19** (2012), no. suppl. 1, 1240014, 11, DOI 10.1142/S14029251124000141. MR2999408

[12] T. Levi-Civita, *有限振幅永久波的严格确定* (法文), Math. Ann. **93** (1925), no. 1, 264–314, DOI 10.1007/BF01449965. MR1512238

[13] Katie Oliveras and Vishal Vasan, *描述行进水波的一个新方程*, J. Fluid Mech. **717** (2013), 514–522, DOI 10.1017/jfm.2012.591. MR3018618

[14] K. L. Oliveras, V. Vasan, B. Deconinck, and D. Henderson, *由压力测量恢复水波剖面*, SIAM J. Appl. Math. **72** (2012), no. 3, 897–918, DOI 10.1137/110853285. MR2968755

[15] Pavel I. Plotnikov and John F. Toland, *Stokes 波的傅里叶系数*, Nonlinear problems in mathematical physics and related topics, I, Int. Math. Ser. (N. Y.) vol. 1, Kluwer/Plenum, New York, 2002, pp. 303–315, DOI 10.1007/978-1-4615-0777-2.18. MR1970618 (2004c:76023)

[16] D. J. Struik, *有限深度渠道中无旋周期波的严格确定* (法文), Math. Ann. **95** (1926), no. 1, 595–634, DOI 10.1007/BF01206629. MR1512296

[17] J. F. Toland, *Stokes 波*, Topol. Methods Nonlinear Anal. **7** (1996), no. 1, 1–48. MR1422004 (97j:35130)

[18] Vishal Vasan and Bernard Deconinck, *行进水波的 Bernoulli 边界条件*, Appl. Math. Lett. **26** (2013), no. 4, 515–519, DOI 10.1016/j.aml.2012.12.008. MR3019985

[19] Vishal Vasan and Bernard Deconinck, *浴底探测的水波逆问题*, J. Fluid Mech. **714** (2013), 562–590, DOI 10.1017/jfm.2012.497. MR3008073

[20] V. Vasan and K. L. Oliveras. 具有常涡度的行进波下的压力. *submitted for publication*, 2013.

Mathematics Department, Seattle University, Seattle, Washington 98102
*E-mail address:* `oliveras@seattleu.edu`

Department of Mathematics, Pennsylvania State University, University Park, Pennsylvania 16802
*E-mail address:* `vasan@math.psu.edu`

## 水波问题中 Dirichlet–Neumann 算子的五种计算方法的比较

Jon Wilkening and Vishal Vasan

摘要. 我们比较了通过 Craig–Sulem (CS) 展开、Ablowitz–Fokas–Musslimani (AFM) 隐式表述、双 AFM 表述 (AFM*)、边界积分配点法 (BIM) 以及变换场展开 (TFE) 方法求解 Dirichlet–Neumann 问题时的有效性。前三种方法涉及高度病态的中间计算，我们证明使用多精度算术可以克服这一问题。后两种方法避免了中间结果中数位的灾难性抵消，更适合数值计算。

对于 Craig–Sulem 展开，我们研究了三种波剖面类型，即带限、实解析或光滑，在每一阶（最高到 150 阶）的项的抵消情况。对于 AFM 和 AFM* 方法，我们给出一个例子，其中 Dirichlet 或 Neumann 数据用 AFM 基函数展开是不可能的，导致方法失效。该例子涉及振幅任意小的带限波剖面，具有解析的 Dirichlet 数据。然后我们展示如何通过过采样基函数并使用奇异值分解或 QR 分解来正交化它们，从而正则化 AFM 和 AFM* 方法。另两个例子用于比较所有五种方法在水波背景下的表现，即深水中的大振幅驻波，以及有限深度中相互作用的一对行进波。

## 1. 引言

水波方程，也称为无粘、无旋波的 Euler 方程，描述了理想流体自由表面的运动。对于二维周期波，在无表面张力且表面平坦的情况下，它们如下给出 [9]：

```
φ_xx + φ_yy = 0,      −h < y < η,
η_t + φ_x η_x = φ_y,    y = η(x,t),
φ_t + 1/2 φ_x² + 1/2 φ_y² + g η = 0,    y = η(x,t),
φ_y = 0,               y = −h.
```

这里 φ 是速度势（与流体速度的关系为 u = ∇φ），η 是水体自由表面的图，g 是重力加速度，h 是未扰动流体的深度，下标表示偏导数。由于我们感兴趣的是周期波，因此在水平方向考虑周期边界条件。我们注意到上述方程代表了 Laplace 方程的自由边界值问题，即 η 和 φ 都是未知量。这些方程很容易推广到三维流体（具有二维表面）；然而，在本工作中，我们将自己限制在一维表面。

水波方程可以用仅表面变量 η(x, t) 和 q = φ(x, η, t) 表示为 [11,33]

```
∂η/∂t = G(η)q,
∂q/∂t = -gη - q_x²/2 + (G(η)q + η_x q_x)² / [2(1 + η_x²)],
```

其中 G(η) 表示 Dirichlet-Neumann 算子 (DNO) 定义为

```
G(η)q = φ_y(x, η) - η_x φ_x(x, η),
```

其中 φ 是以下边界值问题的解

```
φ_xx + φ_yy = 0,      -h < y < η,
φ(x, y) = q(x),      y = η,
φ_y = 0,             y = -h.
```

因此 G(η) 将给定的 Dirichlet 数据 q 映射到自由表面上的相应 Neumann 数据。因此，为了使用某种数值格式在时间上演化表面变量，我们需要在每一步求解 Laplace 方程。数值求解每一步的 Laplace 方程代价高昂，尤其是在三维情况下。

一种避免昂贵数值求解 Laplace 方程的 G(η) 刻画是可取的。在当前工作中，我们讨论了在水波背景下开发的四种此类刻画。这四种方法是 Craig & Sulem 的算子展开法 (CS) [11]、Bruno & Reitich 的变换场展开法 (TFE) [7] 和 Nicholls & Reitich [23,24]、Ablowitz、Fokas & Musslimani 给出的 DNO 的非局部隐式表述 (AFM) [1]，以及由 Ablowitz & Hal [2] 推导的 AFM 方法的对偶版本，我们将其记为 AFM*。每种方法在推导水波在各种物理区域的简化模型 [10]、推导守恒量 [1] 以及为提出某些逆问题提供理论框架 [25,28] 方面都具有显著的理论效用。此外，每种方法都可以很容易地推广到具有变化底部边界和三维流体的情况。

当然，数值求解 Laplace 方程的传统方法很多，包括边界积分法、保角映射技术和有限元法。在本工作中，我们选择将 CS 和 TFE 算子展开以及 AFM/AFM* 非局部表述与边界积分法进行比较。我们不考虑保角映射 [14]，因为它不能推广到三维问题，也不考虑传统有限元 [26]，因为当需要高精度时，高阶单元与刚度矩阵稀疏性之间的权衡使其代价高昂。虽然通常不是这样描述的，但我们将 TFE 方法视为有限元方法的一个谱精度变体。边界积分法在二维中特别高效。

