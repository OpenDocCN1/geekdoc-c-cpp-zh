

$\tau$ 对块 $\mathcal{B}_i$ 和 $\mathcal{Q}$ 的作用给出了 $\tau$ 对点 $\mathcal{P}$ 的作用。根据引理 8.5.1，$A$ 在有理数上是非奇异的。因此 $AQA^{-1} = P^{-1} = P^t$，且 $Q$ 和 $P$ 有相同的迹。由于置换矩阵的不动点数等于矩阵的迹，结果得证。

## **推论 8.7.3** 对称 2-设计的自同构在块上的循环结构与其在点上的循环结构相同。

**证明：** 如果 $\alpha$ 和 $\tau$ 分别表示作用于块和点的同一个自同构，那么 $\alpha^t$ 和 $\tau^t$ 也是如此。设 $n_i$（分别 $n'_i$）为 $\sigma$（分别 $\tau$）的 $i$-循环的个数。如果 $i$ 是素数 $p$，则 $\sigma^t$（分别 $\tau^t$）的不动点个数为 $p \cdot n_p + n_1$（分别 $p \cdot n'_p + n'_1$）。由于根据定理 8.7.2 对 $\sigma$ 和 $\tau$ 得到 $n_1 = n'_1$，并且根据同一定理对 $\sigma^t$ 和 $\tau^t$ 得到 $p \cdot n_p + n_1 = p \cdot n'_p + n'_1$，故 $n_p = n'_p$。我们可以根据 $i$ 的素因子个数继续进行归纳。

## **练习 463** 补全推论 8.7.3 证明的细节。

我们现在准备引入差集的概念；这将与循环设计密切相关。设 $\mathcal{G}$ 为阶为 $v$ 的阿贝尔群。$\mathcal{G}$ 中的一个 $(v, k, \lambda)$ *差集* 是 $\mathcal{G}$ 中 $k$ 个不同元素的集合 $D$，使得多重集 $\{x - y \mid x \in D, y \in D, x \neq y\}$ 包含 $\mathcal{G}$ 中每个非零元素恰好 $\lambda$ 次。$D$ 中不同元素之间有 $k(k-1)$ 个差，这些差恰好 $\lambda$ 次构成 $\mathcal{G}$ 中所有非零元素。因此

$$k(k-1) = (v-1)\lambda. \tag{8.12}$$

我们将最感兴趣的是 $\mathcal{G}$ 为循环群 $\mathbb{Z}_v$ 的情况，在这种情况下差集是一个 *循环差集*。在定理 8.7.5 中，我们将看到差集与对称设计之间的联系。

## **例 8.7.4** 在 $\mathbb{Z}_7$ 中，集合 $D = \{1, 2, 4\}$ 是一个 $(7, 3, 1)$ 循环差集，这可以通过直接计算看出（练习 464）。通过将 $\mathbb{Z}_7$ 中的每个元素 $i$ 加到集合 $D$ 上，我们得到集合 $D_i = \{i+1, i+2, i+4\}$。这些构成了阶 2 的射影平面 $\mathcal{D}$ 的块。映射 $i \mapsto i+1 \pmod 7$ 是 Aut($\mathcal{D}$) 中的一个 7-循环。

## **练习 464** 证明在例 8.7.4 中：
- (a) $D = \{1, 2, 4\}$ 是一个 $(7, 3, 1)$ 循环差集，
- (b) 集合 $D_i = \{i+1, i+2, i+4\}$ 是阶 2 的射影平面 $\mathcal{D}$ 的块，且
- (c) 映射 $i \mapsto i+1 \pmod 7$ 是 Aut($\mathcal{D}$) 中的一个 7-循环。

## **练习 465** 证明：
- (a) $\{1, 3, 4, 5, 9\}$ 和 $\{2, 6, 7, 8, 10\}$ 是 $(11, 5, 2)$ 循环差集，且
- (b) $\{1, 5, 6, 8\}$ 和 $\{0, 1, 3, 9\}$ 是 $(13, 4, 1)$ 循环差集。

