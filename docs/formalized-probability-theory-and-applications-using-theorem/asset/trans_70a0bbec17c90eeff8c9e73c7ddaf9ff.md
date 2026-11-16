

如果在DTMC中至少存在一个吸收态，并且从每个非吸收态都可以到达该吸收态，则这样的DTMC被称为吸收DTMC。

### 定义 7.8

```
⊢ ∀ X p s P₀ Pᵢⱼ·
Absorbing_mc X p s P₀ Pᵢⱼ =
th_dtmc X p s P₀ Pᵢⱼ
∃ i. i ∈ space s ∧ Absorbing_state X p s i ∧
(∀ j. j ∈ space s ⇒ Communicating_state X p s i j)
```

最后，如果存在某个n，使得DTMC中所有状态i和j的pij^(n) > 0，则该DTMC定义为正则DTMC。

### 定义 7.9

```
⊢ ∀ X p s P₀ Pᵢⱼ·
Regular_mc X p s P₀ Pᵢⱼ =
th_dtmc X p s P₀ Pᵢⱼ
∃ n. ∀ i j. i ∈ space s ∧ j ∈ space s ⇒ Trans X p s t n i j > 0
```

上述分类马尔可夫链的高阶逻辑形式化的主要效用是，在定理证明器的可靠环境中正式指定和分析马尔可夫系统的动态特性，这将在下一节中演示。

## 7.3 长期属性的形式验证

DTMC长期行为的分析取决于所考虑的状态类型。在前一节形式化的分类DTMC中，非周期和不可约DTMC被认为是在分析马尔可夫系统中最广泛使用的，因为它们具有吸引人的稳态特性，即其极限概率分布与初始分布无关。因此，我们现在专注于验证非周期和不可约DTMC的一些关键属性。

### 7.3.1 正转移概率

DTMC的形式化非周期性和不可约性特征可用于在HOL中验证其相应属性。

### 定理 7.1

- **属性：** 在DTMC中，状态$i$具有非零访问概率的时间集合在加法下是封闭的。

```
⊢ ∀ X p s P₀ Pᵢⱼ i.
Aperiodic_DTMC X p s P₀ Pᵢⱼ ∧ i ∈ space s ⇒
∀ a b. a ∈ Period_Set X p s i ∧ b ∈ Period_Set X p s i ⇒
(a + b) ∈ Period_Set X p s i
```

### 定理 7.2

- **属性：** 转移概率$p_{ij}^{(n)}$对于状态空间中所有状态$i$和$j$均大于零。对于非周期DTMC的有限状态空间$S$中的任何状态$i$，存在一个$N < \infty$，使得对于所有$n \ge N$和状态空间中的所有$i$，都有$0 < p_{i,j}^{(n)}$。

```
⊢ ∀ X p s P₀ Pᵢⱼ i t.
Aperiodic_DTMC X p s P₀ Pᵢⱼ ∧ i ∈ space s ⇒
∃ N. ∀ n. N ≤ n ⇒ 0 < Trans X p s t n i i
```

在此定理中，$N$是表示正整数的HOL4数据类型num。对上述定理正确性的形式推理涉及定理7.1、一些DTMC属性以及以下三个引理，以及一些算术推理和集合论推理。

### 引理 7.1

- **封闭集中的正元素：** 如果整数集合$S$包含至少一个非零元素且$S$在加法和减法下封闭，则$S = \{ kc; k \in Z \}$，其中$c$是$S$的最小正元素。

```
⊢ ∀ s:int → bool. s ≠ ∅ ∧
(∀ a b. a ∈ s ∧ b ∈ s ⇒ (a + b) ∈ s ∧ (a - b) ∈ s) ⇒
0 < MINSET { r | 0 < r ∧ r ∈ s } ∧
(s = { r | ∃k. r = k * MINSET { r | 0 < r ∧ r ∈ s } })
```

其中MINSET A指的是集合A中的最小元素。

### 引理 7.2

- **两个整数序列的线性性：** 对于正整数序列$a_r, a_2, ..., a_k$，存在整数序列$n_r, n_2, ..., n_k$，使得$d = \sum_{i=1}^k n_i a_i$，其中$d$是序列$a_r, a_2, ..., a_k$的最大公约数。

```
|- \forall a k. 0 < k \land (\forall i. i \le k \Rightarrow 0 < a i) \Rightarrow (\exists n. GCD\_SET { a i | i \in [0, k] } = \sum_{i=1}^k n i * a i)
```

### 引理 7.3

- **最小数：** 如果正整数集合$A$是非格的，即其最大公约数为1，且在加法下封闭，则存在一个整数$N < \infty$，使得对于所有$N \le n$都有$n \in A$。

```
|- \forall A: (int -> bool) a. (A = { a i | 0 < a i \land i \in UNIV :(num) }) \land (GCD\_SET A = 1) \land (\forall a b. a \in A \land b \in A \Rightarrow (a + b) \in A) \Rightarrow (\exists N. { n | N \le n } \subset A)
```

引理7.1、7.2和7.3的证明基于整数集合的各种求和性质以及集合的最大公约数性质。

