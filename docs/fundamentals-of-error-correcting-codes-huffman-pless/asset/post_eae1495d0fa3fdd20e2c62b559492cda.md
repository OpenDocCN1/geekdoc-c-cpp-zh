
$\mathcal{C}_1^\perp = \mathcal{D}_1$, the inner product of $c(x)$ and $m(x)$ is a nonzero multiple of the inner product of $j(x)$ with itself, which is nonzero. Thus any two lines of $\mathcal{L}$ intersect in at least one point. The size of the intersection $\ell_\epsilon \cap \ell_m$ is not changed but if $\ell_\epsilon$ and $\ell_m$ are shifted by the same amount. Hence by shifting $c(x)$ and $m(x)$ by $x^i$ for some $i$, we may assume $x^i \equiv \ell_\epsilon$ and $x^j \not\equiv \ell_\epsilon$ as $\ell_\epsilon \neq \ell_m$. We construct the $d_0 \times n$ matrix $\mathcal{M}$ from $c(x)$ as above. If $\ell$ is the support of any row of $\mathcal{M}$, then the size of $\ell \cap \ell_\epsilon$ is at least one, since we just showed that lines of $\mathcal{L}$ intersect in at least one point. Recall that each column of $\mathcal{M}$ except the first has exactly one nonzero entry. As $\ell_m$ intersects each of the rows of $\mathcal{M}$ in at least one coordinate and that cannot be the first coordinate, the size of $\ell \cap \ell_m$ must be exactly one because $wt(m(x)) = d_2$ and $\mathcal{M}$ has $d_0$ rows. One of the rows of $\mathcal{M}$ has support $\ell_\epsilon$ implying that $\ell_\epsilon \cap \ell_m$ has size one for all distinct lines. In particular, two points determine at most one line and every pair of lines intersects in exactly one point. To complete (iii)(b), we only need to show that two points determine at least one line. The set $\mathcal{L}$ is invariant under cyclic shifts as $\mathcal{D}_1$ is cyclic, and so we only need to show that $x^0$ and $x^i$, for $i > 0$, determine at least one line. But that is clear, as all lines corresponding to rows of $\mathcal{M}$ have a nonzero entry in coordinate $x^0$, and some row has a nonzero entry in coordinate $x^i$. It follows that $\mathcal{L}$ is a cyclic projective plane of order $d_0 - 1$ giving (iii)(b).

Let $c(x) = c_0 + c_1 x + \cdots + c_{n-1} x^{n-1} \in \mathcal{D}_1$ have weight $d_0$. Defining $\mathcal{M}$ as above, if $r > s$ and $c_r, c_s$ are nonzero, the unique nonzero entry of column $x^{r-s}$ of $\mathcal{M}$ is $c_r c_s$. The rows of $\mathcal{M}$ sum to a vector corresponding to $c(x)c(x^{-1}) = \delta(\vec{j})x$, where $\delta \neq 0$. Thus each column of $\mathcal{M}$ sums to $(1/n)\delta$. So if $i < j < k$ and $c_i, c_j, c_k$ are nonzero (three such values exist as $d_0 > 2$), $c_i c_j = c_i c_k = c_j c_k = (1/n)\delta$ implying that $c_i = c_j = c_k$. Hence (iii)(c) holds. There are \(\binom{n}{2} / \binom{d_2}{2} = n\) lines in $\mathcal{L}$, since every minimum weight codeword is a multiple of the binary vector corresponding to a line. (iii)(d) follows.

In part (iii) of the previous theorem, the restriction that $d_0 > 2$ is not significant because if $d_0 \le 2$ and $n = d_2^2 - d_0 + 1$, then $n \le 3$.

## Exercise 359

In this exercise, you will construct certain duadic codes over $\mathbb{F}_3$ of length 13. The 3-cyclotomic cosets modulo 13 are: $C_0 = \{0\}, C_1 = \{1, 3, 9\}, C_2 = \{2, 5, 6\}, C_4 = \{4, 10, 12\}, C_7 = \{7, 8, 11\}$.

Let $c_i(x) = \sum_{j \in C_i} x^j$.

