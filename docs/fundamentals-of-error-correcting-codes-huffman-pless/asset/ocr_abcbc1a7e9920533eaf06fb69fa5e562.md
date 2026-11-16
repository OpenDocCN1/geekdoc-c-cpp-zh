Proof: Let \(\mathbf{z} = (\mathbf{x}, \mathbf{0}, \mathbf{y}) \in \mathbb{F}_2^{m_1+n_2-1}\). Clearly,

\(d(\mathbf{z}, C^{(0,n_1)}) = d((\mathbf{x}, \mathbf{0}), C_1^{(0,n_1)}) + d((\mathbf{0}, \mathbf{y}), C_2^{(0,1)}), \text{ and } d(\mathbf{z}, C^{(1,n_1)}) = d((\mathbf{x}, \mathbf{0}), C_1^{(1,n_1)}) + d((\mathbf{0}, \mathbf{y}), C_2^{(1,1)}) - 1.\)

Therefore adding these two equations and using the definitions

\(d(\mathbf{z}, C^{(0,n_1)}) + d(\mathbf{z}, C^{(1,n_1)}) \le N^{(n_1)}(C_1) + N^{(1)}(C_2) - 1.\) (11.13)

This also holds for \(\mathbf{z} = (\mathbf{x}, \mathbf{1}, \mathbf{y}) \in \mathbb{F}_2^{m_1+n_2-1}\). As (11.13) is true for all \(\mathbf{z} \in \mathbb{F}_2^{m_1+n_2-1}\), \(N^{(n_1)}(C) \le N^{(n_1)}(C_1) + N^{(1)}(C_2) - 1\).

Using Lemma 11.5.4 and the normality assumptions for \(C_1\) and \(C_2\), we see that

\(2\rho(C) \le N(C) \le N(C_1) + N(C_2) - 1 \le 2\rho(C_1) + 2\rho(C_2) + 1,\)

proving the theorem.

# **Exercise 654** Let \(C\) be a binary code of length \(n\). Prove the following:

+   (a) If \(\text{PAut}(C)\) is transitive, then \(N^{(i)}(C) = N^{(j)}(C)\) for \(1 \le i < j \le n\). Furthermore all coordinates are acceptable.

+   (b) If \(c \in C\) and \(\mathbf{x} \in \mathbb{F}_2^n\), then \(d(\mathbf{x} + c, C^{(0,l)}) + d(\mathbf{x} + c, C^{(1,l)}) = d(\mathbf{x}, C^{(0,l)}) + d(\mathbf{x}, C^{(1,l)}).\)

+   (c) The [7, 4, 3] binary Hamming code \(\mathcal{H}_3\) is normal and every coordinate is acceptable. Hint: By part (a) you only have to compute \(N^{(l)}(\mathcal{H}_3)\) as \(\mathcal{H}_3\) is cyclic. By part (b) you only have to check coset representatives \(\mathbf{x}\) of \(\mathcal{H}_3\) in \(\mathbb{F}_2^7\) when calculating \(d(\mathbf{x}, \mathcal{H}_3^{(1,l)}) + d(\mathbf{x}, \mathcal{H}_3^{(1,l)}).\)

+   (d) The [3, 1, 3] binary repetition code is normal and every coordinate is acceptable. \(\unknown\)

**Example 11.5.6** Let \(C_1 = C_2 = \mathcal{H}_3\) and let \(C\) be the ADS of \(C_1\) and \(C_2\). \(C\) is a [13, 7] code. As \(\mathcal{H}_3\) is perfect, \(\rho(\mathcal{H}_3) = 1\). By Exercise 654, \(\mathcal{H}_3\) is normal. Therefore by Theorem 11.5.5, \(\rho(C) \le 2\). If \(\rho(C) = 1\), then every syndrome in \(\mathbb{F}_2^6\) must be a combination of one column of a parity check matrix of \(C\), which is clearly impossible. Hence \(\rho(C) = 2\), implying that \(\ell(6, 2) \le 13\). Applying Exercise 652(a) shows that \(11 \le \ell(6, 2)\). If there is an [11, 5] binary code with covering radius 2, there is a [12, 6] binary code also with covering radius 2 obtained by taking the direct sum of the [11, 5] code with the repetition code of length 1. It can be shown that there is no [12, 6] binary code with covering radius 2; see [34, Theorem 8.8]. This verifies that \(\ell(6, 2) = 13\).

We conclude this section with a result, found in [41], that can be used to compute certain values of \(\ell(m, 2)\); this result is important in showing that there is no [12, 6] binary code with covering radius 2 as discussed in the preceding example.

# **Theorem 11.5.7** If \(C\) is an \([n, n-m]\) binary code with covering radius 2 and \(w\) is the weight of a nonzero vector in \(C^\perp\), then \(w(n+1-w) \ge 2^{m-1}\).