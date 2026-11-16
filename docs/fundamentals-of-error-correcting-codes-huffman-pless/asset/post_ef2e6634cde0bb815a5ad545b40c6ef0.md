
matrices for \(\widehat{\mathcal{H}}_{3,2}\) are

\[
\widehat{G} = \left[ \begin{array}{ccccc} 1 & 0 & 1 & 1 & 0 \\ 0 & 1 & 1 & -1 & -1 \end{array} \right]
\]
and
\[
\widehat{H} = \left[ \begin{array}{ccccc} 1 & 1 & 1 & 1 & 1 \\ -1 & -1 & 1 & 0 & 0 \\ -1 & 1 & 0 & 1 & 0 \end{array} \right] .
\]

If we extend a code and then puncture the new coordinate, we obtain the original code. However, performing the operations in the other order will in general result in a different code.

### Example 1.5.5
If we puncture the binary code \(\mathcal{C}\) with generator matrix

\[
G = \left[ \begin{array}{ccccc} 1 & 1 & 0 & 0 & 1 \\ 0 & 0 & 1 & 1 & 0 \end{array} \right]
\]

on its last coordinate and then extend (on the right), the resulting code has generator matrix

\[
G = \left[ \begin{array}{ccccc} 1 & 1 & 0 & 0 & 0 \\ 0 & 0 & 1 & 1 & 0 \end{array} \right] .
\]

In this example, our last step was to extend a binary code with only even weight vectors. The extended coordinate was always 0. In general, that is precisely what happens when you extend a code that has only even-like codewords.

### Exercise 27
Do the following.

- (a) Let \(\mathcal{C} = \mathcal{H}_{3,2}\) be the \([4, 2, 3]\) tetracode over \(\mathbb{F}_3\) defined in Example 1.3.3 with generator matrix

\[
G = \left[ \begin{array}{cccc} 1 & 0 & 1 & 1 \\ 0 & 1 & 1 & -1 \end{array} \right] .
\]

Give the generator matrix of the code obtained from \(\mathcal{C}\) by puncturing on the right-most coordinate and then extending on the right. Also determine the minimum weight of the resulting code.

- (b) Let \(\mathcal{C}\) be a code over \(\mathbb{F}_q\). Let \(\mathcal{C}_r\) be the code obtained from \(\mathcal{C}\) by puncturing on the right-most coordinate and then extending this punctured code on the right. Prove that \(\mathcal{C} = \mathcal{C}_r\) if and only if \(\mathcal{C}\) is an even-like code.

- (c) With \(\mathcal{C}_1\) defined as in (b), prove that if \(\mathcal{C}\) is self-orthogonal and contains the all-one codeword \(\mathbf{1}\), then \(\mathcal{C} = \mathcal{C}_1\).

- (d) With \(\mathcal{C}_1\) defined as in (b), prove that \(\mathcal{C} = \mathcal{C}_1\) if and only if the all-one vector \(\mathbf{1}\) is in \(\mathcal{C}^{\perp}\).

## 1.5.3 Shortening codes

Let \(\mathcal{C}\) be an \([n, k, d]\) code over \(\mathbb{F}_q\) and let \(T\) be any set of \(t\) coordinates. Consider the set \(\mathcal{C}(T)\) of codewords which are \(\mathbf{0}\) on \(T\); this set is a subcode of \(\mathcal{C}\). Puncturing \(\mathcal{C}(T)\) on \(T\) gives a code over \(\mathbb{F}_q\) of length \(n - t\) called the code _shortened on \(T\)_ and denoted \(\mathcal{C}_T\).

### Example 1.5.6
Let $C$ be the $[6, 3, 2]$ binary code with generator matrix

\[
G = \begin{bmatrix} 1 & 0 & 0 & 1 & 1 & 1 \\ 0 & 1 & 0 & 1 & 1 & 1 \\ 0 & 0 & 1 & 1 & 1 & 1 \end{bmatrix}
\]

