
-   (i) U(s,s)=I（恒等算子），U(t,r)U(r,s)=U(t,s) 对 0 ≤ s ≤ r ≤ t ≤ T̃。
-   (ii) (t,s) ↦ U(t,s) 对 0 ≤ s ≤ t ≤ T̃ 强连续。

**定理 18.2.** 设 τ_N 为 (18.10) 中定义的停时。设 Ba ⊂ X 且 {A(t,b)}, (t,b) ∈ I × Ba 为满足 (H7)–(H9) 的算子族。若 x ∈ L²_𝔽(Ω, C(I,X)) 则存在唯一的随机演化系统 {U(t,s;x)} := {U(t,s,(x(r,ω))_{r≤t})} 定义在三角形 Δ := {0 ≤ s ≤ t ≤ T̃} 上，满足以下性质在 Ω 上逐点成立。

-   (P1) sup_{t,s∈Δ} ‖U(t,s;x)‖_{𝕃(X,X)} ≤ M e^{β T̃}，其中 M 和 β 为稳定性常数。
-   (P2) ∂/∂t U(t,s;x) y = A(s,x(s)) U(t,s;x) y 对 y ∈ Y，0 ≤ s ≤ t ≤ T̃。
-   (P3) ∂/∂s U(t,s;x) y = −U(t,s;x) A(s,x(s)) y 对 y ∈ Y，0 ≤ s ≤ t ≤ T̃。

上述定理的证明类似于 [15] 中定理 2.13 和 [18] 中定理 5.3.1 的证明，因此省略。

所构造的随机演化算子仅为 ℱ_t-可测的，一般不是 ℱ_s-可测的。因此随机积分 ∫₀^t U(t,s;x) Φ dW(s) 在 Itô 意义下未定义。

为纠正此问题，我们应用分部积分（见 [19]）并得到不涉及非适应被积函数的随机积分的项，如下所示。

∫₀^t U(t,s;x) Φ dW(s) = U(t,0;x) ∫₀^t Φ dW(θ) + ∫₀^t U(t,s;x) A(s,x(s)) (∫_s^t Φ dW(θ)) ds. (18.11)

一个 ℱ_t-可测且连续的函数 x(·) 被称为方程 (18.8) 的温和解，如果 x(0)=x₀ 且以下积分方程

x(t)=U(t,0;x)x₀+∫₀ᵗ U(t,s;x)Bu(s)ds+∫₀ᵗ U(t,s;x)f(s,x(s))ds  
+U(t,0)∫₀ᵗ ΦdW(θ)+∫₀ᵗ U(t,s)A(s,x(s))(∫ₛᵗ ΦdW(θ))ds  
(18.12)

成立。

**引理 18.1.** 设 τ_N 为 (18.10) 中定义的停时。设 Ba⊂X 且 {A(t,b), (t,b)∈I×Ba} 为满足 (H7)–(H9) 的算子族。存在常数 C 使得对任意 x₁,x₂∈L₂^s(Ω,C(I,X)) 取值于 Ba 且任意 y∈Y，我们在 Ω 上逐点有，

‖U_{x₁}(t,s)y−U_{x₂}(t,s)y‖ₓ² ≤ C T‖y‖_Y² ∫ₛᵗ ‖x₁(r)−x₂(r)‖ₓ² dr,

(18.13)

其中 C 仅依赖于 {A(t,b)} 和 {Ã(t,b)} 的稳定性常数。

## 18.5 可控性结果

为研究可控性问题，我们假设以下条件。

-   (H12) 算子 B:U→X 为有界线性算子满足 ‖B‖²_{ℒ(U,Y)} ≤ K₂。
-   (H13) 设

    10 N T²‖x₀‖_Y² (1+5 T N² e^{2 N T} K₂ K) ≤ 1/2,

    25 T N² e^{2 N T} K₂ K(E‖x₁‖ₓ² + a) + 5 a ≤ r/2,

    其中

    a = 2E‖U(t,0;x₀)x₀ − x₀‖ₓ² + N² e^{2 N T}‖Φ‖²_{L₂(H,Y)} + T² N³ e^{2 N T}[1 + ‖Φ‖²_{L₂(H,Y)}]

