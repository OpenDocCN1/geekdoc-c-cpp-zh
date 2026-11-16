

## 9.1 RADON-NIKODYM 导数的形式化

对于任意可测集 A，度量 v 相对于度量 u 的 Radon-Nikodym 导数定义为非负可测函数 f，满足以下公式。

\int_A f du = v(A) (9.1)

Radon-Nikodym 导数在 HOL4 中形式化如下（Mhamdi, 2013）：

```
Definition 9.1
|- RN_deriv m v =
   @f. f IN measurable (X,S) Borel /\ 
   (forall x \in X, 0 <= f x /\ 
   forall a \in S, integral m (\x. f x * Ia x) = v a
```

其中 @ 表示 Hilbert-choice 算子。根据 Radon-Nikodym 定理，对于绝对连续度量，Radon-Nikodym 导数的存在性得到保证，该定理指出：如果 v 相对于 u 绝对连续，则存在非负可测函数 f，使得对于任意可测集 A，

\int_A f du = v(A) (9.2)

Radon-Nikodym 定理可在 HOL4 中对有限度量进行验证，并可轻易推广到 σ-有限度量。

```
Theorem 9.1
|- forall m v s st.
   measure_space (s, st, m) /\ 
   measure_space (s, st, v) /\ 
   abs_cont (s, st, m) (s, st, v) ==> 
   exists f measurable (s, st) Borel /\ 
   (forall x \in s, 0 <= f x /\ 
   forall a \in st, integral m (\x. f x * Ia x) = v a
```

对上述定理的形式化推理主要基于 Lebesgue 单调收敛定理和以下引理（Lemma 9.1），据我们所知，该引理此前未在数学文献中被引用：

如果 P 是一组在 max 算子下封闭的非空扩展实值函数集合，g 在 P 上单调且 g(P) 有上界，则存在 P 中元素的单调递增函数序列 f(n)，使得：

\(sup_x g(f(n)) = sup_x g(f)\) (9.3)

证明 Radon-Nikodym 定理包括定义非负可测函数集合 F，使得对于任意可测集 A，\(\int_A f d\mu = \nu(A)\)。该集合可被验证为非空、由空间的有限度量上界且在 max 算子下封闭。接下来，利用积分的单调性和上述引理，可验证存在 F 中函数的单调递增序列 f(n)，使得：

\(sup_x \int_X f_n d\mu = sup_x \int_X f d\mu\) (9.4)

最后，可验证如下定义的函数 g 满足定理的条件。

\(\forall x . g(x) = sup_n f_n(x)\) (9.5)

在概率理论形式化中使用扩展实数的主要原因之一是，若不考虑无穷值，则无法验证 Radon-Nikodym 定理。事实上，Lebesgue 单调收敛定理被用于证明：

\(\int_X g d\mu = sup_n \int_X f_n d\mu\) (9.6)

另一方面，如果不使用扩展实数，则 Lebesgue 单调收敛定理的证明要求序列 f(n) 收敛，而此处不一定如此，且不能将其作为假设添加，因为序列 f(n) 是在证明中生成的。带有扩展实数的 Lebesgue 单调收敛定理即使对于不收敛的序列也成立，因为它使用 sup 算子而非极限 lim。

现在，Radon-Nikodym 导数的性质可以以直接的方式进行形式化验证。例如，对于定义在有限空间上的绝对连续度量，该导数可被验证为简化为：

### Theorem 9.2

```
|- ∀ b u v x. x ∈ s ∧ u { x } ≠ 0 ⇒ RN_deriv u v x = v { x } / u { x }
```

以下性质在形式化推理 Radon-Nikodym 导数中起着至关重要的作用，并且也已在 HOL 中进行了形式化验证。

```
|- ∀x ∈ s ∧ 0 ≤ RN_deriv m v x < ∞
|- RN_deriv m v ∈ measurable (s,st) Borel
|- ∀a ∈ st, integral m (λx. RN_deriv m v x × Ia x) = v a
```

## 9.2 KULLBACK-LEIBLER 散度的形式化

