

[I₂ 表示 2 × 2 单位矩阵]，并利用 (2.12) 可得

(2.16) \[\tilde{\Psi}(x,k)=\tilde{\Phi}(x,k)=\begin{cases}e^{xA_{+}(k)},&\text{for }x>0,\\e^{xA_{-}(k)},&\text{for }x<0.\end{cases}\]

由 (2.16) 并结合 (2.15) 和 (2.10)，我们得到

\[S(k)=\begin{pmatrix}a(k)&\bar b(k)\\b(k)&\bar a(k)\end{pmatrix}=W_{+}^{-1}(k)W_{-}(k)=\frac{\lambda+k}{2\lambda}\begin{pmatrix}1-\frac{q_{+}q_{-}^{*}}{(\lambda+k)^{2}}&i\frac{(q_{+}-q_{-})}{\lambda+k}\\i\frac{(q_{-}^{*}-q_{+}^{*})}{\lambda+k}&1-\frac{q_{-}q_{+}^{*}}{(\lambda+k)^{2}}\end{pmatrix}.\]

令 λ = iℓ，其中 ℓ ∈ (0, q₀)，由上式可得：

\[a(k)=\frac{(k+i\ell)^{2}-q_{0}^{2}e^{i(\theta_{+}-\theta_{-})}}{2i\ell(k+i\ell)}=\frac{k^{2}-\ell^{2}-q_{0}^{2}\cos(\theta_{+}-\theta_{-})+i\left(2k\ell-q_{0}^{2}\sin(\theta_{+}-\theta_{-})\right)}{2i\ell(k+i\ell)}.\]

于是 a(k)=0 当且仅当

(2.17) \[\cos(\theta_{+}-\theta_{-})=\frac{k^{2}-\ell^{2}}{q_{0}^{2}},\qquad \sin(\theta_{+}-\theta_{-})=\frac{2k\ell}{q_{0}^{2}}.\]

除非 q₊ = q₋，方程 (2.17) 在 (−q₀, q₀) 内有唯一解 k₀。 该特征值 k₀ = 0 当且仅当 θ₊ − θ₋ 是 π 的奇数倍。

从现在起，我们用 k₀ 表示与散射问题 (1.3) 相关联的自由哈密顿算子的唯一离散特征值，并在上面的例子中计算得到。

## 3. 自由哈密顿量的解析式

本节计算自由哈密顿量 H_f 的解析式 (k − H_f)⁻¹。 所得结果将在下一节用于确定离散特征值的位置。

设 k ∉ σ(H_f) = Σ ∪ {k₀} 若 q₊ ≠ q₋ [或 k ∉ σ(H_f) = Σ 若 q₊ = q₋]，我们计算自由哈密顿量的解析式 (k − H_f)⁻¹。 令 F(x) 为 L²(ℝ)² = L²(ℝ) ⊕ L²(ℝ) 中的列向量函数，我们寻求 L²(ℝ)² 中的唯一向量函数 Ψ(k, x)，使得 H_f Ψ = k Ψ − F。 写 Ψ(x, k) = W(x, k) ψ(x, k)，其中 W(x, k) = W₊(k)θ(x) + W₋(k)θ(−x)，我们得到对 0 ≠ x ∈ ℝ

