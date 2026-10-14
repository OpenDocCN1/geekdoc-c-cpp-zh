
关于Sobolev嵌入的一个问题是指定高斯曲率。我们的方法正是从这一观点出发。为了解释背景，让我们回顾几何中的一些概念。

设 $(M, g)$ 是一个 $n$ 维黎曼流形，$P_{1,g}$ 为共形拉普拉斯算子，其定义为

$P_{1,g} = -\Delta_g + \frac{n-2}{4(n-1)} R_g,$

其中 $R_g$ 是度量的标量曲率。我们知道，如果 $\tilde g = e^{2u} g$ 是一个与 $g$ 共形的度量，则对所有光滑函数 $v$，有

$P_{1,\tilde g}(v) = e^{-\left(\frac{n+2}{2}\right)u} P_{1,g}\left(e^{\left(\frac{n-2}{2}\right)u} v\right),$

Paneitz 引入了如下形式的四阶算子 $P_{2,g}$：

$P_{2,g} = \Delta_g^2 + \text{低阶项}$

Branson 发现了如下形式的六阶算子 $P_{3,g}$：

$P_{3,g} = \Delta_g^3 + \text{低阶项}$

它们具有共形不变性质。Graham、Jenne、Mason 和 Sparling（通常称为 GJMS 算子）获得了高阶一般共形算子的存在性。他们证明了

## 定理 9.8
设 $(M, g)$ 是一个偶数维 $n$ 的黎曼流形。对于 $k \in \left\{1,2,\dots,\frac{n}{2}\right\}$，存在一个形式为

$P_{k,g} = \Delta_g^k + \text{低阶项}$

的共形不变微分算子 $P_{k,g}$，满足

$P_{k,\tilde g}(v) = e^{-\left(\frac{n+2k}{2}\right)u} P_{k,g}\left(e^{\left(\frac{n-2k}{2}\right)u} v\right)$

其中共形度量 $\tilde g = e^{2u} g$。

当 $n$ 为偶数且 $k > \frac{n}{2}$ 时，具有上述性质的共形不变算子 $P_{k,g}$ 在一般情况下可能不存在。因此，$P_{\frac{n}{2},g}$ 被称为临界 GJMS 算子。

注意到，将 $P_{1,g}$ 作用于常数函数即可恢复度量的标量曲率。类似地，我们为偶数维 $n$ 的黎曼流形 $(M, g)$ 定义称为 $Q_k$ 曲率的高阶曲率。设 $k$ 为满足 $k < \frac{n}{2}$ 的整数，则 $Q_k$ 曲率定义为

$Q_k = \frac{2(-1)^k}{n-2k} P_k(1)$

而 $Q_{\frac{n}{2}}$ 曲率通过上述公式中的解析延拓来定义。

与高斯曲率类似，$Q_{\frac{n}{2}}$ 曲率在度量的共形变换下的变化由 GJMS 算子控制。设 $\tilde{g}=e^{2u}g$ 是 $(M,g)$ 上的共形度量，则 $Q_{\frac{n}{2},g}$ 与 $Q_{\frac{n}{2},\tilde{g}}$ 通过如下关系相联系

$$P_{\frac{n}{2},g}(u)+Q_{\frac{n}{2},g}=Q_{\frac{n}{2},\tilde{g}}\,e^{nu}\tag{9.18}$$

容易看出，上述方程的解正是能量 $J$ 的临界点，其中 $J$ 由下式给出

$$J(u)=\frac{1}{2}\int_{M}P_{k}(u)u\,dV_{g}+\int_{M}Q_{k,g}u\,dV_{g}-\frac{1}{N}\int_{M}Q_{k,\tilde{g}}e^{nu}\,dV_{g}\tag{9.19}$$

其中 $k=\frac{n}{2}$。

我们希望构造该泛函的一个自然空间是满足 $\int_{M}P_{k}(u)u\,dV_{g}<\infty$ 的空间。然后我们需要知道能否用 $\int_{M}P_{k}(u)u\,dV_{g}$ 来控制 $\int_{M}e^{nu}\,dV_{g}$。我们在文献[24]中肯定地回答了这些问题。下面简要讨论主要结果。

首先回顾 Sobolev 空间 $H^{k}(\mathbb{H}^{n})$ 的定义。我们将 $H^{k}(\mathbb{H}^{n})$ 定义为 $C_{c}^{\infty}(\mathbb{H}^{n})$ 关于范数

