

| n | d_var | d_sdII | d_known | n | d_var | d_sdII | d_known |
|---|---|---|---|---|---|---|---|
| 8 | 3 | 4 | 4^E | 56 | 9 | 8 | 12^E |
| 16 | 4 | 4 | 4^E | 64 | 9 | 8 | 12^E |
| 24 | 5 | 4 | 8^E | 72 | 10 | 12 | 12 |
| 32 | 6 | 4 | 8^E | 80 | 11 | 12 | 16^E |
| 40 | 7 | 8 | 8^E | 88 | 12 | 12 | 16^E |
| 48 | 8 | 8 | 12^E | 96 | 13 | 12 | 16 |

表示为 "d_sdII"。长度为 n 的已知存在的 Type II 码的最大最小权重表示为 "d_known"；该条目上的 "E" 表示该码是极码。后者码的构造（含参考文献），适用于 $8 \le n \le 88$，在 [291] 中有描述；[96, 48, 16] Type II 码最初由 Feit [80] 构造。Varshamov 界指出满足该界的码是存在的；在哪里搜索它们并不明显。从表中可以看出，要寻找维度为长度一半的好码，当长度是 8 的倍数时可以查看表 9.6 中的码，并获得接近满足 Varshamov 界的码。将表 9.6（其中我们考察的码的最小权重与下界进行比较）与表 9.1（其中我们处理的码的最小权重与上界进行比较）进行对比是很有启发性的。

### Exercise 529
验证表 9.6 中 d_var 和 d_sdII 列的条目。

There is a result analogous to that of Theorem 9.5.12 for self-dual codes over F_q found in [278]. Example 9.5.13 illustrates this for q = 2.

在 [278] 中，对于 F_q 上的自双码，存在与定理 9.5.12 类似的结果。例 9.5.13 在 q = 2 时对此进行了说明。

### Example 9.5.13
Let n be even. Let r be the largest integer such that

\[
\binom{n}{2} + \binom{n}{4} + \binom{n}{6} + \cdots + \binom{n}{2(r-1)} < 2^{r-1} + 1. \tag{9.8}
\]

### 例 9.5.13
设 n 为偶数。设 r 为满足下式的最大整数：

\[
\binom{n}{2} + \binom{n}{4} + \binom{n}{6} + \cdots + \binom{n}{2(r-1)} < 2^{r-1} + 1. \tag{9.8}
\]

In Exercise 530, you are asked to prove that there exists a self-dual binary code of length n and minimum weight at least 2r. Table 9.7 is analogous to Table 9.6 for self-dual binary codes of even length n with $4 \le n \le 50$ using the bound (9.8). The column "d_var" has the same meaning as it does with Table 9.6. The largest d from bound (9.8) is denoted "d_sd". The largest minimum weight for a self-dual binary code (Type I or Type II) of length n known to exist is denoted "d_known". In all cases, it has been proved by various means that there is no self-dual binary code of length $n \le 50$ and minimum weight higher than that given in the table under "d_known". For length $n \le 32$ there are no codes with higher minimum weight by the classifications discussed in Section 9.7. For $34 < n < 50$, there is no self-dual code with higher minimum weight by Theorem 9.3.5. There are no [34, 17, 8] or [50, 25, 12] self-dual codes by [58]; if either code exists, its shadow code would have a weight enumerator with noninteger coefficients. Furthermore, if $n \equiv 0 \pmod{8}$, the codes of highest minimum weight are all attained by Type II codes (and possibly Type I codes as well). Again it is worth comparing this table to Table 9.1.

在练习 530 中，要求证明存在长度为 n 且最小权重至少为 2r 的自双二进制码。表 9.7 类似于表 9.6，适用于使用界 (9.8) 的长度为偶数 n（$4 \le n \le 50$）的自双二进制码。列 "d_var" 与表 9.6 中的含义相同。界 (9.8) 中的最大 d 表示为 "d_sd"。长度为 n 的已知存在的自双二进制码（Type I 或 Type II）的最大最小权重表示为 "d_known"。在所有情况下，已通过各种方法证明，不存在长度 $n \le 50$ 且最小权重高于表中 "d_known" 所给数值的自双二进制码。对于长度 $n \le 32$，根据第 9.7 节讨论的分类，不存在具有更高最小权重的码。对于 $34 < n < 50$，根据定理 9.3.5，不存在具有更高最小权重的自双码。根据 [58]，不存在 [34, 17, 8] 或 [50, 25, 12] 自双码；如果其中任何一个码存在，其影子码的权重枚举子将具有非整数系数。此外，如果 $n \equiv 0 \pmod{8}$，则最高最小权重的码均由 Type II 码（可能也包括 Type I 码）实现。再次将此表与表 9.1 进行比较是有价值的。

