

对于任意 p > 2，且 T_k 属于 L^p 上积分算子的所谓 Mikhlin-Itskovich 代数。因此我们可以应用 Gohberg、Goldberg 和 Krupnik [21] 提出的重正化行列式理论并定义

```
Δ(k) = det₂(I − T_k)
```

其中行列式 det₂ 是重正化行列式。Brown、Music 和 Perry 证明了对于指数衰减势，该行列式是 k 的实解析函数。现在由 Weierstrass 准备定理可知，Δ(k) 的零点集局部上是多项式的零点集。由于例外集已知是闭且有界的，可以利用有限多个这样的局部表示完全分析 Δ(k) 在例外集附近的行为。可以证明 Δ(k) 也是实值函数，由此可知零点集具有所声称的形式。

定理 6.1 为进一步研究开辟了多个领域。

首先，确定在 t(k) 具有点或线奇异性时，从 t(k) 重构势所需的额外数据将是很有意义的。

其次，很有兴趣知道奇异性是否对超临界势总是存在，或者相反，奇异性在一般情况下是否不存在。

第三，通过将散射变换的‘谱’性质（即其奇异性的性质）与解的长期行为联系起来，我们对 NV 方程及其动力学的理解将得到极大改善。t(k) 的时间演化形式表明，亚临界、临界和超临界势的‘三分法’在 NV 流下是不变的。已知临界初值数据会产生整体解（见 [68]），并且有强有力的证据表明亚临界初值数据也是如此。另一方面，像环状孤子、例 4.3 这样的数值实验，以及 Taimanov 和 Tsarev [85–88] 产生的解析解，都强烈表明超临界初值数据会导致 NV 的解在有限时间内爆破。得到严格证明该情况成立，并通过逆散射方法分析爆破的性质，将是很有趣的。

## 附录 A. 有用的分析

在零能量的直接散射问题中，Faddeev 的格林函数在阐明定义散射变换的 CGO 解的性质方面起着关键作用。回想一下，归一化的 CGO 解满足方程

```
∂̄(∂ + i k) μ = (1/4) q μ
```

并且 Faddeev 的格林函数是算子 ∂̄(∂ + i k) 的格林函数。另一方面，固体 Cauchy 变换是 ∂̄ 算子的逆，其值域在 p > 2 的 L^p 函数中，因此是求解定义逆散射变换的 ∂̄ 问题的根本工具。最后，Beurling 变换是一个积分算子，它为 NV 方程中非线性定义中出现的算子 ∂̄⁻¹ ∂ 赋予了意义。在这里我们收集了这些变换的一些有用性质和一些基本估计。

### A.1. 零能量下的 Faddeev 格林函数。

我们回顾 Faddeev 格林函数 g_k 的一些关键事实。我们将读者引向 Siltanen 的论文 [75] 以获取细节和文献参考。

回想一下 $g_k$ 由公式定义

$$g_k(z) = \frac{1}{(2\pi)^2} \int e^{i\xi\cdot x} \frac{1}{\xi(\xi + k)} \, dm(\xi)$$

其中 $z = x_1 + i x_2$, $\xi \cdot x = \xi_1 x_1 + \xi_2 x_2$, $\xi = \xi_1 + i \xi_2$, 且 $\bar{\xi} = \xi_1 - i \xi_2$。由 Hausdorff-Young 不等式可知，$g_k \in L^p$ 对任意 $p > 2$ 成立。事实上，估计

$$\|g_k\|_p \le C_p |k|^{-2/p}$$

（见 Siltanen [75]，定理 3.10）对任意 $k \neq 0$ 成立。需要注意的是

$$g_k(z) = g_1(kz).$$

$g_1(x)$ 的以下大 $x$ 渐近展开在 [75]，定理 3.11 中证明。

# 引理 A.1. 设 $z = x_1 + i x_2$ 且 $z \neq 0$ 且 $x_1 > 0$。对任意整数 $N \ge 0$,

(A.1)
$$g_1(z) = -\frac{1}{4\pi} \sum_{j=0}^{N} \left[ \frac{j!}{(iz)^{j+1}} - e^{-2 i x_1} \frac{j!}{(-i \bar{z})^{j+1}} \right] + E_N(z)$$

其中

(A.2)
$$|E_N(z)| \le \frac{(N+1)! 2^{(N+1)/2}}{\pi |z|^{N+2}}.$$

由于 $g(-x_1 + i x_2) = \overline{g_1(x_1 + i x_2)}$，当 $x_1 < 0$ 时有类似公式。