-   (H14) 设

    ρ₂ = 5b(1 + 2 T⁴ N K₂ K),

    其中 b = N T²‖x₀‖_Y² + T⁴ N² + 2 T² N³ e^{2 N T} + N T³ M₁ + T⁵ N² M₁ + 2 T² N³ e^{2 N T} M₁ 满足 0 < ρ₂ < 1。

**定理 18.3.** 若假设 (H7)–(H14) 成立且 ‖x₀‖_Y²<∞ a.s. 则方程 (18.8) 在 I 上完全可控。

*证明.* 设 x₁∈ L₂(Ω,ℱ_T,X) 为任意点。定义算子 Λ 在取值于 Ba 的 L₂^ℱ(Ω,C(I,X)) 函数上为

```
\[
\Lambda x(t)=U(t,0;x)x_0+\int_0^tU(t,s;x)Bu(s)\,ds+\int_0^tU(t,s;x)f(s,x(s))\,ds
\]
\[
\qquad +U(t,0;x)\int_0^t\Phi\,dW(\theta)+\int_0^tU(t,s;x)A(s,x(s))\left(\int_s^t\Phi\,dW(\theta)\right)ds.
\tag{18.14}
\]
```

其中控制变量 u(·) 使用假设 (H8) 定义为

```
\[
u(t)=\mathcal{W}_{\bar T}^{-1}\left[x_1-U(\bar T,0;x)x_0-\int_0^{\bar T}U(\bar T,s;x)f(s,x(s))\,ds-U(\bar T,0;x)\int_0^{\bar T}\Phi\,dW(\theta)
\right.
\]
\[
\left.\qquad-\int_0^{\bar T}U(\bar T,s;x)A(s,x(s))\left(\int_s^{\bar T}\Phi\,dW(\theta)\right)ds\right].
\tag{18.15}
\]
```

显然 Λ x(t) 是 ℱ_t-适应的，我们现在证明 Λ 将取值于 Ba 的 L₂(Ω,C(I,X)) 中的函数映射到自身。

```
\[
\begin{aligned}
\|\Lambda x(t)-x_0\|_X^2\leq{}&5\left(\|U(t,0;x)x_0-x_0\|_X^2+\left\|\int_0^tU(t,s;x)Bu(s)\,ds\right\|_X^2\\
&+\left\|\int_0^tU(t,s;x)f(s,x(s))\,ds\right\|_X^2+\left\|U(t,0;x)\int_0^t\Phi\,dW(\theta)\right\|_X^2\\
&+\left\|\int_0^tU(t,s;x)A(s,x(s))\left(\int_s^t\Phi\,dW(\theta)\right)ds\right\|_X^2\right)\\
\leq{}&5\left(2\|U(t,0;x)x_0-U(t,0,x_0)x_0\|_X^2+2\|U(t,0,x_0)x_0-x_0\|_X^2\\
&+\|U(t,0;x)\|_{L(X,X)}^2\left\|\int_0^{\bar T}\Phi\,dW(\theta)\right\|_Y^2+\sup_{0\leq s\leq \bar T}\|U(t,s;x)\|_{L(X,X)}^2\|B\|_{\mathcal L(U,X)}^2\\
&\times\int_0^t\|u(s)\|_U^2\,ds+\bar T^2\sup_{0\leq s\leq \bar T}\|U(t,s;x)\|_{L(X,X)}^2\left[\sup_{t\in I}\|f(t,x(t))\|_X^2\\
&+\sup_{t\in I}\|A(t,x(t))\|_{L(Y,X)}^2\left\|\int_0^{\bar T}\Phi\,dW(\theta)\right\|_Y^2\right]\right).
\end{aligned}
\]
```

使用引理 18.1 对第一项以及 (H9)、(H10)、(H12) 和 (P1) 对其他项的界假设，我们得到