| n | d_var | d_sd | d_known | n | d_var | d_sd | d_known |
|---|---|---|---|---|---|---|---|
| 4 | 2 | 2 | 2 | 28 | 5 | 4 | 6 |
| 6 | 3 | 2 | 2 | 30 | 6 | 4 | 6 |
| 8 | 3 | 2 | 4 | 32 | 6 | 4 | 8 |
| 10 | 3 | 2 | 2 | 34 | 6 | 6 | 6 |
| 12 | 3 | 2 | 4 | 36 | 6 | 6 | 8 |
| 14 | 4 | 2 | 4 | 38 | 7 | 6 | 8 |
| 16 | 4 | 4 | 4 | 40 | 7 | 6 | 8 |
| 18 | 4 | 4 | 4 | 42 | 7 | 6 | 8 |
| 20 | 4 | 4 | 4 | 44 | 7 | 6 | 8 |
| 22 | 5 | 4 | 6 | 46 | 7 | 6 | 10 |
| 24 | 5 | 4 | 8 | 48 | 8 | 6 | 12 |
| 26 | 5 | 4 | 6 | 50 | 8 | 8 | 10 |

### Exercise 530
Prove that there exists a self-dual binary code of length $n$ and minimum weight at least $2r$ provided $r$ is the largest integer satisfying (9.8).

### 练习 530
证明存在长度为 $n$ 且最小权重至少为 $2r$ 的自双二进制码，前提是 $r$ 是满足 (9.8) 的最大整数。

### Exercise 531
Verify the entries in the columns $d_{\text{var}}$ and $d_{\text{sd}}$ of Table 9.7.

### 练习 531
验证表 9.7 中 $d_{\text{var}}$ 和 $d_{\text{sd}}$ 列的条目。

## 9.6 Mass formulas

We now know, from Theorem 9.5.1, that the total number of self-dual binary codes of length $n$ is $\prod_{i=1}^{(n-1)/2} (2^i + 1)$. Ultimately we would like to find a representative from each equivalence class of these codes; this is called a *classification problem*. It would be of great help to know the number of inequivalent codes. At this point there does not seem to be a direct formula for this. However, we can create a formula that can be used to tell us when we have a representative from every class of inequivalent self-dual codes. This formula is called a *mass formula*.

## 9.6 质量公式

我们现在知道，根据定理 9.5.1，长度为 $n$ 的自双二进制码的总数为 $\prod_{i=1}^{(n-1)/2} (2^i + 1)。最终，我们希望从这些码的每个等价类中找到一个代表；这被称为*分类问题*。知道不等价码的数量将非常有帮助。目前似乎没有直接的公式来实现这一点。然而，我们可以创建一个公式，用于判断我们是否拥有每个不等价自双码类的代表。这个公式称为*质量公式*。

Let $C_1, \dots, C_k$ be representatives from every equivalence class of self-dual binary codes of length $n$. The number of codes equivalent to $C_j$ is

\[
\frac{|\text{Sym}_n|}{|\text{PAut}(C_j)|} = \frac{n!}{|\text{PAut}(C_j)|}.
\]

Therefore, summing over $j$, we must obtain the total number of self-dual codes, which yields the following mass formula for self-dual binary codes:

\[
\sum_{j=1}^k \frac{n!}{|\text{PAut}(C_j)|} = \prod_{i=1}^{\frac{n-1}{2}} (2^i + 1). \tag{9.9}
\]

设 $C_1, \dots, C_k$ 为长度为 $n$ 的自双二进制码每个等价类的代表。与 $C_j$ 等价的码的数量为

\[
\frac{|\text{Sym}_n|}{|\text{PAut}(C_j)|} = \frac{n!}{|\text{PAut}(C_j)|}.
\]

因此，对 $j$ 求和，我们必须得到自双码的总数，从而得到自双二进制码的以下质量公式：

\[
\sum_{j=1}^k \frac{n!}{|\text{PAut}(C_j)|} = \prod_{i=1}^{\frac{n-1}{2}} (2^i + 1). \tag{9.9}
\]