$$||u||_{H^{k}(\mathbb{H}^{n})}:=[\sum_{m=0}^{k}\int_{\mathbb{H}^{n}}|\nabla_{g}^{m}u|_{g}^{2}\,dv_{g}]^{\frac{1}{2}},$$

的完备化。

众所周知，Poincaré 不等式

$$\left(\frac{n-1}{2}\right)^{2}\int_{\mathbb{H}^{n}}u_{g}^{2}\,dv_{g}\le\int_{\mathbb{H}^{n}}|\nabla_{g}u|_{g}^{2}\,dv_{g}$$

对所有 $u\in H^{1}(\mathbb{H}^{n})$ 成立。我们还有

$$\int_{\mathbb{H}^{n}}|\nabla_{g}u|_{g}^{2}\,dv_{g}=\int_{\mathbb{H}^{n}}- (\Delta_{g}u)u\,dv_{g}\le\left(\int_{\mathbb{H}^{n}}|\Delta_{g}u|^{2}\,dv_{g}\right)^{\frac{1}{2}}\left(\int_{\mathbb{H}^{n}}u^{2}\,dv_{g}\right)^{\frac{1}{2}}$$

将上述两个不等式与归纳论证相结合，我们得到如下高阶 Poincaré 型不等式：

设 $k,l$ 为非负整数且 $l<k$，则

$$\left(\frac{N-1}{2}\right)^{2(k-l)}\int_{\mathbb{H}^{n}}|\nabla_{g}^{l}u|_{g}^{2}\,dv_{g}\le\int_{\mathbb{H}^{n}}|\nabla_{g}^{k}u|_{g}^{2}\,dv_{g}$$

对所有 $u\in H^{k}(\mathbb{H}^{n})$ 成立。

因此我们看出，由下式定义的范数 $\|u\|_{H^k(\mathbb{H}^n)}$

$$\|u\|_{H^k(\mathbb{H}^n)}:=\left[\int_{\mathbb{H}^n}|\nabla_g^k u|^2\,dv_g\right]^{\frac12},\qquad u\in H^k(\mathbb{H}^n)$$

在 $H^k(\mathbb{H}^n)$ 中定义了一个等价范数。

接下来，我们定义 $\|\cdot\|_{k,g}$ 为

$$\|u\|_{k,g}:=\left[\int_{\mathbb{H}^n}(P_k u)u\,dv_g\right]^{\frac12},\qquad u\in C_0^\infty(\mathbb{H}^n),$$

于是我们得到：

## 引理 9.2
*(Karmakar, Sandeep [24])*

设 $\|\cdot\|_{k,g}$ 如上所述，则当 $2k\le n$ 时，它在 $C_0^\infty(\mathbb{H}^n)$ 上定义了一个范数。此外，当 $n=2k$ 时，存在正常数 $\Theta$ 使得

$$\frac{1}{\Theta}\|u\|_{k,g}\le \|u\|_{H^k(\mathbb{H}^n)}\le \Theta\|u\|_{k,g},$$

对所有 $u\in C_0^\infty(\mathbb{H}^n)$ 成立。

利用该范数 $\|\cdot\|_{k,g}$，我们在 $\mathbb{H}^n$ 上建立了 Adams 型不等式。

## 定理 9.9
*(Karmakar, Sandeep [24])*

设 $\mathbb{H}^n$ 是 $n$ 维双曲空间，其中 $n$ 为偶数且 $k=\frac n2$，则

$$\sup_{u\in C_0^\infty(\mathbb{H}^n),\ \|u\|_{k,g}\le1}\int_{\mathbb{H}^n}(e^{\beta u^2}-1)\,dv_g<+\infty$$

当且仅当 $\beta\le\beta_0(k,n)$，其中 $\beta_0(k,n)$ 如前所述。

回顾一下，Fontana 和 Morpurgo 在文献[23]中得到了 $\mathbb{H}^n$ 上 Adams 不等式的一个版本。一个自然的问题是，定理 9.8 与文献[23]中的不等式相比如何。对于 $n=4,\ 6,\ 8$，我们可以验证 $\|u\|_{k,g}<\int_{\mathbb{H}^n}|\nabla^k u|^2$。因此，我们的不等式蕴含了 Fontana 和 Morpurgo 所得到的结果。

为实现我们的目标，我们利用方程(9.18)中的 Adams 不等式研究了形如方程(9.18)的偏微分方程的存在性。我们可以证明，作为 $Q_{k,g}$ 的 $L^2$ 扰动的负 $Q_{k,\hat g}$ 曲率可以被指定。更一般地，我们证明了

## 定理 9.10
*(Karmakar, Sandeep [24])*

