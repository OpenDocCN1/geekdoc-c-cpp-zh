

或 H_B 的 1.1%。周期相对变化为 (T_Euler − T_KdV)/T_Euler = 3.6%。虽然图 11 和图 12 的左侧面板显示在 t = 0 时 Euler 方程与 KdV 方程的相对周期解之间存在密切一致，但应注意，这些图中余弦波解的波幅是经过选择的，以最小化这些图中的差异。周期分别变化 18% 和 3.6%，或许是衡量一致性的更好指标。

对两个方程的最后一次比较在图 13 中进行，其中我们用 KdV 初始条件演化 Euler 方程。这需要 φ(x) = φ(x, η(x)) 的初始条件，其中我们在此讨论中省略了 t 的记号，因为它固定为 0。基于上面给出的推导，我们首先在底部边界上求解 φ_x(x,0) = √(g/h) [η(x) − h] 得到 φ。然后我们使用近似

```
φ(x,η(x)) ≈ φ(x,0) − η(x)²/2 φ_xx(x,0) + η(x)⁴/24 φ_xxxx(x,0)
```

来在自由表面上求值 φ。在图 13 的左侧面板中，较大的波在 t = T/400 之前在 Euler 方程下演化时增长并翻转，而不是像 KdV 演化时那样向右传播。为了处理波破碎，我们改用自由表面 Euler 方程的角度-弧长公式 [4, 26]。在右侧面板的小振幅示例中，Euler 解产生了可见的辐射并略微落后于 KdV 解，尽管在 T/2 时相位比在图 10 中用 KdV 演化 Stokes 波的结果更接近。我们还尝试求值

```
φ(x,y) = √(g/h) Σ_{k=1}^∞ 2k^{-1} η̂_k sin(kx) cosh(ky)
```

在 y = η(x) 处以获得 φ(x) 的初始条件，其中 η̂_k 是 t = 0 时 η(x) 的傅里叶模态，但对于大振幅示例结果更差——波破碎得更快——而在小振幅示例中在视觉上与图 13 中绘制的结果无法区分。

总之，§4 中找到的 Euler 方程的大振幅时间周期解在任何衡量标准下都远超出 KdV 区域，而小振幅相对周期解更接近，但不够接近，无法在感兴趣的整个时间间隔内实现定量一致。

## 6. 结论

我们证明了当两列 Stokes 波在浅水中相互作用时产生的少量背景辐射通常可以调节，以获得自由表面 Euler 方程的时间周期和相对周期解。就像 Korteweg-de Vries 方程一样，波在碰撞时可以完全合并或保持良好分离。然而比较仅是定性的，因为波太大而无法被 KdV 理论很好地近似。

在未来的工作中，我们将使用 Floquet 理论研究这些解的稳定性。初步结果表明，上面考虑的第一个示例对谐波扰动不稳定，而第二个示例是稳定的。在稳定情况下，一个有趣的开放问题是，作为最小化算法起始猜测的 Stokes 波，其能量与找到的相对周期解相同，是否可能永远保持接近它，围绕它执行近周期振荡。 presumably θ 需要稍微变化才能使这一点成立，因为 θ 是我们手动选择的自由参数，以使初始猜测的 f 具有较小值。另一个开放问题是 Euler 方程是否存在 KdV 方程中 N ≥ 3 的 N 相拟周期解的类似物。我们有信心本文的方法可用于构造 N ≥ 3 的孤立水波沿时间周期或相对周期方式弹性碰撞的退化情况，类似于 [3] 中对 Benjamin-Ono 方程所做的那样。计算形式为 η(x,t)=H(κx+ωt+α), φ(x,t)=Φ(κx+ωt+α) 且 H,Φ∈C(T^N) 且 κ, ω, α∈R^N 的更一般拟周期动力学在原则上似乎是可能的，使用更复杂的打靶方法来确定 H、Φ 和 ω。Euler 方程此类解的存在将表明非可积方程也可以支持复发弹性碰撞，即使它们不能表示为椭圆函数的 N 相叠加。