# 备注 A.2. 由于误差估计 (A.2) 不依赖于条件 $x_1 > 0$，并且 $g_1(z)$ 是连续的，我们可以得出结论，展开式 (A.1) 对 $z \neq 0$ 且 $\operatorname{Re}(z) = 0$ 仍然成立。

现在考虑 $g_k(z) = g_1(kz)$。由于 $\operatorname{Re}(kz) = \frac{1}{2}(kz + \bar{k}\bar{z})$，我们立即得到：

# 引理 A.3. 设 $z = x_1 + i x_2$ 且 $k \in \mathbb{C}$。对任意整数 $N \ge 0$，展开式

(A.3)
$$g_k(z) = -\frac{1}{4\pi} \sum_{j=0}^{N} \left[ \frac{j!}{(i k z)^{j+1}} - e^{-i(kz + \bar{k}\bar{z})} \frac{j!}{(-i \bar{k}\bar{z})^{j+1}} \right] + E_N(kz)$$

成立，其中

$$|E_N(kz)| \le C_N |kz|^{-(N+2)}.$$

### A.2. Cauchy 变换和 Beurling 算子。

遵循 [3]，第 4 章，我们通过与二维 Poisson 方程相关的对数势研究 Cauchy 变换和 Beurling 算子。对于 $\varphi \in \mathcal{C}_0^\infty(\mathbb{R}^2)$，我们可以定义对数势

