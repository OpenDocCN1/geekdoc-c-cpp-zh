
### Research Problem 12.5.3 Give an improved upper bound on the minimum Lee weight of self-dual codes over $\mathbb{Z}_4$

### Exercise 737 By Theorem 12.15, the Lee weight of every codeword in a self-orthogonal $\mathbb{Z}_4$-linear code is even. It is natural to ask what happens in a code over $\mathbb{Z}_4$ in which all codewords have Lee weight a multiple of 4.

- (a) Give an example of a vector in $\mathbb{Z}_4^n$ of Lee weight 4 that is not orthogonal to itself.
- (b) Unlike what occurs with codes where all Euclidean weights are multiples of 8, part (a) indicates that a code over $\mathbb{Z}_4$ in which all codewords have Lee weight a multiple of 4 is not necessarily self-orthogonal. However, if $\mathcal{C}$ is a self-dual $\mathbb{Z}_4$-linear code where all codewords have Lee weight a multiple of 4, then $\mathfrak{C}(\mathcal{C})$ is linear. Prove this. Hint: Let $\mathbf{u}, \mathbf{v} \in \mathcal{C}$. By Theorem 12.2(2i), $wt_L(\mathbf{u} - \mathbf{v}) = d_L(\mathbf{u}, \mathbf{v}) = d(\mathfrak{C}(\mathbf{u}), \mathfrak{C}(\mathbf{v})) = wt(\mathfrak{C}(\mathbf{u}) + \mathfrak{C}(\mathbf{v}))$. As $\mathcal{C}$ is linear, $\mathbf{u} - \mathbf{v} \in \mathcal{C}$. Also $wt_L(\mathbf{u}) = wt(\mathfrak{C}(\mathbf{u}))$ and $wt_L(\mathbf{v}) = wt(\mathfrak{C}(\mathbf{v}))$. Use these facts and $wt(\mathfrak{C}(\mathbf{u}) + \mathfrak{C}(\mathbf{v})) = wt(\mathfrak{C}(\mathbf{u})) + wt(\mathfrak{C}(\mathbf{v})) - 2wt(\mathfrak{C}(\mathbf{u}) \cap \mathfrak{C}(\mathbf{v}))$ together with our assumption to show $\mathfrak{C}(\mathbf{u})$ and $\mathfrak{C}(\mathbf{v})$ are orthogonal. Assessing the size of $\mathfrak{C}(\mathcal{C})$, show that the self-orthogonal binary linear code spanned by $\mathfrak{C}(\mathcal{C})$ cannot be larger than $\mathfrak{C}(\mathcal{C})$.

Let $\mathcal{C}$ be a $\mathbb{Z}_4$-linear code of length $n$. There are two binary linear codes of length $n$ associated with $\mathcal{C}$. The *residue code* $\text{Res}(\mathcal{C})$ is $\mu(\mathcal{C})$. The *torsion code* $\text{Tor}(\mathcal{C})$ is $\{\mathbf{b} \in \mathbb{F}_2^n \mid 2\mathbf{b} \in \mathcal{C}\}$. So the vectors in $\text{Tor}(\mathcal{C})$ are obtained from the vectors in $\mathcal{C}$ with all components 0 or 2 by dividing these components in half. If $\mathcal{C}$ has generator matrix $G$ in standard form (12.1), then $\text{Res}(\mathcal{C})$ and $\text{Tor}(\mathcal{C})$ have generator matrices

$$
G_{\text{Res}} = \begin{bmatrix} I_k & A & B_1 \end{bmatrix} \quad \text{and} \quad (12.13)
$$

$$
G_{\text{Tor}} = \begin{bmatrix} I_{k_1} & A & B_1 \\ O & I_{k_2} & C \end{bmatrix} \quad (12.14)
$$

So $\text{Res}(\mathcal{C}) \subseteq \text{Tor}(\mathcal{C})$. If $\mathcal{C}$ is self-dual, we have the following additional relationship between $\text{Res}(\mathcal{C})$ and $\text{Tor}(\mathcal{C})$.

**Theorem 12.5.4** If $\mathcal{C}$ is a self-dual $\mathbb{Z}_4$-linear code, then $\text{Res}(\mathcal{C})$ is doubly-even and $\text{Res}(\mathcal{C}) = \text{Tor}(\mathcal{C})^\perp$.

**Proof:** Suppose $\mathcal{C}$ has generator matrix $G$ given by (12.1). Denote one of the first $k_1$ rows of $G$ by $\mathbf{r} = (\mathbf{i}, \mathbf{a}\mathbf{b}_1 + 2\mathbf{b}_2)$, where $\mathbf{i}, \mathbf{a}, \mathbf{b}_1$, and $\mathbf{b}_2$ are rows of $I_k, A, B_1$, and $B_2$, respectively. Then $\mathbf{0} = \mathbf{r} \cdot \mathbf{r} \equiv \mathbf{i} \cdot \mathbf{i} + \mathbf{a} \cdot \mathbf{a} + \mathbf{b}_1 \cdot \mathbf{b}_1 \pmod 4$, implying that the rows of (12.13) are doubly-even and so are orthogonal to themselves. If $\mathbf{r}' = (\mathbf{i}', \mathbf{a}', \mathbf{b}'_1 + 2\mathbf{b}'_2)$ is another of the first $k_1$ rows of $G$, then