$C^\perp$ is also a $[6, 3, 2]$ code with generator matrix

\[
G^\perp = \begin{bmatrix} 1 & 1 & 1 & 1 & 0 & 0 \\ 1 & 1 & 1 & 0 & 1 & 0 \\ 1 & 1 & 0 & 0 & 0 & 1 \end{bmatrix}
\]

If the coordinates are labeled $1, 2, \dots, 6$, let $T = \{5, 6\}$. Generator matrices for the shortened code $C_T$ and punctured code $C^T$ are

\[
G_T = \begin{bmatrix} 1 & 0 & 1 & 0 \\ 0 & 1 & 1 & 0 \\ 0 & 1 & 1 & 0 \end{bmatrix} \text{ and } G^T = \begin{bmatrix} 1 & 0 & 0 & 1 \\ 0 & 1 & 0 & 1 \\ 0 & 0 & 1 & 1 \end{bmatrix}
\]

Shortening and puncturing the dual code gives the codes $(C^\perp)_T$ and $(C^\perp)^T$, which have generator matrices

\[
(G^\perp)_T = [1 \ 1 \ 1 \ 1] \text{ and } (G^\perp)^T = \begin{bmatrix} 1 & 1 & 1 & 1 \\ 1 & 1 & 1 & 0 \end{bmatrix}
\]

From the generator matrices $G_T$ and $G^T$, we find that the duals of $C_T$ and $C^T$ have generator matrices

\[
(G_T)^\perp = \begin{bmatrix} 1 & 1 & 1 & 0 \\ 0 & 0 & 0 & 1 \end{bmatrix} \text{ and } (G^T)^\perp = [1 \ 1 \ 1 \ 1]
\]

Notice that these matrices show that $(C^\perp)_T = (C^T)^\perp$ and $(C^\perp)^T = (C_T)^\perp$.

The conclusions observed in the previous example hold in general.

### Theorem 1.5.7
Let $C$ be an $[n, k, d]$ code over $\mathbb{F}_q$. Let $T$ be a set of $t$ coordinates. Then:
(i) $(C^\perp)_T = (C^T)^\perp$ and $(C^\perp)^T = (C_T)^\perp$,
(ii) if $t < d$, then $C_T$ and $(C^\perp)^T$ have dimensions $k$ and $n - t - k$, respectively;
(iii) if $t = d$ and $T$ is the set of coordinates where a minimum weight codeword is nonzero, then $C^T$ and $(C^\perp)_T$ have dimensions $k - 1$ and $n - d - k + 1$, respectively.

**Proof.** Let $c$ be a codeword of $C^\perp$ which is $\mathbf{0}$ on $T$ and $c^*$ the codeword with the coordinates in $T$ removed. So $c^* \in (C^\perp)_T$. If $\mathbf{x} \in C$, then $\mathbf{0} = \mathbf{x} \cdot \mathbf{c} = \mathbf{x}^* \cdot \mathbf{c}^*$, where $\mathbf{x}^*$ is the codeword $\mathbf{x}$ punctured on $T$. Thus $(C^\perp)_T \subseteq (C^T)^\perp$. Any vector $\mathbf{c} \in (C^T)^\perp$ can be extended to a vector $\tilde{\mathbf{c}}$ by inserting 0s in the positions of $T$. If $\mathbf{x} \in C$, puncture $\mathbf{x}$ on $T$ to obtain $\mathbf{x}^*$. As $\mathbf{0} = \mathbf{x}^* \cdot \mathbf{c} = \mathbf{x} \cdot \tilde{\mathbf{c}}$, $\tilde{\mathbf{c}} \in (C^\perp)_T$. Thus $(C^T)^\perp = (C^\perp)_T$. Replacing $C$ by $C^\perp$ gives $(C^\perp)^T = (C_T)^\perp$, completing (i).

