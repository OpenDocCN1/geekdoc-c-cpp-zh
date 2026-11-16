**Exercise 685** Find generator matrices in standard form for all self-dual codes of lengths \(n \le 4\), up to monomial equivalence. Give the type of each code.

If C has generator matrix in standard form (12.1), then \(C^\perp\) has generator matrix

\(\displaystyle G^\perp = \begin{bmatrix} -(B_1 + 2B_2)^T - C^T A^T & C^T \\ 2A^T & I_{k_1-k_2} \\ O & O \end{bmatrix}.\) (12.2)

where \(O\) is the \(k_2 \times (n - k_1 - k_2)\) zero matrix. In particular, \(C^\perp\) has type

\(4^{n-k_1-k_2}2^{k_2}.\) (12.3)

**Exercise 686** Give the generator matrix (12.2) of \(C^\perp\) for the code \(\mathcal{C}\) of Example 12.1.1.

**Exercise 687** Prove that \(G^\perp G^T\) is the zero matrix, where \(G\) is given in (12.1) and \(G^\perp\) is given in (12.2).

Unlike codes over \(\mathbb{F}_2\), the concept of weight of a vector in \(\mathbb{Z}_4^n\) can have more than one meaning. In fact, three different weights, and hence three different distances, are used when dealing with codes over \(\mathbb{Z}_4\). Let \(\mathbf{x} \in \mathbb{Z}_4^n\). Suppose that \(n_i(\mathbf{x})\) denotes the number of components of \(\mathbf{x}\) equal to \(a\) for all \(a \in \mathbb{Z}_4\). The **Hamming weight** of \(\mathbf{x}\) is \(w_H(\mathbf{x}) = n_1(\mathbf{x}) + n_2(\mathbf{x}) + n_3(\mathbf{x})\), the **Lee weight** of \(\mathbf{x}\) is \(w_L(\mathbf{x}) = n_1(\mathbf{x}) + 2n_2(\mathbf{x}) + n_3(\mathbf{x})\), and the **Euclidean weight** of \(\mathbf{x}\) is \(w_E(\mathbf{x}) = n_1(\mathbf{x}) + 4n_2(\mathbf{x}) + n_3(\mathbf{x})\). Thus components equaling 1 or 3 contribute 1 to each weight while 2 contributes 2 to the Lee and 4 to the Euclidean weight. The **Hamming, Lee, and Euclidean distances** between \(\mathbf{x}\) and \(\mathbf{y}\) are \(d_H(\mathbf{x}, \mathbf{y}) = w_H(\mathbf{x} - \mathbf{y})\), \(d_L(\mathbf{x}, \mathbf{y}) = w_L(\mathbf{x} - \mathbf{y})\), and \(d_E(\mathbf{x}, \mathbf{y}) = w_E(\mathbf{x} - \mathbf{y})\), respectively.

**Exercise 688** Do the following:
(a) What are the Hamming, Lee, and Euclidean weights of the vector \(120\,203\,303\)?
(b) What are the Hamming, Lee, and Euclidean distances between the vectors \(30\,012\,221\) and \(20\,202\,213\)?

**Exercise 689** Find the Hamming, Lee, and Euclidean weight distributions of the code \(\mathcal{C}\) of Example 12.1.1.

**Exercise 690** Let \(\mathcal{C}\) be a \(\mathbb{Z}_4\)-linear code that contains a codeword with only 1s and 3s. Prove that the Lee weight of all codewords in \(C^\perp\) is even.

The following theorem is the \(\mathbb{Z}_4\) analogue to Theorem 1.4.5(iv).

**Theorem 12.1.5** Let \(\mathcal{C}\) be a self-orthogonal \(\mathbb{Z}_4\)-linear code with \(\mathbf{c} \in C\). Then:
(i) \(w_L(\mathbf{c}) \equiv 0 \pmod 2\),
and
(ii) \(w_E(\mathbf{c}) \equiv 0 \pmod 4\).

**Exercise 691** Prove Theorem 12.1.5.

There are also analogues to the MacWilliams equations for \(\mathbb{Z}_4\)-linear codes \(\mathcal{C}\) of length \(n\).

Let

\(\displaystyle \text{Ham}_C(x, y) = \sum_{\mathbf{c} \in C} x^{w_H(\mathbf{c} - \mathbf{y})} y^{n - w_H(\mathbf{c})}\)