对于 $i \in \mathcal{G}$，定义移位 $g_i : \mathcal{G} \to \mathcal{G}$ 为 $zg_i = i + z$。可以很容易地看出，将 $g_i$ 应用于 $\mathcal{G}$ 中的一个差集会得到具有相同参数的差集。$\mathcal{G}$ 中一个 $(v, k, \lambda)$ 差集的移位构成了一个对称 $2-(v, k, \lambda)$ 设计，其自同构群中包含 $\mathcal{G}$。

## **定理 8.7.5** 设 $\mathbb{G}$ 为阶为 $v$ 的阿贝尔群，并设 $\mathcal{G} = \{g_i \mid i \in \mathbb{G}\}$。以下结论成立：
- (i) 设 $D$ 为 $\mathbb{G}$ 中的一个 $(v, k, \lambda)$ 差集。设 $D_i = \{i + \delta \mid \delta \in D\}$ 和 $\mathcal{B} = \{D_i \mid i \in \mathbb{G}\}$。那么 $\mathcal{D} = (\mathbb{G}, \mathcal{B})$ 是一个具有 $\mathcal{G} \le \text{Aut}(\mathcal{D})$ 的对称 $2-(v, k, \lambda)$ 设计。
- (ii) 如果 $\mathcal{D} = (\mathbb{G}, \mathcal{B})$ 是一个具有 $\mathcal{G} \le \text{Aut}(\mathcal{D})$ 的对称 $2-(v, k, \lambda)$ 设计，那么 $\mathcal{D}$ 的任意块 $D$ 都是 $\mathbb{G}$ 中的一个 $(v, k, \lambda)$ 差集，且 $\mathcal{B}$ 的块为 $D_i = \{i + \delta \mid \delta \in D\}$。

**证明：** 设 $D$ 为 $\mathbb{G}$ 中的一个 $(v, k, \lambda)$ 差集，$\mathcal{D} = (\mathbb{G}, \mathcal{B})$ 如所述。设 $i$ 和 $j$ 为 $\mathbb{G}$ 中的不同元素。根据定义，$i - j = x - y$ 对于 $D \times D$ 中不同元素的 $\lambda$ 对 $(x, y)$ 成立。那么 $i - x = j - y$；由于 $i \in i - x \in D_{i-x}$，且 $j = j - y + y = i - x + y \in D_{i-x}$，每对点至少在 $\lambda$ 个块中。根据 (8.12),

$$v \binom{k}{2} = \binom{v}{2} \lambda.$$

左边计算所有 $D_i$ 中不同元素对的个数，右边计算 $\mathbb{G}$ 中不同元素对的个数，每个重复 $\lambda$ 次。因此，在所有 $D_i$ 中没有一对出现超过 $\lambda$ 次。于是 $\mathcal{D}$ 是一个 $2-(v, k, \lambda)$ 设计；由于 $\mathbb{G}$ 有阶 $v$，$\mathcal{D}$ 有 $v$ 个块，因此是对称的。由于 $(D_i)g_i = D_{i+j}$，故 $\mathcal{G} \le \text{Aut}(\mathcal{D})$，从而证明 (i)。

对于逆命题，设 $D$ 为 $\mathcal{B}$ 中的任意块。那么 $D_i = \{i + \delta \mid \delta \in D\}$ 是 $D$ 在 $g_i$ 下的像，因此也在 $\mathcal{B}$ 中。首先假设对于某些 $i \neq j$ 有 $D_i = D_j$。那么 $D = D_m$，其中 $m = i - j \neq 0$，这意味着 $g_m$ 固定块 $D$。根据定理 8.7.2，$g_m$ 必须固定一个点。因此对于某些 $\ell \in \mathbb{G}$ 有 $m + \ell = \ell$，这与 $m \neq 0$ 矛盾。因此 $D_i$ 互不相同，并且由于 $\mathcal{G}$ 有阶 $v$，它们必定是全部 $v$ 个块。