- (a) Show that $c_1(x)^2 = c_2(x) - c_4(x)$. Then use $\mu_2$ to compute $c_2(x)^2, c_4(x)^2$, and $c_7(x)^2$.
- (b) Show that $c_1(x)c_2(x) = c_1(x) + c_2(x) + c_7(x)$ and $c_1(x)c_4(x) = c_2(x) + c_7(x)$. Then use $\mu_2$ to compute $c_i(x)c_j(x)$ for $i < j$ and $i, j \in \{1, 2, 4, 7\}$.
- (c) Construct generating idempotents for the two pairs of even-like duadic codes of length 13 over $\mathbb{F}_3$ whose splitting is given by $\mu_{-1}$. Hint: The generating idempotents each have weight 9. If $e(x)$ is such an idempotent, $e(x) + e(x)\mu_{-1} = 1 - \vec{j}(x)$.
- (d) Construct the generating idempotents for the two pairs of odd-like duadic codes of length 13 over $\mathbb{F}_3$ whose splitting is given by $\mu_{-1}$.

### Table 6.1 Binary duadic codes of length n ≤ 119

| n | Idempotent | d | d_b | a | Number of codes |
|---|---|---|---|---|---|
| 7 | 1* | 3 | 3 | -1‡ | 2 |
| 17 | 0, 1* | 5 | 5 | 3‡ | 2 |
| 23 | 1* | 7 | 7 | -1‡ | 2 |
| 31 | 1, 5, 7* | 7 | 7 | -1‡ | 2 |
| 31 | 1, 3, 5 | 7 | 7 | -1‡ | 6 |
| 41 | 0, 1* | 9 | 9 | 3‡ | 2 |
| 47 | 1* | 11 | 11 | -1‡ | 2 |
| 49 | 0, 1, 7 | 4 | 9 | -1‡ | 4 |
| 71 | 1* | 11 | 11 | -1‡ | 2 |
| 73 | 0, 1, 3, 5, 11 | 9 | 9 | -1‡ | 8 |
| 73 | 0, 1, 3, 5, 13 | 9 | 9 | -1‡ | 8 |
| 73 | 0, 1, 5, 9, 17 | 12 | 13 | 3‡ | 4 |
| 73 | 0, 1, 3, 9, 25* | 13 | 13 | 5‡ | 2 |
| 79 | 1* | 15 | 15 | -1‡ | 2 |
| 89 | 0, 1, 3, 5, 13 | 12 | 17 | -1‡ | 8 |
| 89 | 0, 1, 3, 5, 19 | 12 | 17 | -1‡ | 8 |
| 89 | 0, 1, 3, 11, 33 | 15 | 15 | 5‡ | 4 |
| 89 | 0, 1, 5, 9, 11* | 17 | 17 | 3‡ | 2 |
| 97 | 0, 1* | 15 | 15 | 5‡ | 2 |
| 103 | 1* | 19 | 19 | -1‡ | 2 |
| 113 | 0, 1, 9* | 15 | 15 | 3‡ | 2 |
| 113 | 0, 1, 3 | 18 | 19 | 9‡ | 4 |
| 119 | 0, 1, 13, 17, 21 | 4 | 15 | 3 | 4 |
| 119 | 0, 1, 7, 11, 51 | 6 | 15 | 3 | 4 |
| 119 | 0, 1, 7, 13, 17 | 8 | 15 | 3 | 4 |
| 119 | 0, 1, 7, 11, 17 | 12 | 15 | 3 | 4 |

- (e) Show that $1 + c_i(x)$ for $i \in \{1, 2, 4, 7\}$ are each in some code in part (d). Hint: Do this for $i = 1$ and then use $\mu_2$.

- (f) Write down all 13 cyclic shifts of $1 + c_1(x)$. What is the resulting structure?