$$\le 5\Bigg(2C\tilde T\|x_0\|_Y^2\int_0^{\tilde T}\|x(s)-x_0\|_X^2\,ds+2\|U(t,0;x_0)x_0-x_0\|_X^2$$

$$\qquad +M^2e^{2\beta\tilde T}\left\|\int_0^{\tilde T}\Phi\,dW(\theta)\right\|_Y^2+M^2e^{2\beta\tilde T}K_2\sup_{t\in I}\int_0^t\|u(s)\|_U^2\,ds$$

$$\qquad +\tilde T^2M^2e^{2\beta\tilde T}\left[C_3+C_2\left\|\int_0^{\tilde T}\Phi\,dW(\theta)\right\|_Y^2\right]\Bigg).$$

使用停时定义在方程 (18.10) 中我们看到随机变量 $C$, $M$, $\beta$, $C_2$, $C_3$ 被 $N$ 所界。进一步使用事实 $\tilde T\le T$ 以及假设 $\|x_0\|_Y<\infty$ a.s. 我们有

$$\mathbb E\sup_{t\in I}\|\Lambda x(t)-x_0\|_X^2\le 5\Bigg(2NT^2\|x_0\|_Y^2\,\mathbb E\sup_{t\in I}\|x(t)-x_0\|_X^2$$

$$\qquad +2\mathbb E\|U(t,0;x_0)x_0-x_0\|_X^2$$

$$\qquad +N^2e^{2NT}\mathbb E\left\|\int_0^{\tilde T}\Phi\,dW(\theta)\right\|_Y^2+N^2e^{2NT}K_2\mathbb E\int_0^{\tilde T}\|u(s)\|_U^2\,ds$$

$$\qquad +T^2N^3e^{2NT}\left[1+\mathbb E\left\|\int_0^T\Phi\,dW(\theta)\right\|_Y^2\right]\Bigg).$$

使用 Itô 等距性我们有

$$\mathbb E\sup_{t\in I}\|\Lambda x(t)-x_0\|_X^2\le 5\Bigg(2NT^2\|x_0\|_Y^2\,\mathbb E\sup_{t\in I}\|x(t)-x_0\|_X^2$$

$$\qquad +2\mathbb E\|U(t,0;x_0)x_0-x_0\|_X^2$$

$$\qquad +N^2e^{2NT}\|\Phi\|_{L_2^0(H,Y)}^2+TN^2e^{2NT}K_2\mathbb E\int_0^{\tilde T}\|u(s)\|_U^2\,ds$$

$$\qquad +T^2N^3e^{2NT}\left[1+\|\Phi\|_{L_2^0(H,Y)}^2\right]\Bigg)$$

$$\le 5\Bigg(2NT^2\|x_0\|_Y^2\,\mathbb E\sup_{t\in I}\|x(t)-x_0\|_X^2$$

$$\qquad +TN^2e^{2NT}K_2\mathbb E\int_0^{\tilde T}\|u(s)\|_U^2\,ds+a\Bigg).$$

使用引理 18.1 我们有

≤ 5( C T̃² ‖x₀‖²_Y ∫ₛᵗ ‖x₁(r) − x₂(r)‖²_X dr + 4 T̃² C ‖B‖²_{ℒ(U,Y)} ∫₀ᵗ ∫ₛᵗ ‖x₁(r)−x₂(r)‖² ‖u(s)‖²_{U} dr ds + 2 T̃² C sup_{t∈I} ‖f(t,x(t))‖²_Y ∫₀^{T̃} ∫ₛᵗ ‖x₁(r)−x₂(r)‖²_X dr ds + 2 T̃² L₂ sup_{s,t∈Δ} ‖U(t,s,x₂)‖²_{ℒ(X,X)} sup_{t∈I} ‖x₁(t)−x₂(t)‖²_X + C T̃ ∫ₛᵗ ‖x₁(r)−x₂(r)‖²_X dr ‖∫₀ᵗ Φ dW(θ)‖²_Y + 2 T̃² C sup_{t∈I} ‖A(t,x(t))‖²_{ℒ(Y,X)} sup_{t,s∈Δ} ‖∫ₛᵗ Φ dW(θ)‖²_Y ∫₀^{T̃} ∫ₛᵗ ‖x₁(r)−x₂(r)‖²_X dr ds + 2 T̃² L₃ sup_{s,t∈Δ} ‖U(t,s,x₂)‖²_{ℒ(X,X)} sup_{s,t∈Δ} ‖∫ₛᵗ Φ dW(θ)‖²_Y sup_{t∈I} ‖x₁(t)−x₂(t)‖²_X ).

