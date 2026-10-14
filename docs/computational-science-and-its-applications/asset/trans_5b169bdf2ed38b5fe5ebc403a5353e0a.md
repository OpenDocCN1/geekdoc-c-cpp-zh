

-Δ_g u + k_g = k_g e^{2u} on M

因此如果我们想知道给定的函数 k : M → ℝ 是否为共形度量的高斯曲率，等价于证明 PDE

-Δ_g u + k_g = k e^{2u} on M

是否有解。该 PDE 的解是能量泛函的临界点：

J(u) = 1/2 ∫_M |∇_g u|^2 dV_g + ∫_M k_g u dV_g - 1/2 ∫_M k e^{2u} dV_g  (9.6)

定义在适当的函数空间上。另一个出现类似非线性类型的方程是平均场方程：设 (M, g) 为二维紧致黎曼流形，则在一定假设下平均场方程化为

-Δ_g u = λ ( k e^{u} / ∫_M k e^{u} dV_g - 1 / Vol(M) ) on M

其中 k : M → ℝ 为给定。相应的能量为：

J(u) = 1/2 ∫_M |∇_g u|^2 dV_g + λ/Vol(M) ∫_M u dV_g - λ/2 log( ∫_M k e^{2u} dV_g )

上述例子表明，如果我们需要能量在自然空间中定义，则需要利用 ∫_M |∇_g u|^2 dV_g 来估计形如 ∫_M e^{2u} dV_g 的项。事实上这类估计是可用的，其最优版本被称为 Moser–Trudinger 不等式。该不等式的高阶版本被称为 Adams 不等式。我们将在下一节详细讨论这些不等式。

## 9.2 预备知识

在本节中我们将回顾一些基本定义和标准结果。

我们用 D^α 表示微分算子

D^α = ∂^{|α|} / ∂x_1^{α_1} ... ∂x_n^{α_n}

对应于多指标 α = (α_1, ..., α_n)，其中 |α| = α_1 + ... + α_n。

我们用 C_c^k(Ω) 表示在 Ω 中具有紧支集且所有阶数不超过 k 的偏导数均存在且连续的函数集合。我们还记 C_c^∞(Ω) = ∩_{k=1}^∞ C_c^k(Ω)。

### 定义 9.1 设 Ω 为 ℝ^n 中的开集，我们对 1 ≤ p ≤ ∞ 和 k ∈ ℕ 定义 Sobolev 空间 W^{k,p}(Ω) 和 W_0^{k,p}(Ω) 为

W^{k,p}(Ω) = { u ∈ L^p(Ω) : D^α u ∈ L^p(Ω), ∀ α with |α| ≤ k }

以及

W_0^{k,p}(Ω) = closure of C_c^∞(Ω) in W^{k,p}(Ω)

其中 W^{k,p}(Ω) 配备范数 ||·||_{k,p} 给出为

|| u ||_{k,p} = Σ_{|α| ≤ k} || D^α u ||_{L^p}

当 p = 2 时我们记

W^{k,2}(Ω) = H^k(Ω), W_0^{k,2}(Ω) = H_0^k(Ω)

有了这些定义我们可以陈述 Sobolev 嵌入定理：

### 引理 9.1 设 Ω 为 ℝ^n 中的有界域且 kp < n，则

W^{k,p}(Ω) ↪ L^q(Ω), 1 ≤ q ≤ np / (n - kp)

当 kp = n 时

W^{k,p}(Ω) ↪ L^q(Ω), 1 ≤ q < ∞

但 W^{k,p}(Ω) ↪̸ L^∞(Ω)

我们也回顾众所周知的 Poincaré 引理：

### 引理 9.2 设 Ω 为 ℝ^n 中的有界域，则存在仅依赖于 Ω 的常数 C 使得

C ∫_Ω |u|^p dx ≤ ∫_Ω |∇u|^p dx, ∀ u ∈ W_0^{1,p}(Ω).