设 $w$ 为 $\mathbb{G}$ 中的非零元素。那么 $0$ 和 $w$ 是不同的点，因此必须在 $\lambda$ 个块 $D_i$ 中。于是对于 $D$ 中的某些 $x$ 和 $y$，有 $0 = \ell + x$ 和 $w = \ell + y$。但 $y - x = w$，因此 $\mathbb{G}$ 中每个非零元素至少作为 $D$ 中元素的差出现 $\lambda$ 次。$D$ 中不同元素的差共有 $k(k - 1)$ 个。但是，根据定理 8.1.3，

$$b = v = \lambda \frac{v(v-1)}{k(k-1)},$$

因此 $k(k - 1) = \lambda(v - 1)$，故每个差恰好出现 $\lambda$ 次，从而证明 (ii)。

该定理表明，$\mathbb{G}$ 中的差集与具有块 $\mathbb{G}$ 且拥有同构于 $\mathbb{G}$ 且在点和块上自然作用的自同构群的对称设计之间存在一一对应关系。由差集 $D$ 如定理 8.7.5 所述得到的设计 $\mathcal{D}$ 称为 $D$ 的展开。

我们可以使用二次剩余来构造差集。

## **定理 8.7.6** ([204]) 设 $q = 4m - 1 = p^r$，其中 $p$ 为素数。集合 $D = \{x^2 \mid x \in \mathbb{F}_q, x \neq 0\}$ 是 $\mathbb{F}_q$ 加法群中的一个 $(4m-1, 2m-1, m-1)$ 差集。

**证明：** 由于 $q = 4m - 1 = p^r$，有 $p \equiv -1 \pmod 4$ 且 $r$ 为奇数。根据引理 6.2.4，$-1$ 不是 $\mathbb{F}_q$ 中的平方。因此 $-1$ 是 $\mathbb{F}_q$ 中 $x^2 + 1$ 的一个根，但不是 $\mathbb{F}_p$ 中的根。由于 $\mathbb{F}_p \not\subseteq \mathbb{F}_q$，$-1$ 不是 $\mathbb{F}_q$ 中的平方。由于 $\mathbb{F}_q$ 的非零元素构成一个以 $\alpha$ 为生成元的循环群 $\mathbb{F}_q^*$，$D$ 由 $2m-1$ 个元素 $\{\alpha^{2i} \mid 1 \le i \le 2m-1\}$ 组成，而 $(-1)D$ 构成 $\mathbb{F}_q$ 的其余非零元素（非平方）。设 $M$ 为多重集 $\{x-y \mid x \in D, y \in D, x \ne y\}$。如果 $x-y$ 是 $M$ 中一个固定的差，那么对于 $1 \le i \le 2m-1$，$\alpha^i(x-y) = (\alpha^i y)^{-1}x - (\alpha^i y)x$ 和 $-\alpha^{2i}(x-y) = (\alpha^i y)^{-1}y - (\alpha^i y)x$ 各自都在 $M$ 中，并构成 $\mathbb{F}_q$ 的全部 $4m-2$ 个非零元素。因此，$\mathbb{F}_q$ 中每个非零元素恰好出现 $\lambda$ 次（对某个 $\lambda$），从而构成 $\mathbb{F}_q$ 加法群中的一个 $(4m-1, 2m-1, \lambda)$ 差集。根据 (8.12)，$\lambda = m-1$。

将定理 8.7.6 应用于 $q = p = 4m-1$ 且 $p$ 为素数的情况，我们在 $\mathbb{Z}_p$ 中得到一个循环差集。