(3.1) \[\psi'(x,k)=-i\lambda\sigma_{3}\psi(x,k)+iW^{-1}(x,k)\sigma_{3}F(x),\]

其中我们利用了 A(x,k)W(x,k) = −iλW(x,k)σ₃。

### THEOREM 3.1. 设 q₊ ≠ q₋ 且 k ∈ ℂ⁺。 则对 F ∈ L²(ℝ)² 且 k ∉ Σ ∪ {k₀} 有

(3.2) \[[(k-H_f)^{-1}F](x)=\int_{-\infty}^{\infty}dy\,[K_f(x,y;k)+K_{f1}(x;k)K_{f2}(y;k)]F(y),\]

其中 $K_f(x,y;k)$ 由

(3.3a) $K_f(x,y;k)=\begin{cases}-i\,e^{i\lambda(y-x)}W_{+}(k)\begin{pmatrix}1&0\\0&0\end{pmatrix}\sigma_3W_{+}^{-1}(k)\sigma_3,&y>x>0,\\-i\,e^{i\lambda(x-y)}W_{+}(k)\begin{pmatrix}0&0\\0&1\end{pmatrix}\sigma_3W_{+}^{-1}(k)\sigma_3,&x>y>0,\\-i\,e^{i\lambda(y-x)}W_{-}(k)\begin{pmatrix}1&0\\0&0\end{pmatrix}\sigma_3W_{-}^{-1}(k)\sigma_3,&0>y>x,\\-i\,e^{i\lambda(x-y)}W_{-}(k)\begin{pmatrix}0&0\\0&1\end{pmatrix}\sigma_3W_{-}^{-1}(k)\sigma_3,&0>x>y,\\0,&xy<0,\end{cases}$

(3.3b) $K_{f1}(x;k)=\begin{cases}e^{i\lambda x}\begin{pmatrix}0&0\\0&1\end{pmatrix}W_{+}^{-1}(k),&x>0,\\e^{-i\lambda x}\begin{pmatrix}1&0\\0&0\end{pmatrix}W_{-}^{-1}(k),&x<0,\end{cases}$

(3.3c) $K_{f2}(y;k)=\begin{cases}-i\,e^{i\lambda y}Z^{-1}(k)\begin{pmatrix}1&0\\0&0\end{pmatrix}W_{+}^{-1}(k)\sigma_3,&y>0,\\i\,e^{-i\lambda y}Z^{-1}(k)\begin{pmatrix}0&0\\0&1\end{pmatrix}W_{-}^{-1}(k)\sigma_3,&y<0,\end{cases}$

(3.3d) $Z(k)=\begin{pmatrix}1&0\\0&0\end{pmatrix}W_{+}^{-1}(k)+\begin{pmatrix}0&0\\0&1\end{pmatrix}W_{-}^{-1}(k)=\frac{1}{2\lambda}\begin{pmatrix}\lambda+k&i q_r\\-i q_l^{*}&\lambda+k\end{pmatrix}.$

若 $q_{+}=q_{-}\neq0$，则对 $k\notin\Sigma$

(3.4) $[(k-H_f)^{-1}F](x)=-i\int_{-\infty}^{\infty}dy\,e^{i\lambda|x-y|}W_{+}(k)E(y-x)W_{+}^{-1}(k)\sigma_3F(y), $

其中

$E(w)=\theta(w)\begin{pmatrix}1&0\\0&0\end{pmatrix}+\theta(-w)\begin{pmatrix}0&0\\0&-1\end{pmatrix}.$

类似的结果也可以在 $k\in\mathbb{K}^{-}$（或 $\lambda\in\Lambda^{-}$）时证明。

Proof. 设 $q_{+}\neq q_{-}$。 则 (3.1) 蕴含恒等式

$\frac{\partial}{\partial y}\left\{e^{-i\lambda(x-y)\sigma_3}\psi(y,k)\right\}=i\,e^{-i\lambda(x-y)\sigma_3}W^{-1}(y,k)\sigma_3F(y),$

其中 $0\neq y\in\mathbb{R}$ 且 $k\notin\Sigma$。 因此，对 $0\neq y\in\mathbb{R}$ 且 $k\notin\Sigma$ 我们得到

(3.5a) $\frac{\partial}{\partial y}\left\{e^{i\lambda(y-x)}\begin{pmatrix}1&0\\0&0\end{pmatrix}\psi(y,k)\right\}=i\,e^{i\lambda(y-x)}\begin{pmatrix}1&0\\0&0\end{pmatrix}W^{-1}(y,k)\sigma_3F(y),$

(3.5b) $\frac{\partial}{\partial y}\left\{e^{i\lambda(x-y)}\begin{pmatrix}0&0\\0&1\end{pmatrix}\psi(y,k)\right\}=i\,e^{i\lambda(x-y)}\begin{pmatrix}0&0\\0&1\end{pmatrix}W^{-1}(y,k)\sigma_3F(y).$

设 $k$ 属于 $\mathbb{K}^{+}$ [或 $\lambda\in\Lambda^{+}$]，并对 $x\ge0$ 将 (3.5a) 关于 $y\in(x,+\infty)$ 积分，对 $x<0$ 关于 $y\in(x,0)$ 积分；对 $x\le0$ 将 (3.5b) 关于 $y\in(-\infty,x)$ 积分，对 $x>0$ 关于 $y\in(0,x)$ 积分。 把对 $x>0$ 和 $x<0$ 分别得到的结果合并，我们得到 [Ψ(x, k) 在 x = 0 处连续但 ψ(x, k) 不连续]

(3.6a) Ψ(x, k) = −iW₊(k) ∫ₓ^∞ dy e^{iλ(y−x)} (1 0; 0 0) W₊⁻¹(k)σ₃F(y) + iW₊(k) ∫₀ˣ dy e^{iλ(x−y)} (0 0; 0 1) W₊⁻¹(k)σ₃F(y) + e^{iλx}W₊(k) (0 0; 0 1) W₊⁻¹(k)Ψ(0, k) 对 x > 0，

(3.6b) = iW₋(k) ∫₋∞ˣ dy e^{iλ(x−y)} (0 0; 0 1) W₋⁻¹(k)σ₃F(y) − iW₋(k) ∫ₓ⁰ dy e^{iλ(y−x)} (1 0; 0 0) W₋⁻¹(k)σ₃F(y) + e^{−iλx}W₋(k) (1 0; 0 0) W₋⁻¹(k)Ψ(0, k) 对 x < 0，

(3.6c) = Z⁻¹(k) [ −i ∫₀^∞ dy e^{iλy} (1 0; 0 0) W₊⁻¹(k)σ₃F(y) + i ∫₋∞⁰ dy e^{−iλy} (0 0; 0 1) W₋⁻¹(k)σ₃F(y) ] 对 x = 0，

前提是矩阵 Z(k) 非奇异。 令 k ∈ (−q₀, q₀) 且 λ = iℓ，我们得到

(3.7) det Z(k) = [ℓ² − k² + q₀² cos(θ₊ − θ₋) + i[−2kℓ + q₀² sin(θ₊ − θ₋)]] / (4ℓ²)，

它只能在 (2.17) 成立时为零。 换句话说，在 q₊ ≠ q₋ 的情况下，我们必须排除离散特征值 k = k₀。

现在考虑 q₊ = q₋ 的情况。 写 Ψ(x, k) = W₊(k)ψ(x, k) 为 (3.4) 左边，我们验证它满足 Ψ′(x, k) = A₊(k)Ψ(x, k) + iσ₃F(x)。

并且公式 (3.4) 由 (3.3a)-(3.3d) 得出，如果考虑到 q₊ = q₋ 蕴含 W₊ = W₋，从而完成证明。

我们强调：

- a. 若 q₊ ≠ q₋，解析式算子 (k − H_f)⁻¹ 是对 k ∉ Σ 的积分算子，其积分核为 K_f(x, y; k)，加上对 k ∉ Σ ∪ {k₀} 的秩二算子；
- b. 若 q₊ = q₋，解析式算子 (k − H_f)⁻¹ 是积分算子，其积分核为 −i e^{iλ|x−y|}W₊(k)E(y − x)W₊⁻¹(k)σ₃。

## 4. 离散特征值的位置

本节的目的是刻画 (−q₀, q₀) 中离散特征值的位置。 事实上，例 2.1 显示如果 q₋ ≠ q₊ 至少存在一个这样的特征值。 我们模仿 Klaus 等人在 [14–16] 中对衰减势的聚焦 NLS 给出的证明来得到主要结果。 我们需要以下技术结果，即下面的定理 4.1 和 4.2。

### THEOREM 4.1. 设 W^(1)(x) 和 W^(2)(x) 是两个 2 × 2 矩阵，其元素属于 L^2(ℝ)，且 k ∉ Σ。 则在 L^2(ℝ)^2 上具有积分核

W^(1)(x) K_f(x, y; k) W^(2)(y)

的积分算子是希尔伯特-施密特算子，即使我们取 k 趋于 Σ 的内部点时的极限也是如此。

PROOF. W^(1)(k − H_f)^−1 W^(2) 减去秩二贡献的平方希尔伯特-施密特范数由

∫_{−∞}^{∞} dx ∫_{−∞}^{∞} dy ‖W^(1)(x)‖_{HS}^2 ‖W^(2)(y)‖_{HS}^2 |K_f(x, y; k)|^2

给出。 由于 K_f(x, y; k) 表达式中的指数因子 e^{iλ|x−y|} 的绝对值被 1 所限制，我们得到 W^(1)(k − H_f)^−1 W^(2) 减去秩二贡献的平方希尔伯特-施密特范数的以下上界：

(4.1)  k^2/λ^2 (∫_{−∞}^{∞} dx ‖W^(1)(x)‖_{HS}^2) (∫_{−∞}^{∞} dy ‖W^(2)(y)‖_{HS}^2)，

它对每个 ε > 0，在满足 √(|k^2 − q_0^2|) ≥ ε 的 k 下一致有界。

下面的定理是希尔伯特-施密特范数定义的一个直接推论。 在范数估计中，使用哪种酉等价的矩阵范数并不重要，因为 K_{f1}(x; k) 和 K_{f2}(y; k) 都是秩一的。

### THEOREM 4.2. 设 W^(1)(x) 和 W^(2)(x) 是两个 2 × 2 矩阵，其元素属于 L^2(ℝ)，且 k ∉ Σ。 则在 L^2(ℝ)^2 上具有积分核

W^(1)(x) K_{f1}(x; k) K_{f2}(y; k) W^(2)(y)

的积分算子是秩二的，其范数与

(4.2) [∫_{−∞}^{∞} dx ‖W^(1)(x) K_{f1}(x; k)‖^2]^{1/2} [∫_{−∞}^{∞} dy ‖K_{f2}(y; k) W^(2)(y)‖^2]^{1/2}

一致。

由 [14, Eq. (4.10)] 和 [16, proof of Thm. 4.2] 可知，核为 e^{−τ(y−x)}θ(y−x)√(m(x)m(y)) 的 L^2(ℝ) 上积分算子的范数小于 (2/π)‖m‖_1。 为了将该结果推广到非消失情形，我们从极分解开始

Q(x) − Q_f(x) = ( 0 σ(x); σ(x)* 0 ) √|q(x)−q_f(x)| I_2 · √|q(x)−q_f(x)| I_2
(4.3) = U_δ(x) |Δ(x)|^{1/2} |Δ(x)|^{1/2}，

其中
(4.4) q_f(x) = (q(x)−q_−)θ(−x) + (q(x)−q_+)θ(x),      Δ(x) = |q(x)−q_f(x)| I_2，
|σ(x)| = 1，且因此 U_δ(x) = ( 0 σ(x); σ(x)* 0 ) 是一个酉矩阵。 对 k ∉ Σ 我们现在定义

(4.5) 𝒲(k) = I + |Δ|^{1/2} (k − H_f)^{−1} U_δ |Δ|^{1/2}。

