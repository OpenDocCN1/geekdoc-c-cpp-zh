

‖A(t, b₁) − A(t, b₂)‖²_{𝕃(Y,X)} ≤ L₃ ‖b₁ − b₂‖²_X

对所有 t ∈ J 和 b₁, b₂ ∈ Ba 成立。

-   (H10) 非线性函数 f: J × X → X 满足 (H2)，其 Lipschitz 常数为 L₂，并且存在常数 C₃ > 0 使得对所有 b ∈ Ba，‖f(t, b)‖²_Y ≤ C₃。

-   (H11) 算子 Φ ∈ 𝕃₂⁰(H, Y)。

由 (H11) 可得 ‖∫₀^τ̃ Φ dW(θ)‖²_Y 几乎必然有界，使用 Markov 不等式并记为 M₁。令停时序列 τ_N 定义为，

τ_N := inf_{t≥0} {t: M ∨ β ∨ C₂ ∨ C₃ ∨ L₂ ∨ L₃ ∨ M₁ ∨ C ≥ N}, (18.10)

其中常数 C 在引理 18.1 中出现之后给出，且我们假设 τ_N > 0。由于 x(·) 是随机的，假设中的常数 M, β, C₂, C₃, L₂, L₃, M₁ 不仅依赖于 𝔹 的参数，还依赖于来自停时的 N。我们用记号 T̃ = T ∧ τ_N 和 I 表示时间区间 [0, T̃] ⊂ J。

我们现在给出随机演化系统的定义并给出其存在性。

## 定义 18.5. 一个有界线性算子 U(t,s), 0 ≤ s ≤ t ≤ T̃, 在 X 上的二参数族称为演化系统，如果满足以下两个条件：

-   (i) U(s,s)=I（恒等算子），U(t,r)U(r,s)=U(t,s) 对 0 ≤ s ≤ r ≤ t ≤ T̃。

-   (ii) (t,s) ↦ U(t,s) 对 0 ≤ s ≤ t ≤ T̃ 强连续。

## 定理 18.2. 设 τ_N 为 (18.10) 中定义的停时。设 Ba ⊂ X 且 {A(t,b)}, (t,b) ∈ I × Ba 为满足 (H7)–(H9) 的算子族。若 x ∈ L²_𝔽(Ω, C(I,X)) 则存在唯一的随机演化系统 {U(t,s;x)} := {U(t,s,(x(r,ω))_{r≤t})} 定义在三角形 Δ := {0 ≤ s ≤ t ≤ T̃} 上，满足以下性质在 Ω 上逐点成立。

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

引理 18.1. 设 τ_N 为 (18.10) 中定义的停时。设 Ba⊂X 且 {A(t,b), (t,b)∈I×Ba} 为满足 (H7)–(H9) 的算子族。存在常数 C 使得对任意 x₁,x₂∈L₂^s(Ω,C(I,X)) 取值于 Ba 且任意 y∈Y，我们在 Ω 上逐点有，

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

## **定理 18.3.** 若假设 (H7)–(H14) 成立且 ‖x₀‖_Y²<∞ a.s. 则方程 (18.8) 在 I 上完全可控。

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