We can find mass formulas for Type II, III, and IV codes also, in the same fashion, using the results of Theorems 9.5.5(i) and 9.5.10. For Type III, we use the group of all monomial transformations, which has size $2^n n!$, in place of $\text{Sym}_n$. For Type IV, we use the group of all monomial transformations followed possibly by the Frobenius map, which has size \( 2 \cdot 3^n n! \), in place of \(\text{Sym}_n\). This gives the following theorem.

同样地，我们也可以使用定理 9.5.5(i) 和 9.5.10 的结果，以同样的方式找到 Type II、III 和 IV 码的质量公式。对于 Type III，我们使用所有单项变换组（大小为 $2^n n!$）来代替 $\text{Sym}_n$。对于 Type IV，我们使用所有单项变换后可能接着 Frobenius 映射的组（大小为 \( 2 \cdot 3^n n! \)）来代替 \(\text{Sym}_n\)。这给出了以下定理。

### Theorem 9.6.1
We have the following mass formulas:

- (i) For self-dual binary codes of length \( n \),
  \[
  \sum_j \frac{n!}{|\text{PAut}(C_j)|} = \prod_{i=0}^{\frac{n}{2}-1} (2^i + 1).
  \]

- (ii) For Type II codes of length \( n \),
  \[
  \sum_j \frac{n!}{|\text{PAut}(C_j)|} = \prod_{i=0}^{\frac{n}{2}-2} (2^i + 1).
  \]

- (iii) For Type III codes of length \( n \),
  \[
  \sum_j \frac{2^n n!}{|\text{MAut}(C_j)|} = 2 \prod_{i=1}^{\frac{n}{4}-1} (3^i + 1).
  \]

- (iv) For Type IV codes of length \( n \),
  \[
  \sum_j \frac{2 \cdot 3^n n!}{|\Gamma\text{Aut}(C_j)|} = \prod_{i=0}^{\frac{n}{4}-1} (2^{2i+1} + 1).
  \]

In each case, the summation is over all \( j \), where \(\{C_j\}\) is a complete set of representatives of inequivalent codes of the given type.

### 定理 9.6.1
我们有以下质量公式：

- (i) 对于长度为 \( n \) 的自双二进制码，
  \[
  \sum_j \frac{n!}{|\text{PAut}(C_j)|} = \prod_{i=0}^{\frac{n}{2}-1} (2^i + 1).
  \]

- (ii) 对于长度为 \( n \) 的 Type II 码，
  \[
  \sum_j \frac{n!}{|\text{PAut}(C_j)|} = \prod_{i=0}^{\frac{n}{2}-2} (2^i + 1).
  \]

- (iii) 对于长度为 \( n \) 的 Type III 码，
  \[
  \sum_j \frac{2^n n!}{|\text{MAut}(C_j)|} = 2 \prod_{i=1}^{\frac{n}{4}-1} (3^i + 1).
  \]

- (iv) 对于长度为 \( n \) 的 Type IV 码，
  \[
  \sum_j \frac{2 \cdot 3^n n!}{|\Gamma\text{Aut}(C_j)|} = \prod_{i=0}^{\frac{n}{4}-1} (2^{2i+1} + 1).
  \]

在每种情况下，求和是对所有 \( j\) 进行，其中 \(\{C_j\}\) 是给定类型不等价码的完整代表集。

### Example 9.6.2
We continue with Example 9.5.6 and illustrate the mass formula for Type II codes in Theorem 9.6.1(ii) for \( n=8 \). Any Type II code of length 8 must be an \([8, 4, 4]\) code. Such a code \( C \) is unique and the left-hand side of the mass formula is \( 8!/|\text{PAut}(C)|\); the right-hand side is 30. Therefore, \(|\text{PAut}(C)| = 1344\); it is known that \(\text{PAut}(C)\) is isomorphic to the 3-dimensional general affine group over \(\mathbb{F}_2\), which indeed has order 1344.

### 例 9.6.2
我们继续沿用例 9.5.6，并说明定理 9.6.1(ii) 中针对 \( n=8 \) 的 Type II 码的质量公式。任何长度为 8 的 Type II 码必须是一个 \([8, 4, 4]\) 码。这样的码 \( C \) 是唯一的，质量公式的左边为 \( 8!/|\text{PAut}(C)|\)；右边为 30。因此，\(|\text{PAut}(C)| = 1344\)；已知 \(\text{PAut}(C)\) 与 \(\mathbb{F}_2\) 上的 3 维一般仿射群同构，该群的阶确实为 1344。