Kullback-Leibler (KL) 散度 DKL (u ‖ v) 是两个分布 u 和 v 之间距离的度量。它可用于定义大多数信息论度量，如互信息和熵，因此可用于为形式化大多数信息泄漏度量提供统一框架。从数学上讲，KL 散度定义为：

```
DKL(μ ‖ ν) = - ∫x log(dν/dμ) dμ (9.7)
```

其中 dν/dμ 是 v 相对于 u 的 Radon-Nikodym 导数。KL 散度在 HOL4 中形式化如下：

### Definition 9.2

```
|- ∀ b m v. KL_divergence b m v =
-integral m (λx. logr b (RN_deriv m v x))
```

其中 b 是对数的底数。当 b = 2 时，DKL 以比特为单位计量。此定义现在可用于验证 DKL 的一些经典性质。例如，对于有限空间上的绝对连续度量，DKL 简化为：

```
D_{KL}(\mu || \nu) = \sum_{x \in s} \mu \{x\} \log \frac{\mu \{x\}}{\nu \{x\}} (9.8)
```

### Theorem 9.3

```
|- ∀ b u v. KL_divergence b u v =
SIGMA (λx. u { x } logr b (u { x } / v { x })) s
```

HOL4 中 DKL 的其他一些经过形式化验证的性质如下

```
|- ∀ b u. KL_divergence b u u = 0
```

```
|- ∀ b u v. 1 ≤ b ⇒ 0 ≤ KL_divergence b u v
```

对于有限空间上的绝对连续概率度量，KL 散度的非负性被广泛用于证明互信息和熵等信息论度量的性质。接下来，我们介绍使用 KL 散度来形式化互信息、Shannon 熵、条件熵和条件互信息，这些是最常用的信息度量之一。

## 9.3 互信息的形式化

两个随机变量的互信息 I (X; Y) 是两个随机变量之间相互依赖的度量，因为它衡量当另一个变量已知时，关于这些变量之一的不确定性降低了多少。互信息通常用作从程序的安全输入 X 到其公开输出 Y 的信息泄漏度量。它定义为联合分布与边缘分布乘积之间的 KL 散度。以下是 HOL 中互信息的形式化：

### Definition 9.3

```
|- ∀ X Y. I (X ; Y) = KL_divergence b (joint_distribution p X Y)
prod_measure (distribution p X) (distribution p Y)
```

互信息的各种性质已在 HOL 中得到验证，如非负性、对称性以及有限空间下的简化表达式，其依据是联合分布相对于边缘分布乘积绝对连续这一结果。

```
|- ∀ b X Y p s. I (X; Y) =
SIGMA (λ (x, y). p ( (x, y) ) logr b (p ( (x, y) ) / p ( x ) * p ( y ))) s
```

## 9.4 熵

Shannon 熵 H(X) 是与随机变量相关的不确定性的度量。此外，它也是当随机变量的值未知时平均缺失信息量的度量。Shannon 熵是最早被提出用于分析匿名协议和安全通信的度量之一（Diaz, Seys, Claessens, & Preneel, 2003）。它可以定义为 pX 的期望，或者简单地定义为 I (X; X)。

### Definition 9.4

```
|- ∀ X. H (X) = I (X; X)
```

它也可以用 p_X 与均匀分布 p'_X 之间的 KL 散度来表示，其中 N 是 X 的字母表大小。

### Definition 9.5

```
|- ∀ X N p. H (X) =
log (N) - KL_divergence b (distribution p X) (uniform_dist p X)
```

交叉熵 H(X; Y) 衡量两个随机变量联合系统中包含多少熵，它是随机变量 (X; Y) 的熵，因此无需单独形式化交叉熵。

条件熵 H (X | Y) 量化了在已知随机变量 Y 的值的情况下，关于随机变量 X 的剩余不确定性。它用 KL 散度定义如下：

### Definition 9.6

```
|- ∀ X Y N p. H (X | Y) =
log (N) - KL_divergence b (joint_distribution p X Y)
prod_measure (uniform_dist p X)
(distribution p Y)
```