Table 6.1 gives information about the odd-like binary duadic codes $\mathcal{D}$ of length $n \le 119$. The splittings given in this table are obtained in a manner similar to that of Example 6.4.8. The idempotent of $\mathcal{D}$ is of the form $\sum_{i \in \mathcal{I}} \sum_{c \in C} x^c$. The column "Idempotent" gives the index set $\mathcal{I}$ for each equivalence class of odd-like duadic codes; a * in this column means that the code is a quadratic residue code. The columns "d" and "d_b" are the minimum weight and minimum odd weight, respectively. The column "a" indicates the multiplier $\mu_a$ giving the splitting. An $\propto$ in column "a" indicates that the two extended odd-like duadic codes are duals of each other (i.e., $\mu_{-1}$ fixes each code by Theorem 6.4.12). If the splitting is given by $\mu_{-1}$, then by Theorem 6.5.1 the extended code is self-dual doubly-even if $n \equiv -1 \pmod 8$ and self-dual singly-even if $n \equiv 1 \pmod 8$. We denote the codes whose extensions are self-dual singly-even by † and the codes whose extensions are self-dual doubly-even by ‡ in the column “a”. Finally, the column “Number of codes” is the number of either even-like or odd-like duadic codes in an equivalence class of duadic codes constructed from the given splitting. (For example, a 6 in the “Number of codes” column means that there are six equivalent even-like codes and six equivalent odd-like codes in the class of codes represented by the given splitting.) Theorem 4.3.17 shows that equivalence is determined by multipliers except in the case n = 49, however, in that case using multipliers is enough to show that there is only one class. The table comes from [277]. (The values of d_b and d for the [113, 57, 18] code in the table were computed probabilistically in [277] and exactly in [315].) This code has higher minimum weight than the quadratic residue code of the same length.) The minimum weight codewords in the [7, 4, 3] and [73, 37, 9] codes support projective planes of orders 2 and 8, respectively; see Exercise 358. There are 16 duadic codes of length 73 containing projective planes of order 8; while the codes fall into two equivalence classes of eight codes each, the projective planes are all equivalent. The codes of length 31, which are not quadratic residue codes, are punctured Reed-Muller codes; see Example 6.4.8.

Information about the binary duadic odd-like codes of lengths 127 ≤ n ≤ 241 has been computed in [277]. We summarize some of this information in Table 6.2. In this table we list in the column labeled “d” the minimum weights that occur. The minimum weights reported here were computed probabilistically. Some of these were computed exactly in [315]; wherever exact minimum weights were found, they agreed with those computed in [277]. See [189, 277]. There may be several codes at each length. For example, if n = 217, there are 1024 duadic codes that fall into 88 equivalence classes by Theorem 4.3.17. Further information on the idempotents and splittings can be found in [277]. In the column “Comments”, we indicate if the extended codes are self-dual singly-even by † or self-dual doubly-even by ‡, or if the extended codes are duals of each other by ∞. By examining Tables 6.1 and 6.2, the square Root Bound is seen to be very useful for duadic codes of relatively small length but becomes weaker as the length gets longer.

Table 6.3, taken from [266], with certain values supplied by Philippe Gaborit, gives information about the odd-like duadic codes over $\mathbb{F}_4$ of odd lengths 3 through 41. No prime lengths p = −1 (mod 8) are listed as these duadic codes have the same generating idempotents as those given in Table 6.1; because these codes have a binary generator matrix, their minimum weight is the same as the minimum weight of the corresponding binary code by Theorem 3.8.8. For the same reasons we do not list those codes of prime length p ≡ 1 (mod 8) which have binary idempotents (also described in Table 6.1). The codes of length p ≡ −1 (mod 8) have extensions that are self-dual under both the ordinary and the Hermitian inner products; see Theorems 6.4.9 and 6.4.12 and Exercise 360. In Table 6.3, the column labeled “n” gives the length, “d” the minimum weight, and “d” the minimum weight of the extended code. Each row of the table represents a family of equivalent odd-like duadic codes that are permutation equivalent. The column “Number of codes” is the number of odd-like (or even-like) duadic codes in the equivalence class. In the “Comments” column, the symbol ♦ means that the splitting is given by μ_{-1} and so the extended codes are self-dual with respect to the ordinary inner product. The symbol ♡ means that the splitting is given by μ_{-2} and so the extended codes are self-dual with respect to the