假设 $Q_1-Q_2\in L^2(\mathbb{H}^n)$ 且 $Q_2\le0$，则方程

$$P_k(u)+Q_1=Q_2e^{nu}$$

在 $H^k(\mathbb{H}^n)$ 中存在解。

Moser–Trudinger 和 Adams 不等式的研究仍然是一个活跃的研究领域，在上述结果建立之后涌现出许多有趣的结果。例如，文献[25]中建立了其他一些版本，文献[26]中在具夹挤性质的 Hadamard 流形情形下建立了 Adams 不等式等。

## 参考文献

- 1. Pohozhaev, S.I. The Sobolev imbedding in the case p l = n, In: Proc. Tech. Sci. Conf. on Adv. Sci. Research 1964–1965, Mathematics Section, pp. 158–170. Moskov. Energet. Inst., Moscow, 1965.
- 2. Trudinger, Neil S. On imbeddings into Orlicz spaces and some applications, J. Math. Mech. 17, 473–483, 1967.
- 3. Moser, J. A sharp form of an inequality by N. Trudinger, Indiana Univ. Math. J. 20, 1077–1092, 1970/71.
- 4. Carleson, Lennart, and Chang, Sun-Yung A. On the existence of an extremal function for an inequality of J. Moser, Bull. Sci. Math. 110(2), 113–127, 1986.
- 5. Flucher, M. Extremal functions for the Trudinger-Moser inequality in 2 dimensions, Comment. Math. Helv. 67, 471–497, 1992.
- 6. Adimurthi , and Druet, O.. Blow-up analysis in dimension 2 and a sharp form of Trudinger-Moser inequality, Comm. Partial Diff. Equat. 29(1–2), 295–322, 2004.
- 7. Cao, D. Nontrivial solution of semilinear elliptic equations with critical exponent in R², Commun. Partial Diff. Equat. 17, 407–435, 1992.
- 8. Panda, R. Nontrivial solution of a quasilinear elliptic equation with critical growth in Rⁿ, Proc. Indian Acad. Sci. 105, 425–444, 1995.
- 9. do Ó, J.M. N-Laplacian equations in Rᴺ with critical growth, Abstr. Appl. Anal. 2, 301–315, 1997.
- 10. Ruf, B. A sharp Trudinger-Moser type inequality for unbounded domains in R², J. Funct. Anal. 219(2), 340–367, 2005.
- 11. Li, Y., and Ruf, B. A sharp Trudinger-Moser type inequality for unbounded domains in Rᴺ, Indiana Univ. Math. J. 57(1), 451–480, 2008.
- 12. Onofri, E. On the positivity of the effective action in a theory of random surfaces, Comm. Math. Phys. 86(3), 321–326, 1982.
- 13. Beckner, William. Sharp Sobolev inequalities on the sphere and the Moser-Trudinger inequality, Ann. of Math. 138(1), 213–242, 1993.
- 14. Cherrier, Pascal. Une inégalité de Sobolev sur les variétés riemanniennes, Bull. Sci. Math. 103(4), 353–374, 1979.
- 15. Fontana, Luigi. Sharp borderline Sobolev inequalities on compact Riemannian manifolds, Comment. Math. Helv. 68(3), 415–454, 1993.
- 16. Mancini, G., and Sandeep, K. Moser-Trudinger inequality on conformal discs, Commun. Contemp. Math. 12(6), 1055–1068, 2010.
- 17. Battaglia, Luca, and Mancini, Gabriele. Remarks on the Moser-Trudinger inequality, Adv. Nonlinear Anal. 2(4), 389–425, 2013.
- 18. Lu, G., and Tang, H. Best constants for Moser-Trudinger inequalities on high dimensional hyperbolic spaces, Adv. Nonlinear Stud. 13(4), 1035–1052, 2013.
- 19. Mancini, G., Sandeep, K., and Tintarev, C. Trudinger-Moser inequality in the hyperbolic space Hⁿ, Adv. Nonlinear Anal. 2(3), 309–324, 2013.
- 20. Adimurthi , and Tinterev, K. On a version of Trudinger-Moser inequality with Möbius shift invariance, Calc. Var. Part. Diff. Equat. 39(1–2), 203–212, 2010.
- 21. Yang, Qiaohua, Su, Dan, and Kong, Yinying. Sharp Moser-Trudinger inequalities on Riemannian manifolds with negative curvature. Ann. Mat. Pura Appl. 195(2), 459–471, 2016.
- 22. Adams, D.R. A sharp inequality of J. Moser for higher order derivatives, Ann. Math. 128, 385–398, 1988.