$$
\mathbf{r} \cdot \mathbf{r}' \equiv \mathbf{i} \cdot \mathbf{i}' + \mathbf{a} \cdot \mathbf{a}' + \mathbf{b}_1 \cdot \mathbf{b}'_1 + 2(\mathbf{b}_2 \cdot \mathbf{b}'_1 + \mathbf{b}_1 \cdot \mathbf{b}'_2) \pmod 4. \quad (12.15)
$$

If $\mathbf{s} = (\mathbf{0}, \mathbf{2}', 2\mathbf{c})$ is one of the bottom $k_2$ rows of $G$, using analogous notation, then

$$
\mathbf{r} \cdot \mathbf{s} \equiv 2\mathbf{a}' \cdot \mathbf{b}_1 \cdot \mathbf{c} \pmod 4. \quad (12.16)
$$

As $\mathbf{r} \cdot \mathbf{r}' \equiv \mathbf{r} \cdot \mathbf{s} \equiv 0 \pmod 4$, (12.15) and (12.16) imply that the rows of (12.13) are orthogonal as binary vectors to the rows of (12.14). Thus $\text{Res}(\mathcal{C}) \subseteq \text{Tor}(\mathcal{C})^\perp$; as $\mathcal{C}$ is self-dual, $2k_1 + k_2 = n$, implying $\text{Res}(\mathcal{C}) = \text{Tor}(\mathcal{C})^\perp$. In particular, $\text{Res}(\mathcal{C})$ is self-orthogonal and as it has a generator matrix with doubly-even rows, $\text{Res}(\mathcal{C})$ is doubly-even.

One consequence of this result is that a Type II code must contain a codeword with all entries $\pm 1$. This implies that Type II codes can exist only for lengths a multiple of 8. The simple proof we give of this was originally due to Gabidr.

**Corollary 12.5.5** Let $\mathcal{C}$ be a Type II code of length $n$. Then $\text{Tor}(\mathcal{C})$ is an even binary code, $\text{Res}(\mathcal{C})$ contains the all-one binary vector $1$, $\mathcal{C}$ contains a codeword with all entries $\pm 1$, and $n \equiv 0 (\text{mod } 8)$.

**Proof:** Let $c \in \text{Tor}(\mathcal{C})$. Then $2c \in \mathcal{C}$; as $\text{wt}_E(2c) \equiv 0 (\text{mod } 8)$, $c$ is a binary vector of even weight. Hence $\text{Tor}(\mathcal{C})$ is an even binary code. So $\text{Res}(\mathcal{C})$ contains the all-one binary vector $1$ as $\text{Res}(\mathcal{C}) = \text{Tor}(\mathcal{C})^\perp$ by Theorem 12.5.4. Any vector $v \in \mathcal{C}$ with $\mu(v) = 1$ has no entries 0 or 2; at least one such $v$ exists. As $0 \equiv \text{wt}_E(v) \equiv n (\text{mod } 8)$, the proof is complete.

If we start with an arbitrary doubly-even binary code, can we form a self-dual $\mathbb{Z}_4$-linear code with this binary code as its residue code? This is indeed possible, a fact we explore in the next section; but in order to do so, we need another form for the generator matrix.

**Corollary 12.5.6** Let $\mathcal{C}$ be a self-dual $\mathbb{Z}_4$-linear code with generator matrix in standard form. Then $\mathcal{C}$ has a generator matrix of the form

$$
G' = \begin{bmatrix} F & I_k + 2B \\ 2H & O \end{bmatrix},
$$

where $B$, $F$, and $H$ are binary matrices. Furthermore, generator matrices for $\text{Res}(\mathcal{C})$ and $\text{Tor}(\mathcal{C})$ are

$$
G'_{\text{Res}} = [F \quad I_k] \quad \text{and} \quad G'_{\text{Tor}} = \begin{bmatrix} F & I_k \\ H & O \end{bmatrix},
$$

respectively.

**Proof:** Let $k = k_1$ where $\mathcal{C}$ has type $4^k 2^{k_2}$. As $\mathcal{C}$ is self-dual, $k_2 = n - 2k$. We first show that $\mathcal{C}$ has a generator matrix of the form

$$
G'' = \begin{bmatrix} D & E & I_k + 2B \\ O & 2I_{n-2k} & 2C \end{bmatrix},
$$

where $B$, $C$, $D$, and $E$ are binary matrices. To verify this, we only need to show that we can replace the first $k = k_1$ rows of $G$ from (12.1) by $[D \quad E \quad I_k + 2B]$. By Theorems 12.5.4 and 1.6.2, the right-most $k$ coordinates of $\text{Res}(\mathcal{C})$ are information positions, as the left-most $n - k$ coordinates of $\text{Tor}(\mathcal{C})$ are information positions. Thus by (12.13), $B_1$ has binary rank $k$ and so has a binary inverse $D$. Hence the first $k$ rows of $G$ can be replaced by $[I_k \quad A_1 + 2B_2] = [D \quad E + 2E_1 \quad I_k + 2B_2]$, where $DA = E + 2E_1$ and $D(B_1 + 2B_2) = I_k + 2B_2$. Adding $E_1(O \quad 2I_{n-2k} \quad 2C)$ to this gives $G''$. Now add $2C[D \quad E \quad I_k + 2B]$ to the bottom $n - 2k$ rows of $G''$ to obtain $G'$. That $\text{Res}(\mathcal{C})$ and $\text{Tor}(\mathcal{C})$ have the stated generator matrices follows from the definitions of the residue and torsion codes.

## 12.5.1 Mass formulas

We can use the form of the generator matrix for a self-dual $\mathbb{Z}_4$-linear code given in Corollary 12.5.6 to count the total number of such codes. Let $\mathcal{C}$ be a self-dual $\mathbb{Z}_4$-linear code of type $4^k 2^{(n-2k)}$ with $0 \le k \le \lfloor n/2 \rfloor$. By Theorem 12.5.4, $\text{Res}(\mathcal{C})$ is an $[n, k]$ self-orthogonal doubly-even binary code, and we can apply a permutation matrix $P$ to $\mathcal{C}$ so that the generator matrix $G'$ of $\mathcal{C}P$ is given in Corollary 12.5.6. Conversely, if we begin with an $[n, k]$ self-orthogonal doubly-even binary code with generator matrix $[F \mid I_k]$ that generates $\text{Res}(\mathcal{C}P)$, we must be able to find the binary matrix $B$ to produce the first $k$ rows of $G'$. While the submatrix $H$ in $G'$ is not unique, its span is uniquely determined as $\text{Res}(\mathcal{C})^\perp = \text{Tor}(\mathcal{C})$. This produces a generator matrix for $\mathcal{C}P$ and from there we can produce $\mathcal{C}$. So to count the total number of codes $\mathcal{C}$ with a given residual code, we only need to count the number of choices for $B$.

Beginning with a generator matrix $[F \mid I_k]$, which generates an $[n, k]$ self-orthogonal doubly-even binary code $C_1$, choose $H$ so that

$$
\begin{bmatrix}
F & I_k \\
H & O
\end{bmatrix}
$$

generates $C_2 = C_1^\perp$. We now show that there are $2^{k(k+1)/2}$ choices for $B$ that yield self-dual $\mathbb{Z}_4$-linear codes with generator matrices of the form $G'$ given in Corollary 12.5.6. As the inner product modulo 4 of vectors whose components are only 0s and 2s is always 0, the inner product of two of the bottom $n - 2k$ rows of $G'$ is 0. Regardless of our choice of $B$, the inner product modulo 4 of one of the top $k$ rows of $G'$ with one of the bottom $n - 2k$ rows of $G'$ is also always 0 as $C_1^\perp = C_2$. Furthermore, the inner product modulo 4 of one of the top $k$ rows of $G'$ with itself is 0 regardless of the choice of $B$ because $C_1$ is doubly-even. Let $B = [b_{i,j}]$ with $1 \le i \le k$, $1 \le j \le k$. Choose the entries of $B$ on or above the diagonal (that is, $b_{i,j}$ with $1 \le i \le j \le k$) arbitrarily; notice that we are freely choosing $k(k + 1)/2$ entries. We only need to make sure that the inner product of row $i$ and row $j$ of $G'$, with $1 \le i < j \le k$, is 0 modulo 4. But this inner product modulo 4 is

$$
f_i \cdot f_j + 2(b_{i,j} + b_{j,i}). \quad (12.17)
$$

where $f_i$ and $f_j$ are rows $i$ and $j$ of $F$. As $C_1$ is self-orthogonal, $f_i \cdot f_j \equiv 0 \pmod 2$ implying that we can solve (12.17) for the binary value $b_{j,i}$ uniquely so that the desired inner product is 0 modulo 4. This proves the following result, first shown in [92].

**Theorem 12.5.7** For $0 \le k \le \lfloor n/2 \rfloor$, there are $v_{n,k} 2^{k(k+1)/2}$ self-dual codes over $\mathbb{Z}_4$ of length $n$ and type $4^k 2^{(n-2k)}$, where $v_{n,k}$ is the number of $[n, k]$ self-orthogonal doubly-even binary codes. The total number of self-dual codes over $\mathbb{Z}_4$ of length $n$ is

$$
\sum_{k=0}^{\lfloor n/2 \rfloor} v_{n,k} 2^{k(k+1)/2}.
$$