## **练习 466** 使用定理 8.7.6 在 $\mathbb{Z}_7, \mathbb{Z}_{11}, \mathbb{Z}_{19}, \mathbb{Z}_{23}$ 和 $\mathbb{Z}_{31}$ 中得到 $(v, k, \lambda)$ 循环差集。它们的参数 $v, k$ 和 $\lambda$ 是多少？

当 $\lambda = 1$ 且 $\mathbb{G} = \mathbb{Z}_v$ 时，对称设计是循环射影平面。由于证明不符合 Bruck-Ryser-Chowla 定理所涵盖参数的射影平面不存在非常困难，因此考虑具有额外条件的平面是合理的。一种自然的可能性是考察循环射影平面不存在的准则。我们接下来的两个定理表明，如果一个循环射影平面的阶 $\mu$ 满足 $\mu \equiv 2 \pmod 4$ 或 $\mu \equiv \pm 3 \pmod 9$，则 $\mu = 2$ 或 $\mu = 3$。这些结果在 [353] 中以更一般的阶 $\mu^2+\mu+1$ 的阿贝尔群中的 $(\mu^2+\mu+1, \mu+1, 1)$ 差集的框架下被证明。使用双重码，我们可以相当容易地证明这两个定理。第一个定理的证明见 [267]。

## **定理 8.7.7** 设 $\mathcal{D}$ 为阶 $\mu \equiv 2 \pmod 4$ 的循环射影平面。则 $\mu = 2$。

**证明：** 设 $A$ 为 $\mathcal{D}$ 的关联矩阵。根据定理 8.7.1(ii)，$\mathcal{D}_2(A)$ 是一个具有分割 $\mu_{-1}$ 的 $[v, (v-1)/2]$ 自正交偶型双重码。根据定理 8.5.3 和 6.4.2，$C_2(A)$ 是一个奇型双重码。根据定理 8.6.3，$C_2(A)$ 的最小权为 $\mu+1$，最小权码字是那些支持为直线的码字。根据定理 4.3.13，$\mu_2 \in \text{PAut}(C_2(A))$，因此 $\mu_2$ 置换最小权码字。故 $\mu_2 \in \text{Aut}(\mathcal{D})$。由于 $\mu_2$ 固定坐标 $0$，根据定理 8.7.2，$\mu_2$ 固定一条直线 $\ell$，因此 $\mu_2$ 固定 $C_2(A)$ 的一个最小权码字 $\mathbf{c}$。但是，任何被 $\mu_2$ 固定的非零二进制码字必须是幂等元。根据定理 8.7.5，$\mathcal{D}$ 的直线可以通过 $\ell$ 的循环移位得到；由于 $C_2(A)$ 中支持为直线的码字，$\mathbf{c}$ 必须是生成幂等元。但是，根据方程 (6.1) 和 (6.3)，长度为 $v$ 的二进制双重码的生成幂等元的权为 $(v-1)/2$ 或 $(v+1)/2$。因此 $\mu+1 = (v \pm 1)/2 = (\mu^2+\mu+1 \pm 1)/2$，这意味着 $\mu = 2$。

涉及三元双重码的类似论证得出以下结果。

## **定理 8.7.8** 设 $\mathcal{D}$ 为阶 $\mu$ 的循环射影平面，其中 $3 \mid \mu$ 但 $9 \nmid \mu$。则 $\mu = 3$。

**证明：** 设 $A$ 为阶 $\mu = k-1$ 的 $2\text{-}(v, k, 1)$ 设计 $\mathcal{D}$ 的关联矩阵。根据定理 8.5.3，由于 $3 \mid (\mu+1)$，$\mathcal{D}_3(A)$ 的维为 $(v-1)/2$，且 $\mathcal{D}_3(A) = C_3(A)^\perp \subset C_3(A) = C_3(A)^\perp$。因此，根据定理 6.4.1，$\mathcal{D}_3(A)$ 是一个由 $\mu_{-1}$ 给出分割的偶型双重码。根据定理 6.4.2，$C_3(A)$ 是一个奇型双重码。根据定理 4.3.13,