## 9.7 Classification

Once we have the mass formula for a class of codes, we can attempt to classify them. Suppose we want to classify the self-dual codes of length \( n \). The strategy is to classify these codes for the smallest lengths first. Once that is accomplished, we proceed to larger lengths using the results obtained for smaller lengths. We discuss the overall strategy for classification focusing primarily on self-dual binary codes.

## 9.7 分类

一旦我们有了某类码的质量公式，就可以尝试对它们进行分类。假设我们想要对长度为 \( n \) 的自双码进行分类。策略是先对最小长度的码进行分类。一旦完成，我们就使用较小长度获得的结果来处理更大的长度。我们主要讨论自双二进制码的分类总体策略。

### 9.7.1 The Classification Algorithm

There is a general procedure that has been used in most of the classifications attempted. The Classification Algorithm, which we state for self-dual binary codes, is as follows:

- I. Find a self-dual binary code $\mathcal{C}_1$ of length $n$.
- II. Compute the size of the automorphism group $\text{PAut}(\mathcal{C}_1)$ of the code found in Step I and calculate the contribution of $n/|\text{PAut}(\mathcal{C}_1)|$ to the left-hand side of (9.9).
- III. Find a self-dual binary code $\mathcal{C}_j$ not equivalent to any previously found. Compute the size of the automorphism group $\text{PAut}(\mathcal{C}_j)$ and calculate $n/|\text{PAut}(\mathcal{C}_j)|$; add this to the contributions to the left-hand side of (9.9) from the inequivalent codes previously found.
- IV. Repeat Step III until the total computed on the left-hand side of (9.9) gives the amount on the right-hand side.

The classification for Type II, III, and IV codes is analogous where we use the appropriate mass formula from Theorem 9.6.1.

### 9.7.1 分类算法

在大多数尝试的分类中都使用了一种通用程序。针对自双二进制码，我们给出的分类算法如下：

- I. 找到一个长度为 $n$ 的自双二进制码 $\mathcal{C}_1$。
- II. 计算步骤 I 中找到的码的自同构群 $\text{PAut}(\mathcal{C}_1)$ 的大小，并计算 $n/|\text{PAut}(\mathcal{C}_1)|$ 对 (9.9) 左边的贡献。
- III. 找到一个与之前找到的任何码都不等价的自双二进制码 $\mathcal{C}_j$。计算自同构群 $\text{PAut}(\mathcal{C}_j)$ 的大小并计算 $n/|\text{PAut}(\mathcal{C}_j)|$；将其加到之前找到的不等价码对 (9.9) 左边的贡献中。
- IV. 重复步骤 III，直到 (9.9) 左边计算出的总和等于右边的数值。

Type II、III 和 IV 码的分类是类似的，使用定理 9.6.1 中相应的质量公式。

### Example 9.7.1

We classify all the self-dual binary codes of length $n=8$. The right-hand side of the mass formula is $(2+1)(2^2+1)(2^3+1) = 135$. From Example 9.6.2, the unique $[8, 4, 4]$ code $\mathcal{C}_1$ has automorphism group of size 1344. It contributes 30 to the left-hand side of the mass formula. There is also the self-dual code $\mathcal{C}_2 = \mathcal{C} \oplus \mathcal{C} \oplus \mathcal{C} \oplus \mathcal{C}$, where $\mathcal{C}$ is the $[2, 1, 2]$ binary repetition code. Any of the two permutations on the two coordinates of any direct summand is an automorphism; this gives a subgroup of $\text{PAut}(\mathcal{C}_2)$ of order $2^4$. Furthermore, any of the four summands can be permuted in $4!$ ways. All the automorphisms can be generated from these; the group has order $2^4 4!$ and $\mathcal{C}_2$ contributes 105 to the left-hand side of the mass formula. The total contribution is 135, which equals the right-hand side. Hence there are only two inequivalent self-dual binary codes of length 8.

### 例 9.7.1