使用假设 (H9)、(H10)、(H11)、(H12) 和性质 (P1) 我们有

E sup_{t∈I} ‖Λx₁(t)−Λx₂(t)‖²_X ≤ 5 E( C T̃² ‖x₀‖²_Y + 4 T̃² C K₂ ∫₀^{T̃} ‖u(s)‖²_{U} ds + T̃⁴ C C₃ + 2 T̃² L₂ M² e^{2β T̃} + C T̃² ‖∫₀^{T̃} Φ dW(θ)‖²_Y + T̃⁴ C C₂ ‖∫₀^{T̃} Φ dW(θ)‖²_Y + 2 T̃² L₃ M² e^{2β T̃} ‖∫₀^{T̃} Φ dW(θ)‖²_Y ) E sup_{t∈I} ‖x₁(t)−x₂(t)‖²_X ≤ 5b(1+2 T⁴ N K₂ K) E sup_{t∈I} ‖x₁(t)−x₂(t)‖²_X ≤ ρ₂ E sup_{t∈I} ‖x₁(t)−x₂(t)‖²_X.

故由压缩映射原理，Λ 在 L²₂(Ω, C(I, X)) 中取值于 Ba 具有唯一不动点 x，它是拟线性随机微分系统的解

+   16. Kim, J.U.：随机波动方程的近似可控性。*应用数学与优化* **49**(1), 81–98 (2004)。
+   17. Da Prato, G.，Zabczyk, J.：*无穷维随机方程*。剑桥大学出版社，剑桥 (1990)。
+   18. Pazy, A.：*线性算子半群及其在偏微分方程中的应用*。施普林格出版社，纽约 (1983)。
+   19. Pronk, M.，Veraar, M.：具有适应漂移的随机演化方程的一种新方法。*微分方程期刊* **256**(11), 3634–3683 (2014)。

# 19 非均质介质中不同渗流速度模式下的对流-弥散方程

Amit Kumar Pandey 和 Mritunjay Kumar Singh

## 目录

-   19.1 引言............................................................................... 291
-   19.2 带线性等温线的对流-弥散方程....................................... 293
-   19.2.1 数值取值、结果与讨论.................................................... 299
-   19.2.2 正弦速度模式..................................................................... 299
-   19.3 正弦速度模式下的浓度分布 ...................... 299
-   19.4 指数递减速度模式下的浓度分布....... 304
-   19.5 指数递增速度模式下的浓度分布....... 305
-   19.6 结论................................................................................... 307
-   参考文献........................................................................................... 307

## 19.1 引言

就土壤介质中溶质运移相关信息而言，过去四五十年间已涌现出大量文献。重金属、农药、农业废弃物以及因工业持续增长而产生的废料向下游迁移，加上需要开挖地表的工程建设导致地球承载能力下降，都是影响地下水环境的一些主要因素。溶质运移不仅取决于土壤含水层复杂的水文地质结构，还取决于溶质颗粒的异常行为，正是这种行为导致了溶质扩散过程的发生。人们为建立确定性/随机性数学模型以观测天然地质构造中污染物的时空分布付出了巨大努力。输运介质的非均质性会使溶质在空间或时间依赖的弥散和渗流速度作用下发生扩散。渗流速度的变化源于水力传导度的变化。与水力传导度相比，孔隙度的空间变化相对较小；因此，在溶质运移过程中，为便于数值计算，通常假定孔隙度均匀。
