of a code to obtain an equivalent code provided the scalars are invertible elements of $\mathbb{Z}_4$. To that end, we say that $\mathcal{C}_1$ and $\mathcal{C}_2$ are *monomially equivalent* provided there is an \(n \times n\) monomial matrix \(M\) with all nonzero entries equal to 1 or 3 such that \(\mathcal{C}_2 = \mathcal{C}_1 M\). The permutation automorphism group PAut(\(\mathcal{C}\)) of \(\mathcal{C}\) is the set of all permutation matrices \(P\) such that \(\mathcal{C} P = \mathcal{C}\), while the monomial automorphism group MAut(\(\mathcal{C}\)) of \(\mathcal{C}\) is the set of all monomial matrices \(M\) (with nonzero entries 1 and 3) such that \(\mathcal{C} M = \mathcal{C}\).

**Exercise 680** Show that the $\mathbb{Z}_4$-linear codes with generator matrices
\(G_1 = \begin{bmatrix} 1 & 1 & 1 & 3 \\ 0 & 2 & 0 & 2 \\ 0 & 0 & 2 & 2 \end{bmatrix} \quad \text{and} \quad G_2 = \begin{bmatrix} 1 & 1 & 1 & 1 \\ 2 & 0 & 0 & 2 \\ 0 & 2 & 0 & 2 \end{bmatrix}\)
are monomially equivalent.

**Exercise 681** Find PAut(\(\mathcal{C}\)) and MAut(\(\mathcal{C}\)), where \(\mathcal{C}\) is the code in Example 12.1.1.

Every \([n, k]\) linear code over \(\mathbb{F}_q\) is permutation equivalent to a code with generator matrix in standard form \([I_k | A]\) by Theorem 1.6.2. In a similar way, there is a standard form for the generator matrix of a $\mathbb{Z}_4$-linear code. A generator matrix \(G\) of a $\mathbb{Z}_4$-linear code \(\mathcal{C}\) is in *standard form* if

\(G = \begin{bmatrix} I_{k_1} & A & B_1 + 2B_2 \\ O & 2I_{k_2} & 2C \end{bmatrix} . \quad (12.1)\)

where \(A, B_1, B_2\), and \(C\) are matrices with entries from \(\mathbb{Z}_2\), and \(O\) is the \(k_2 \times k_1\) zero matrix. The code \(\mathcal{C}\) is of type \(4^{k_1}2^{k_2}\). Notice that the generator matrix for the code of Example 12.1.1 is in standard form. Although rather tedious, the proof of the following result is straightforward.

**Theorem 12.1.3** Every $\mathbb{Z}_4$-linear code is permutation equivalent to a code with generator matrix in standard form.

**Exercise 682** Prove Theorem 12.1.3.

There is a natural inner product, the ordinary dot product modulo 4, on $\mathbb{Z}_4^n$ defined by \(\mathbf{x} \cdot \mathbf{y} = x_1y_1 + x_2y_2 + \cdots + x_ny_n \pmod 4\) ,
where \(\mathbf{x} = x_1 \cdots x_n\) and \(\mathbf{y} = y_1 \cdots y_n\). As with linear codes over finite fields, we can define the *dual code* \(\mathcal{C}^\perp\) of a $\mathbb{Z}_4$-linear code \(\mathcal{C}\) of length \(n\) by \(\mathcal{C}^\perp = \{ \mathbf{x} \in \mathbb{Z}_4^n \mid \mathbf{x} \cdot \mathbf{c} = 0 \text{ for all } \mathbf{c} \in \mathcal{C} \}\). By Exercise 683, \(\mathcal{C}^\perp\) is indeed a $\mathbb{Z}_4$-linear code. A $\mathbb{Z}_4$-linear code is *self-orthogonal* when \(\mathcal{C} \subseteq \mathcal{C}^\perp\) and *self-dual* if \(\mathcal{C} = \mathcal{C}^\perp\).

**Exercise 683** Prove that the dual code of a $\mathbb{Z}_4$-linear code is a $\mathbb{Z}_4$-linear code.

**Exercise 684** Prove that the code of Example 12.1.1 is self-dual.

**Example 12.1.4** Unlike codes over finite fields, there are self-dual $\mathbb{Z}_4$-linear codes of odd length. For example, the code of length \(n\) and type \(2^n\) with generator matrix \(2I_n\) is self-dual