**大振幅示例** **小振幅示例**

**图 11.** §4 中找到的时间周期解与 KdV 的附近相对周期两相余弦波解的比较。周期分别为 T = 138.387 和 113.079。

**图 12.** §4 中找到的相对周期解与 KdV 的附近相对周期两相余弦波解的比较。周期分别为 T = 1108.11 和 1068.73。

**图 13.** KdV 与 Euler 解的比较，两者均以 2 相余弦波初始化，其峰值与图 1 中标记为 A 和 B（左）或 B 和 C（右）的 Stokes 波的高度相匹配。这里 T = 138.387（左）和 T = 1068.73（右）。

## 参考文献

- [1] Mark J. Ablowitz and Harvey Segur, Solitons and the inverse scattering transform, SIAM Studies in Applied Mathematics, vol. 4, Society for Industrial and Applied Mathematics (SIAM), Philadelphia, Pa., 1981. MR642018 (84a:35251)
- [2] H. Airault, H. P. McKean, and J. Moser, Rational and elliptic solutions of the Korteweg-de Vries equation and a related many-body problem, Comm. Pure Appl. Math. 30 (1977), no. 1, 95–148. MR0649926 (58 #31214)
- [3] David M. Ambrose and Jon Wilkening, Global paths of time-periodic solutions of the Benjamin-Ono equation connecting pairs of traveling waves, Commun. Appl. Math. Comput. Sci. 4 (2009), 177–215, DOI 10.2140/camcos.2009.4.177. MR2565874 (2010j:35437)
- [4] David M. Ambrose and Jon Wilkening, Computation of symmetric, time-periodic solutions of the vortex sheet with surface tension, Proc. Nat. Acad. Sci. 107 (2010), no. 8, 3361–3366.
- [5] David M. Ambrose and Jon Wilkening, Computation of time-periodic solutions of the Benjamin-Ono equation, J. Nonlinear Sci. 20 (2010), no. 3, 277–308, DOI 10.1007/s00332-009-9058-x. MR2639896 (2011d:65146)
- [6] David M. Ambrose and Jon Wilkening, Dependence of time-periodic vortex sheets with surface tension on mean vortex sheet strength, Procedia IUTAM 11 (2014), 15–22.
- [7] Gregory R. Baker, Daniel I. Meiron, and Steven A. Orszag, Generalized vortex methods for free-surface flow problems, J. Fluid Mech. 123 (1982), 477–501, DOI 10.1017/S0022112082003164. MR687014 (84a:76002)
- [8] Gregory R. Baker and Chao Xie, Singularities in the complex physical plane for deep water waves, J. Fluid Mech. 685 (2011), 83–116, DOI 10.1017/jfm.2011.283. MR2844303
- [9] Jerry L. Bona, Thierry Colin, and David Lannes, Long wave approximations for water waves, Arch. Ration. Mech. Anal. 178 (2005), no. 3, 373–410, DOI 10.1007/s00205-005-0378-1. MR2196497 (2007a:76012)
- [10] R. K.-C. Chan and R. Street, A computer study of finite amplitude water waves, J. Comput. Phys. 6 (1970), 68–94.
- [11] G. A. Chandler and I. G. Graham, The computation of water waves modelled by Nekrasov's equation, SIAM J. Numer. Anal. 30 (1993), no. 4, 1041–1065, DOI 10.1137/0730054. MR1231326 (94e:65144)
- [12] B. Chen and P. G. Saffman, Numerical evidence for the existence of new types of gravity waves of permanent form on deep water, Stud. Appl. Math. 62 (1980), no. 1, 1–21. MR557677 (80k:76014)
- [13] M. J. Cooker, P. D. Weidman, and D. S. Bale, Reflection of a high-amplitude solitary wave at a vertical wall, J. Fluid Mech. 342 (1997), 141–158, DOI 10.1017/S002211209700551X. MR1460657 (98d:76026)
- [14] Walter Craig, An existence theory for water waves and the Boussinesq and Korteweg-de Vries scaling limits, Comm. Partial Differential Equations 10 (1985), no. 8, 787–1003, DOI 10.1080/03605308508820396. MR795808 (87f:35210)
- [36] G. N. Mercer and A. J. Roberts, Standing waves in deep water: their stability and extreme form, Phys. Fluids A 4 (1992), no. 2, 259–269, DOI 10.1063/1.858354. MR1146134 (92k:76014)
- [37] Paul A. Milewski, J.-M. Vanden-Broeck, and Zhan Wang, Dynamics of steep two-dimensional gravity–capillary solitary waves, J. Fluid Mech. 664 (2010), 466–477, DOI 10.1017/S0022112010004714. MR2747492 (2011m:76026)
- [38] R. M. Mirie and C. H. Su, Collisions between two solitary waves, Part II, J. Fluid Mech. 115 (1982), 475–492.
- [39] Jorge Nocedal and Stephen J. Wright, Numerical optimization, Springer Series in Operations Research, Springer-Verlag, New York, 1999. MR1713114 (2001b:90002)
- [40] L. A. Ostrovsky and Y. A. Stepanyants, Internal solitons in laboratory experiments: comparison with theoretical models, Chaos 15 (2005), no. 3, 037111, 28, DOI 10.1063/1.2107087. MR2184887 (2006h:76025)
- [41] P. I. Plotnikov and J. F. Toland, Nash-Moser theory for standing water waves, Arch. Ration. Mech. Anal. 159 (2001), no. 1, 1–83, DOI 10.1007/PL00004246. MR1854060 (2002k:76019)
- [42] Chris H. Rycroft and Jon Wilkening, Computation of three-dimensional standing water waves, J. Comput. Phys. 255 (2013), 612–638, DOI 10.1016/j.jcp.2013.08.026. MR3109807
- [43] Guido Schneider and C. Eugene Wayne, The long-wave limit for the water wave problem. I. The case of zero surface tension, Comm. Pure Appl. Math. 53 (2000), no. 12, 1475–1535, DOI 10.1002/1097-0312(200012)53:12<1475::AID-CPA1>3.0.CO;2-V. MR1780702 (2002c:76025a)
- [44] C. H. Su and Rida M. Mirie, On head-on collisions between solitary waves, J. Fluid Mech. 98 (1980), no. 3, 509–525, DOI 10.1017/S0022112080000262. MR583060 (81g:76023)
- [45] J.-M. Vanden-Broeck, Elevation solitary waves with surface tension, Phys. Fluids A 3 (1991), 1989–1993.
- [46] G. B. Whitham, Linear and nonlinear waves, Wiley-Interscience [John Wiley & Sons], New York-London-Sydney, 1974. Pure and Applied Mathematics. MR0483954 (58 #3905)
- [47] J. Wilkening, Breakdown of self-similarity at the crests of large amplitude standing water waves, Phys. Rev. Lett. 107 (2011), 184501.
- [48] ———, Traveling-standing water waves, (2014), (in preparation).
- [49] J. Wilkening and J. Yu, Overdetermined shooting methods for computing standing water waves with spectral accuracy, Comput. Sci. Disc. 5 (2012), 014017:1–38.
- [50] M. O. Williams, J. Wilkening, E. Shlizerman, and J. N. Kutz, Continuation of periodic solutions in the waveguide array mode-locked laser, Physica D 240 (2011), no. 22, 1791–1804.
- [51] Wolfram Research, Inc., Mathematica, version 8.0, Champaign, IL, 2010.
- [52] N. J. Zabusky and C. J. Galvin, Shallow-water waves, the Korteweg-de Vries equation and solitons, J. Fluid Mech. 47 (1970), 811–824.
- [53] Qisu Zou and Chau Hsing Su, Overtaking collision between two solitary waves, Phys. Fluids 29 (1986), no. 7, 2113–2123, DOI 10.1063/1.865599. MR848314 (87h:76033)

