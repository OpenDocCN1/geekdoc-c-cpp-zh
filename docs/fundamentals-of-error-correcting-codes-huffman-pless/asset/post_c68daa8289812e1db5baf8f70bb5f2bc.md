
set $\mathcal{S}$ if the following three conditions are fulfilled:
- (i) (reflexive) $\mathcal{C} \sim \mathcal{C}$ for all $\mathcal{C} \in \mathcal{S}$.
- (ii) (symmetric) if $\mathcal{C}_1 \sim \mathcal{C}_2$, then $\mathcal{C}_2 \sim \mathcal{C}_1$, and
- (iii) (transitive) if $\mathcal{C}_1 \sim \mathcal{C}_2$ and $\mathcal{C}_2 \sim \mathcal{C}_3$, then $\mathcal{C}_1 \sim \mathcal{C}_3$.

The set of coordinate permutations that map a code $\mathcal{C}$ to itself forms a *group*, that is, a set with an associative binary operation which has an identity and where all elements have inverses, called the *permutation automorphism group* of $\mathcal{C}$. This group is denoted by PAut($\mathcal{C}$). So if $\mathcal{C}$ is a code of length $n$, then PAut($\mathcal{C}$) is a subgroup of the *symmetric group* Sym$_n$.

### Exercise 38 Show that if $\mathcal{C}$ is the [$n$, 1] binary repetition code of Example 1.2.2, then PAut($\mathcal{C}$) = Sym$_n$.

### Exercise 39 Show that (1, 2)(5, 6), (1, 2, 3)(5, 6, 7), and (1, 2, 4, 5, 7, 3, 6) are automorphisms of the [7, 4] binary code $\mathcal{H}_3$ given in Example 1.2.3. These three permutations generate a group of order 168 called the *projective special linear group* PSL(2, 7). This is in fact the permutation automorphism group of $\mathcal{H}_3$.

Knowledge of the permutation automorphism group of a code can give important theoretical and practical information about the code. While these groups for some codes have been determined, they are in general difficult to find. The following result shows the relationship between the permutation automorphism group of a code and that of its dual; it also establishes the connection between automorphism groups of permutation equivalent codes. Its proof is left to the reader.

### Theorem 1.6.4 Let $\mathcal{C}$, $\mathcal{C}_1$, and $\mathcal{C}_2$ be codes over $\mathbb{F}_q$. *Then:*
- (i) PAut($\mathcal{C}$) = PAut($\mathcal{C}^\perp$),
- (ii) if $q = 4$, PAut($\mathcal{C}$) = PAut($\mathcal{C}^{1-\mu}$), and
- (iii) if $\mathcal{C}_1 P = \mathcal{C}_2$ for a permutation matrix $P$, then $P^{-1}$PAut($\mathcal{C}_1)P$ = PAut($\mathcal{C}_2$).

### Exercise 40 Prove Theorem 1.6.4.

One can prove that if two codes are permutation equivalent, so are their extensions; see Exercise 41. This is not necessarily the case for punctured codes.

### Exercise 41 Prove that if $\mathcal{C}_1$ and $\mathcal{C}_2$ are permutation equivalent codes, then so are $\widehat{\mathcal{C}_1}$ and $\widehat{\mathcal{C}_2}$.

### Example 1.6.5 Let $\mathcal{C}$ be the binary code with generator matrix
$$
G = \begin{bmatrix} 1 & 1 & 0 & 0 & 0 \\ 0 & 1 & 0 & 1 & 0 \\ 0 & 0 & 1 & 1 & 1 \end{bmatrix}.
$$

Let $\mathcal{C}_1^*$ and $\mathcal{C}_2^*$ be $\mathcal{C}$ punctured on coordinate 1 and 5, respectively. Then $\mathcal{C}_2^*$ has only even weight vectors, while $\mathcal{C}_1^*$ has odd weight codewords. Thus although $\mathcal{C}$ is certainly permutation equivalent to itself, $\mathcal{C}_1^*$ and $\mathcal{C}_2^*$ are not permutation equivalent.

In some instances, the group PAut(C) is transitive as a permutation group; thus for every ordered pair $(i, j)$ of coordinates, there is a permutation in PAut(C) which sends coordinate $i$ to coordinate $j$. When PAut(C) is transitive, we have information about the structure of its punctured codes. When PAut(C) is transitive, we have information about the minimum weight of C.

### Theorem 1.6.6 Let C be an $[n, k, d]$ code.
- (i) Suppose that PAut(C) is transitive. Then the $n$ codes obtained from C by puncturing C on a coordinate are permutation equivalent.
- (ii) Suppose that PAut(C) is transitive. Then the minimum weight $d$ of C is its minimum odd-like weight $d_o$. Furthermore, every minimum weight codeword of C is odd-like.