Assume $t < d$. Then $n - d + 1 \le n - t$, implying any $n - t$ coordinates of $C$ contain an information set by Theorem 1.4.15. Therefore $C^T$ must be $k$-dimensional and hence $(C^\perp)_T = (C^T)^\perp$ has dimension $n - t - k$ by (i); this proves (ii).

As in (ii), (iii) is completed if we show that $C^T$ has dimension $k-1$. If $S \subset T$ with $S$ of size $d-1$, $C^S$ has dimension $k$ by part (ii). Clearly $C^S$ has minimum distance 1 and $C^T$ is obtained by puncturing $C^S$ on the nonzero coordinate of a weight 1 codeword in $C^S$. By Theorem 1.5 (ii) $C^T$ has dimension $k-1$.

### Exercise 28
Let \(\mathcal{C}\) be the binary repetition code of length $n$ as described in Example 1.2.2. Describe \((\mathcal{C}^\perp)_T\) and \((\mathcal{C}_T)^\perp\) for any $T$.

### Exercise 29
Let \(\mathcal{C}\) be the code of length 6 in Example 1.4.4. Give generator matrices for \((\mathcal{C}^\perp)_T\) and \((\mathcal{C}_T)^\perp\) when $T = \{1, 2\}$ and $T = \{1, 3\}$.

## 1.5.4 Direct sums

For $i \in \{1, 2\}$ let $\mathcal{C}_i$ be an $[n_i, k_i, d_i]$ code, both over the same finite field $\mathbb{F}_q$. Then their *direct sum* is the $[n_1 + n_2, k_1 + k_2, \min\{d_1, d_2\}]$ code

\[
\mathcal{C}_1 \oplus \mathcal{C}_2 = \{(\mathbf{c}_1, \mathbf{c}_2) | \mathbf{c}_1 \in C_1, \mathbf{c}_2 \in C_2\}.
\]

If $\mathcal{C}_i$ is generator matrix $G_i$ and parity check matrix $H_i$, then

\[
G_1 \oplus G_2 = \begin{bmatrix} G_1 & O \\ O & G_2 \end{bmatrix} \text{ and } H_1 \oplus H_2 = \begin{bmatrix} H_1 & O \\ O & H_2 \end{bmatrix} \quad (1.4)
\]

are a generator matrix and parity check matrix for $\mathcal{C}_1 \oplus \mathcal{C}_2$.

### Exercise 30
Let $\mathcal{C}_i$ have generator matrix $G_i$ and parity check matrix $H_i$ for $i \in \{1, 2\}$. Prove that the generator and parity check matrices for $\mathcal{C}_1 \oplus \mathcal{C}_2$ are as given in (1.4).

### Exercise 31
Let $\mathcal{C}$ be the binary code with generator matrix

| 1 | 1 | 0 | 0 | 1 | 1 | 0 |
|---|---|---|---|---|---|---|
| 1 | 0 | 0 | 1 | 0 | 1 | 1 |
| 1 | 0 | 0 | 1 | 1 | 1 | 0 |
| 1 | 0 | 1 | 0 | 1 | 1 | 0 |
| 1 | 0 | 0 | 1 | 0 | 1 | 1 |

Give another generator matrix for $\mathcal{C}$ that shows that $\mathcal{C}$ is a direct sum of two binary codes.

### Example 1.5.8
The [6, 3, 2] binary code $\mathcal{C}$ of Example 1.4.4 is the direct sum $\mathcal{D} \oplus \mathcal{D} \oplus \mathcal{D}$ of the [2, 1, 2] code $\mathcal{D} = (00, 11)$.

Since the minimum distance of the direct sum of two codes does not exceed the minimum distance of either of the codes, the direct sum of two codes is generally of little use in applications and is primarily of theoretical interest.

## 1.5.5 The [u | u + v] construction

Two codes of the same length can be combined to form a third code of twice the length in a way similar to the direct sum construction. Let $\mathcal{C}_i$ be an $[n, k_i, d_i]$ code for $i \in \{1, 2\}$,
