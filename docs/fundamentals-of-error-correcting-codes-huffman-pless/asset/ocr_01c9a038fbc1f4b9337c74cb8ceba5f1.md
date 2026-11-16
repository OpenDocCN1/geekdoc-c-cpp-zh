As in (ii), (iii) is completed if we show that $C^T$ has dimension $k-1$. If $S \subset T$ with $S$ of size $d-1$, $C^S$ has dimension $k$ by part (ii). Clearly $C^S$ has minimum distance 1 and $C^T$ is obtained by puncturing $C^S$ on the nonzero coordinate of a weight 1 codeword in $C^S$. By Theorem 1.5 (ii) $C^T$ has dimension $k-1$.

**Exercise 28** Let $\mathcal{C}$ be the binary repetition code of length $n$ as described in Example 1.2.2. Describe $(\mathcal{C}^\perp)_T$ and $(\mathcal{C}_T)^\perp$ for any $T$.

**Exercise 29** Let $\mathcal{C}$ be the code of length 6 in Example 1.4.4. Give generator matrices for $(\mathcal{C}^\perp)_T$ and $(\mathcal{C}_T)^\perp$ when $T = \{1, 2\}$ and $T = \{1, 3\}$. 

# ## 1.5.4 Direct sums

For $i \in \{1, 2\}$ let $\mathcal{C}_i$ be an $[n_i, k_i, d_i]$ code, both over the same finite field $\mathbb{F}_q$. Then their *direct sum* is the $[n_1 + n_2, k_1 + k_2, \min\{d_1, d_2\}]$ code

$\mathcal{C}_1 \oplus \mathcal{C}_2 = \{(\mathbf{c}_1, \mathbf{c}_2) | \mathbf{c}_1 \in C_1, \mathbf{c}_2 \in C_2\}$.

If $\mathcal{C}_i$ is generator matrix $G_i$ and parity check matrix $H_i$, then

$G_1 \oplus G_2 = \begin{bmatrix} G_1 & O \ O & G_2 \end{bmatrix} \text{ and } H_1 \oplus H_2 = \begin{bmatrix} H_1 & O \ O & H_2 \end{bmatrix} \quad (1.4)$

are a generator matrix and parity check matrix for $\mathcal{C}_1 \oplus \mathcal{C}_2$.

**Exercise 30** Let $\mathcal{C}_i$ have generator matrix $G_i$ and parity check matrix $H_i$ for $i \in \{1, 2\}$. Prove that the generator and parity check matrices for $\mathcal{C}_1 \oplus \mathcal{C}_2$ are as given in (1.4).

**Exercise 31** Let $\mathcal{C}$ be the binary code with generator matrix

| 1 | 1 | 0 | 0 | 1 | 1 | 0 |
|---|---|---|---|---|---|---|
| 1 | 0 | 0 | 1 | 0 | 1 | 1 |
| 1 | 0 | 0 | 1 | 1 | 1 | 0 |
| 1 | 0 | 1 | 0 | 1 | 1 | 0 |
| 1 | 0 | 0 | 1 | 0 | 1 | 1 |

Give another generator matrix for $\mathcal{C}$ that shows that $\mathcal{C}$ is a direct sum of two binary codes.

**Example 1.5.8** The [6, 3, 2] binary code $\mathcal{C}$ of Example 1.4.4 is the direct sum $\mathcal{D} \oplus \mathcal{D} \oplus \mathcal{D}$ of the [2, 1, 2] code $\mathcal{D} = (00, 11)$.

Since the minimum distance of the direct sum of two codes does not exceed the minimum distance of either of the codes, the direct sum of two codes is generally of little use in applications and is primarily of theoretical interest.

# ## 1.5.5 The [u | u + v] construction

Two codes of the same length can be combined to form a third code of twice the length in a way similar to the direct sum construction. Let $\mathcal{C}_i$ be an $[n, k_i, d_i]$ code for $i \in \{1, 2\}$,