我们对长度为 $n=8$ 的所有自双二进制码进行分类。质量公式的右边为 $(2+1)(2^2+1)(2^3+1) = 135$。根据例 9.6.2，唯一的 $[8, 4, 4]$ 码 $\mathcal{C}_1$ 的自同构群大小为 1344。它对质量公式左边贡献 30。还存在自双码 $\mathcal{C}_2 = \mathcal{C} \oplus \mathcal{C} \oplus \mathcal{C} \oplus \mathcal{C}$，其中 $\mathcal{C}$ 是 $[2, 1, 2]$ 二进制重复码。对任何直和分量的两个坐标进行的任何两个排列都是自同构；这给出了 $\text{PAut}(\mathcal{C}_2)$ 的一个阶为 $2^4$ 的子群。此外，四个分量中的任何一个都可以以 $4!$ 种方式进行排列。所有自同构都可以由此生成；该群的阶为 $2^4 4!$，$\mathcal{C}_2$ 对质量公式左边贡献 105。总贡献为 135，等于右边。因此，长度为 8 的不等价自双二进制码只有两个。

### Exercise 532

Find a complete list of all inequivalent self-dual binary codes of lengths:

- (a) $n=2$,
- (b) $n=4$,
- (c) $n=6$, and
- (d) $n=10$.

As the lengths grow, the classification becomes more difficult. There are methods to simplify this search. When many of the original classifications were done, computing the automorphism groups was also problematic; now, with computer programs that include packages for codes, finding the automorphism groups is simplified.

### 练习 532

找出以下长度的所有不等价自双二进制码的完整列表：

- (a) $n=2$，
- (b) $n=4$，
- (c) $n=6$，以及
- (d) $n=10$。

随着长度的增加，分类变得更加困难。有方法可以简化这种搜索。在最初的许多分类完成时，计算自同构群也是一个问题；现在，带有码包的计算机程序使得查找自同构群变得简单。

We now go into more detail regarding classification of binary codes and the specifics of carrying out the Classification Algorithm. There are several self-orthogonal codes that will arise frequently. They are denoted $i_2, e_7, e_8, \text{and } d_{2m}$, with $m \ge 2$. The subscript on these codes indicates their length. The codes $i_2, e_7, \text{and } e_8$ have generator matrices

\[
i_2: [1\ 1], \quad
e_7: \begin{bmatrix}
1 & 1 & 1 & 1 & 0 & 0 & 0 \\
0 & 0 & 1 & 1 & 1 & 0 & 0 \\
1 & 0 & 1 & 0 & 1 & 0 & 1 \\
1 & 0 & 1 & 0 & 0 & 1 & 1
\end{bmatrix}, \quad
e_8: \begin{bmatrix}
1 & 1 & 1 & 1 & 0 & 0 & 0 & 0 \\
0 & 0 & 1 & 1 & 1 & 0 & 0 & 0 \\
0 & 0 & 0 & 0 & 1 & 1 & 0 & 0 \\
1 & 0 & 1 & 0 & 1 & 0 & 1 & 0 \\
1 & 0 & 0 & 1 & 0 & 1 & 0 & 1 \\
1 & 0 & 1 & 0 & 0 & 1 & 0 & 1 \\
1 & 0 & 0 & 1 & 0 & 0 & 1 & 0
\end{bmatrix}.
\]

我们现在将详细介绍二进制码的分类以及执行分类算法的具体细节。有几个自正交码将频繁出现。它们表示为 $i_2, e_7, e_8, \text{和 } d_{2m}$，其中 $m \ge 2$。这些码的下标表示它们的长度。码 $i_2, e_7, \text{和 } e_8$ 的生成矩阵为

\[
i_2: [1\ 1], \quad
e_7: \begin{bmatrix}
1 & 1 & 1 & 1 & 0 & 0 & 0 \\
0 & 0 & 1 & 1 & 1 & 0 & 0 \\
1 & 0 & 1 & 0 & 1 & 0 & 1 \\
1 & 0 & 1 & 0 & 0 & 1 & 1
\end{bmatrix}, \quad
e_8: \begin{bmatrix}
1 & 1 & 1 & 1 & 0 & 0 & 0 & 0 \\
0 & 0 & 1 & 1 & 1 & 0 & 0 & 0 \\
0 & 0 & 0 & 0 & 1 & 1 & 0 & 0 \\
1 & 0 & 1 & 0 & 1 & 0 & 1 & 0 \\
1 & 0 & 0 & 1 & 0 & 1 & 0 & 1 \\
1 & 0 & 1 & 0 & 0 & 1 & 0 & 1 \\
1 & 0 & 0 & 1 & 0 & 0 & 1 & 0
\end{bmatrix}.