作为推论我们得到

### 推论 9.1 设 Ω 为 ℝ^n 中的有界域，则 (∫_Ω |∇u|^p dx)^{1/p} 是 W_0^{1,p}(Ω) 中的等价范数。

## 9.3 Moser–Trudinger

Moser–Trudinger 不等式处理的是 $W_0^{1,n}(\Omega)$ 嵌入的情况。我们知道

$$W_0^{1,n}(\Omega)\hookrightarrow L^q(\Omega),\ 1\le q<\infty$$

且该结果对 $q=\infty$ 不成立。现在问题是是否可以将该空间嵌入到更好的空间。为解释此点，首先注意 $W_0^{1,n}(\Omega)\hookrightarrow L^q(\Omega)$ 当且仅当存在 $C>0$ 使得

$$\left[\int_\Omega |u|^p\,dx\right]^{\frac np}\le C\int_\Omega |\nabla u|^n\,dx,\quad u\in C_c^\infty(\Omega)$$

等价地

$$\sup_{u\in C_c^\infty(\Omega),\ \int_\Omega |\nabla u|^n\le1}\int_\Omega |u|^q\,dx\le C, \tag{9.7}$$

现在可以问是否可以将函数 $|u|^q$ 替换为增长高于多项式幂的某个 $f(u)$。Pohožaev ([1]) 和 Trudinger([2]) 对此问题给出了答案。他们建立了 Sobolev 空间 $W_0^{1,n}(\Omega)$ 到 Orlicz 空间的嵌入，建立了这些函数的指数可积性。

1971 年 J. Moser ([3]) 在试图研究在球面上规定高斯曲率的问题时，认识到需要建立 Pohožaev 和 Trudinger 所得嵌入的尖锐形式。他证明了：

### **定理 9.1** *(Moser, [3])*

存在仅依赖于 $n$ 的正常数 $C_0$ 使得

$$\sup_{u\in C_c^\infty(\Omega),\ \int_\Omega |\nabla u|^n\le1}\int_\Omega e^{\alpha|u|^{\frac n{n-1}}}\,dx\le C_0\,|\Omega|. \tag{9.8}$$

对所有 $\alpha\le\alpha_n=n[\omega_{n-1}]^{\frac1{n-1}}$ 成立，其中 Ω 是 ℝ^n 中的有界域，$|\Omega|$ 表示 Ω 的体积，$\omega_{n-1}$ 表示球面 $S^{n-1}$ 的 $n-1$ 维面积。而且当 $\alpha>\alpha_n$ 时，上述上确界为无穷。

上述不等式对 $\alpha\le\alpha_n$ 的证明使用了对称化并将问题化为一维不等式。$\alpha<\alpha_n$ 的情形比 $\alpha=\alpha_n$ 的情形更容易。$\alpha>\alpha_n$ 的情形使用以下我们称为 Moser 函数的试验函数证明：对 $0<l<R<\infty$，定义

$$u_{R,l}(r)=\frac1{\sqrt{2\pi}}\left[\sqrt{\log\left(\frac Rl\right)}\,\chi_{(0,l)}+\left(\log\frac Rl\right)^{-\frac12}\log\left(\frac rR\right)\chi_{[l,R]}\right]$$

Ω 不应包含任意大半径的球，即

```
IR_Ω := sup{r > 0 : B(x, r) ⊂ Ω, for some x ∈ Ω} < ∞
```

作为上述定理的推论，我们证明了当 Ω 为单连通时这些条件是等价的。

### 定理 9.4 (G. Mancini, K. Sandeep [16])

设 Ω 为 ℝ² 中的单连通开集，则以下条件等价：

- Moser–Trudinger 不等式 (式 (9.12)) 在 Ω 中成立。
- λ₁(Ω) > 0
- IR_Ω < ∞.

去掉单连通性时定理不成立