$$(L\varphi)(z) = \frac{2}{\pi} \int \log|z - z'| \, \varphi(z') \, dm(z')$$

它具有性质

$$\bar{\partial}\bar{\partial}(L\varphi) = \varphi.$$

与 $L$ 相关的是 Cauchy 变换，

$(P\varphi)(z) = \frac{\partial}{\partial z} (L\varphi)(z),

变换

$(\overline{P}\varphi)(z) = \frac{\partial}{\partial \overline{z}} (L\varphi)(z),

以及 Beurling 变换

$(\mathcal{S}\varphi)(z) = \frac{\partial^2}{\partial z^2} (L\varphi)(z).

由这些定义和 (3.2) 可知

(A.4) $P \circ \frac{\partial}{\partial \overline{z}} = \frac{\partial}{\partial \overline{z}} \circ P = I$

其中 $I$ 是 $\mathcal{C}_0^\infty(\mathbb{R}^2)$ 上的恒等算子，且

(A.5) $\mathcal{S}\left(\frac{\partial \varphi}{\partial \overline{z}}\right) = \frac{\partial \varphi}{\partial z}.$

我们有

$(P\varphi)(z) = \frac{1}{\pi} \int \frac{1}{z - z'} \varphi(z') \, dm(z'),

$(\overline{P}\varphi)(z) = \frac{1}{\pi} \int \frac{1}{\overline{z - z'}} \varphi(z') \, dm(z'),

且

(A.6) $(\mathcal{S}\varphi)(z) = -\frac{1}{\pi} \lim_{\varepsilon \downarrow 0} \left( \int_{|z - z'|>\varepsilon} \frac{1}{(z - z')^2} \varphi(z') \, dm(z') \right).$

关于 $P$ 的以下估计将 Cauchy 变换推广到 $L^p$ 空间，并且是 Hardy-Littlewood-Sobolev 和 Hölder 不等式的标准推论（见 Vekua [92] 或 [3]，§4.3）。它们用于证明定义逆问题的 $\overline{\partial}$ 问题的存在性和唯一性。

# 引理 A.4. (i) 对任意 $p \in (2, \infty)$ 和 $f \in L^{2p/(p+2)}(\mathbb{R}^2)$,

(A.7) $\|P f\|_p \le C_p \|f\|_{2p/(p+2)}.$

(ii) 对任意满足 $1 < q < 2 < p < \infty$ 的 $p,q$ 和任意 $f \in L^p(\mathbb{R}^2) \cap L^q(\mathbb{R}^2)$，估计

(A.8) $\|P f\|_\infty \le C_{p,q} \|f\|_{L^p \cap L^q}$

成立。此外，$P$ 是阶为 $(p-2)/p$ 的 Hölder 连续的，且有

(A.9) $|(Pf)(z) - (Pf)(w)| \le C_p |z - w|^{(p-2)/p} \|f\|_p.$

(iii) 若 $v \in L^s(\mathbb{R}^2)$ 且 $q > 2$ 满足 $q^{-1} + 1/2 = p^{-1} + s^{-1}$，则对任意 $f \in L^p(\mathbb{R}^2)$,

(A.10) $\|P(vf)\|_q \le C_{p,q} \|v\|_s \|f\|_p.$

# 备注 A.5. 由于 $\mathcal{C}_0^\infty(\mathbb{R}^2)$ 在 $L^p \cap L^q$ 中稠密，并且 $(Pf)(z) = \mathcal{O}(z^{-1})$ 当 $|z| \to \infty$ 对任意 $f \in \mathcal{C}_0^\infty(\mathbb{R}^2)$ 成立，由 (ii) 可知，若 $f \in L^p \cap L^q$ 对 $1 < p < 2 < q < \infty$，则 $Pf \in C_0(\mathbb{R}^2)$，即在无穷远处消失的连续函数。

# 备注 A.6. 注意在 (A.10) 中取 s = q 时有

‖P(vf)‖_p ≤ C_p ‖v‖_2 ‖f‖_p.

对任意 $f \in L^{2p/(p+2)}(\mathbb{R}^2)$，引理 A.4 连同 (A.4) 意味着 $u = Pf$ 在分布意义下求解 $\bar{\partial}u = f$。另一方面，假设 $u \in L^p(\mathbb{R}^2)$ 对某个 $p \in [1,\infty)$ 且 $\bar{\partial}u = 0$ 在分布意义下成立。则可知 $\partial\bar{\partial}u = 0$ 在分布意义下成立，从而由 Weyl 引理可知 $u \in C^\infty$。因此，$u$ 实际上是全纯的，由 Liouville 定理可知 $u$ 恒等于零。由这一事实和 (A.4)，我们推得：

# 引理 A.7. 设 $p \in (2,\infty)$，$u \in L^p(\mathbb{R}^2)$，$f \in L^{2p/(p+2)}(\mathbb{R}^2)$，且 $\bar{\partial}u = f$ 在分布意义下成立。则 $u = Pf$。反之，若 $f \in L^{2p/(p+2)}(\mathbb{R}^2)$ 且 $u = Pf$，则 $\bar{\partial}u = f$ 在分布意义下成立。

以下关于 $f$ 快速衰减时 $\bar{\partial}u = f$ 的解的展开式导致了 $\mu(z,k)$ 的大 $k$ 渐近展开。

# 引理 A.8. 设 $p \in (2,\infty)$，$u \in L^p(\mathbb{R}^2)$，$f \in L^{2p/(p+2),N}(\mathbb{R}^2)$，且 $\bar{\partial}u = f$。则

z^N [ u(z) - Σ_{j=0}^{N-1} 1/z^{j+1} ∫ ζ^j f(ζ) dm(ζ) ] ∈ L^p(ℝ²).

# 证明. 估计 (A.7)、引理 A.7 以及公式

1/(z - ζ) = 1/z Σ_{j=0}^{N-1} (ζ/z)^j + 1/z^N ζ^N/(z - ζ).

的直接推论。

# 备注 A.9. 若 $f \in S(\mathbb{R}^2)$ 且关于参数光滑依赖，则渐近展开在逐点意义下成立并且关于参数可微。

主值积分 (A.6) 将 S 识别为 Calderón-Zygmund 型积分算子。我们有（见例如 [3]，§4.5.2）：

# 引理 A.10. 设 $p \in (1,\infty)$。算子 S 延拓为从 $L^p(\mathbb{R}^2)$ 到自身的有界算子，若 $p = 2$ 则为酉算子。此外，若 $\nabla\varphi$ 属于 $L^p(\mathbb{R}^2)$ 对 $p \in (1,\infty)$，则 $S(\partial\varphi) = \bar{\partial}\varphi$。

## 参考文献

- [1] Angelopoulos, Y. Well-posedness and ill-posedness results for the Novikov-Veselov equation. Preprint, arXiv:1307.4110[Math.AP].
- [2] C. Athorne and J. J. C. Nimmo, On the Moutard transformation for integrable partial differential equations, Inverse Problems 7 (1991), no. 6, 809–826. MR1140316 (92k:35011)
- [3] Kari Astala, Tadeusz Iwaniec, and Gaven Martin, Elliptic partial differential equations and quasiconformal mappings in the plane, Princeton Mathematical Series, vol. 48, Princeton University Press, Princeton, NJ, 2009. MR2472875 (2010j:30040)
- [4] Kari Astala and Lassi Päivärinta, Calderón’s inverse conductivity problem in the plane, Ann. of Math. (2) 163 (2006), no. 1, 265–299, DOI 10.4007/annals.2006.163.265. MR2195135 (2007b:30019)
- [5] Richard Beals and R. R. Coifman, Linear spectral problems, nonlinear equations and the ∂̄-method, Inverse Problems 5 (1989), no. 2, 87–130. MR991913 (90f:35171)