- **属性：** 对于具有有限状态空间$S$的任何非周期和不可约DTMC，存在$N$，使得对于所有$n \ge N$，所有状态$i, j \in S$的$n$步转移概率$p_{ij}^{(n)}$均非零。

### 定理 7.3

```
|- \forall X p s P_0 Pij. \forall i j t. Aperiodic\_DTMC X p s P_0 Pij \land Irreducible\_DTMC X p s P_0 Pij \land i \in space s \land j \in space s \Rightarrow \exists N. \forall n. N \le n \Rightarrow 0 < Trans X p s t n i j
```

定理7.3的证明基于对$i$和$j$相等性的情况分析以及引理7.2和7.3。

- **属性：** 对于具有有限状态空间S和转移概率\( p_{ij} \)的任何非周期和不可约DTMC，对于所有状态\( i \)和\( j \in S \)，都存在\( \lim_{n \to \infty} p_{ij}^{(n)} \)。

### 定理 7.4

```
∀ X p s P₀ Pij i j t.
Aperiodic_DTMC X p s P₀ Pij ∧ Irreducible_DTMC X p s P₀ Pij ⇒
∃ u. lim (λ n. Trans X p s t n i j) = u
```

定理7.4的证明基于\( M_j^n \)和\( m_j^n \)的单调性性质，它们分别是集合\( \{n \ge 1: p_{jj}^{(n)} > 0\} \)的最大值和最小值。然后，通过验证对于所有满足\( N \le n \)的\( n \)的序列\( (M_j^n, m_j^n) \)的收敛性以及一些实数序列的性质来完成证明。需要注意的是，与所有其他定理一样，我们在这里不需要使用假设\( j \in space \)，因为\( \forall n j j \notin space \Rightarrow p_{jj}^{(n)} = 0 \)，这反过来意味着利用条件概率性质可得\( \lim_{n \to \infty} p_{jj}^{(n)} = 0 \)和\( \lim_{n \to \infty} p_{ij}^{(n)} = 0 \)。

### 7.3.2 收敛性分析

在随机系统中随机变量的收敛性分析中，通常会考虑长期概率分布。在一般非平凡DTMC中，验证某个状态的极限概率分布是否存在并不容易，因为此类分析所需的计算通常非常庞大。然而，在非周期和不可约DTMC中，我们可以通过以下两个属性证明所有状态都具有极限概率分布。

- **属性：** 对于具有有限状态空间S的任何非周期和不可约DTMC，对于任何状态\( i \in S \)，都存在\( \lim_{n \to \infty} p_{ij}^{(n)} \)。

### 定理 7.5

```
∀ X p s P₀ pij i.
Aperiodic_DTMC X p s P₀ pij ∧ Irreducible_DTMC X p s P₀ pij ⇒
∃ u. lim (λ n. P (x | X n x = i)) = u
```

该证明基于定理7.4以及序列极限的一些性质。

- **属性：** 对于非周期和不可约DTMC中的每个状态\( i \)，\( \lim_{n \to \infty} p_{i}^{(n)} \)是一个稳态分布。

### 定理 7.6

```
|- \forall X p s P₀ P_{i,j}.
Aperiodic_DTMC X p s P₀ P_{i,j} \land Irreducible_DTMC X p s P₀ P_{i,j} =>
(stationary_dist p x (i, lim (\lambda n. P (x | X n x = i))) s)
```

定理7.6的证明主要基于以下三个子目标：

- 0 \le lim_{n \to \infty} p_j^{(n)}
- \sum_{i \in S} lim_{n \to \infty} p_i^{(n)} = 1
- lim_{n \to \infty} p_j^{(n)} = \sum_{i \in S} p_i^{(n)} p_{ij}

第一个子目标可以使用概率界定理进行验证。第二个子目标的证明主要基于条件概率的可加性性质。而最后一个子目标可以使用序列极限和求和的线性性质进行验证。本节所呈现的所有形式化对应的脚本可在(Liu, 2013b)中找到。

## 7.4 应用

在上一节中，分类DTMC的一些常用属性已在HOL4中得到验证，以便于分析马尔可夫系统的长期行为。为了展示其有用性，本节首先在HOL中展示了一个LRU堆栈模型的形式验证。然后，利用非周期和不可约DTMC的形式化来正式定义一个离散时间生死过程，该过程可应用于正式分析软件数据结构的性能。

### 7.4.1 LRU堆栈模型

在最近最少使用（LRU）堆栈模型（Kwon & Agha, 2007）中，如图1所示，一系列堆栈s_1, s_2 ... s_n与引用字符串w = x_1, x_2 ...相关联。任何堆栈s_i都是一个n元组(j_1, j_2 ... j_j)，其中j_r指的是时间t时第r个最近被引用的页面。设D_j为堆栈s_{i-1}中页面x_i的位置。那么距离字符串是D_1, D_2 ... D_n ...，它与引用字符串相关联。这个距离字符串可以建模为一组独立同分布（IID）随机变量序列，这使得它们的概率质量