Proof: The proof of assertion (i) is left to the reader in Exercise 42. Now assume that PAut(C) is transitive. Applying (i) to $\widetilde{C}$ we conclude that puncturing $\widetilde{C}$ on any coordinate gives a code permutation equivalent to C. Let $e$ be a minimum weight vector of C and assume that $e$ is even-like. Then $wt(\widetilde{C}) = d$, where $\widetilde{c} \in \widetilde{C}$ is the extended vector. Puncturing $\widetilde{C}$ on a coordinate where $e$ is nonzero gives a vector of weight $d - 1$ in a code permutation equivalent to C, a contradiction.

### Exercise 42 Prove Theorem 1.6.6(i).

### Exercise 43 Let C be the code of Example 1.4.4.
- (a) Is PAut(C) transitive?
- (b) Find generator matrices for all six codes punctured on one point. Which of these punctured codes are equivalent?
- (c) Find generator matrices for all 15 codes punctured on two points. Which of these punctured codes are equivalent?

### Exercise 44 Let C = C_1 \oplus C_2, where C_1 and C_2 are of length $n_1$ and $n_2$, respectively. Prove that PAut(C_1) \oplus PAut(C_2) \subseteq PAut(C), where PAut(C_1) \oplus PAut(C_2) is the direct product of the groups PAut(C_1) (acting on the first $n_1$ coordinates of C) and PAut(C_2) (acting on the last $n_2$ coordinates of C).

For binary codes, the notion of permutation equivalence is the most general form of equivalence. However, for codes over other fields, other forms of equivalence are possible.

maps include those which rescale coordinates and those which are induced from field automorphisms (a topic we study more extensively in Chapter 3). We take up these maps one at a time.

First, recall that a *monomial matrix* is a square matrix with exactly one nonzero entry in each row and column. A monomial matrix $M$ can be written either in the form $DP$ or the form $PD_1$, where $D$ and $D_1$ are diagonal matrices and $P$ is a permutation matrix.

### Example 1.7.1 The monomial matrix
$$
M = \begin{bmatrix} 0 & a & 0 \\ 0 & 0 & b \\ c & 0 & 0 \end{bmatrix}
$$
equals
$$
DP = \begin{bmatrix} a & 0 & 0 \\ 0 & b & 0 \\ 0 & 0 & c \end{bmatrix} \begin{bmatrix} 0 & 1 & 0 \\ 0 & 0 & 1 \\ 1 & 0 & 0 \end{bmatrix} = PD_1 = \begin{bmatrix} 0 & 1 & 0 \\ 0 & 0 & 1 \\ 1 & 0 & 0 \end{bmatrix} \begin{bmatrix} c & 0 & 0 \\ 0 & a & 0 \\ 0 & 0 & b \end{bmatrix}
$$

We will generally choose the form $M = DP$ for representing monomial matrices; $D$ is called the *diagonal part* of $M$ and $P$ is the *permutation part*. This notation allows a more compact form using (1.6), as we now illustrate.

### Example 1.7.2 The monomial matrix $M = DP$ of Example 1.7.1 can be written

diag$(a, b, c)(1, 2, 3)$,

where diag$(a, b, c)$ is the diagonal matrix $D$ and $(1, 2, 3)$ is the permutation matrix $P$ written in cycle form.

We will apply monomial maps $M = DP$ on the right of row vectors $\mathbf{x}$ in the manner of the next example.

### Example 1.7.3 Let $M = \text{diag}(a, b, c)(1, 2, 3)$ be the monomial map of Example 1.7.2 and $\mathbf{x} = x_1 x_2 x_3 = (x_1, x_2, x_3)$. Then

$\mathbf{x}M = \mathbf{x}DP = (ax_1, bx_2, cx_3)P = (cx_3, ax_1, bx_2)$.

This example illustrates the more general principle of how to apply $M = DP$ to a vector $\mathbf{x}$ where $\sigma$ is the permutation (in cycle form) associated to $P$. For all $i$:
- first, multiply the $i$th component of $\mathbf{x}$ by the $i$th diagonal entry of $D$, and
- second, move this product to coordinate position $i\sigma$.

With this concept of monomial maps, we now are ready to define monomial equivalence. Let $\mathcal{C}_1$ and $\mathcal{C}_2$ be codes of the same length over a field $\mathbb{F}_q$, and let $G_1$ be a generator matrix for $\mathcal{C}_1$. Then $\mathcal{C}_1$ and $\mathcal{C}_2$ are *monomially equivalent* provided there is a monomial matrix $M$ so that $G_1 M$ is a generator matrix of $\mathcal{C}_2$. More simply, $\mathcal{C}_1$ and $\mathcal{C}_2$ are monomially equivalent if there is a monomial map $M$ such that $\mathcal{C}_2 = \mathcal{C}_1 M$. Monomial equivalence and permutation equivalence are precisely the same for binary codes.