容易证明 (i) ⇒ (ii) ⇒ (iii)。因此只需证明 (iii) ⇒ (i)。由于 Ω 是单连通的，它与单位圆盘共形等价，因此可以将不等式拉回到单位圆盘，拉回后的不等式类似于式 (9.11)，然后前述定理适用，因为可以证明利用 Kobe 的四分之一定理，(iii) 意味着拉回度量被 Poincaré 度量从上方控制（详见 [16]）。

尽管该定理对非单连通域不成立，但人们可以问在一般情形下 (i) 和 (ii) 是否等价。该问题在 [17] 中被肯定地回答。

## 9.4 Adams 不等式

Adams 不等式是 Moser–Trudinger 型不等式在高阶 Sobolev 空间 W₀^{k,p}(Ω) 中的推广，其中 kp = n。尽管人们期望类似的不等式对高阶 Sobolev 空间成立，但如何将 k = 1 的情形的证明推广到 k > 1 并不明显，这是由于高阶梯度 ∇ᵏ 定义的 Polya–Szego 型不等式失效

```
∇ᵏ := { Δ^{k/2}, if k is even,
∇Δ^{(k-1)/2}, if k is odd. } (9.13)
```

在重要工作中，D.R. Adams ([22]) 建立了当 kp = n 时高阶 Sobolev 空间 W₀^{k,p}(Ω) 的尖锐嵌入。

### 定理 9.5 (Adams [22])

对所有 β ≤ β₀(k, n) 成立，其中 p = n/k, p′ = p/(p − 1), β₀(k, n) = { n/ωₙ₋₁ [π^(n/2) 2^k Γ((k+1)/2)]^p′ / Γ((n−k+1)/2) , if k is odd, n/ωₙ₋₁ [π^(n/2) 2^k Γ(k/2)]^p′ / Γ((n−k)/2) , if k is even, } (9.15)

此外，若 β > β₀，则式 (9.14) 中的上确界为无穷。

上述形式的等式称为 Adams 不等式。如前所述，尽管 Adams 的陈述看起来与 Moser–Trudinger 相似，但证明截然不同。Adams 使用 Riesz 变换将其转化为卷积型估计，然后使用 O’Neil 关于函数非增重排的卷积算子的引理来证明结果。随后 Fontana 在 [15] 中得到了紧致黎曼流形上式 (9.14) 的以下尖锐版本：

### 定理 9.6 (Fontana [15]) 设 (M, g) 为无边界的 n 维紧致黎曼流形，k 为小于 n 的正整数，则存在常数 c₀ = c₀(k, M) 使得

sup_{u∈C^k(M), ∫_M u=0, ∫_Ω |∇_g^k u|^p′ ≤1} ∫_M e^{β|u(x)|^{p′}} dx ≤ c₀ (9.16)

若 β ≤ β₀(k, n)，其中 p, p′, ∇_g^k 如上，其中 ∇_g 和 Δ_g 分别为关于度量 g 的梯度和 Laplace Beltrami 算子。此外，若 β > β₀，则式 (9.16) 中的上确界为无穷。

由于 Moser–Trudinger 不等式在双曲空间中成立，一个自然的问题是双曲空间中是否具有 Adams 不等式。Fontana 和 Morpurgo 给出了答案：

### 定理 9.7 (Fontana and Morpurgo,[23]) 设 1 ≤ k < n 则 Adams 不等式

sup_{u∈C^k_c(H^n), ∫_{H^n} |∇_g^k u|^p′ ≤1} ∫_{H^n} Exp_{[p−1]}(β |u(x)|^{p′}) dx < ∞, (9.17)

在 n 维双曲空间 H^n 中成立当且仅当 β ≤ β₀(k, n)，其中 [p − 1] 表示 p − 1 的整数部分且 Exp_m(x) = e^x − Σ_{i=1}^m x^i / i!

我们也在 [24] 中对双曲空间中的 Adams 不等式采取了另一种方法。回顾 Moser 证明式 (9.8) 中尖锐版本的原始动机

