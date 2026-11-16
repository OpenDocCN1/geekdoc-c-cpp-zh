Two-scale relations relate the scaling function and the wavelets at a given scale with the scaling function at the next higher scale. Since

(5.24) \(\phi(t) \in A_0 \subset A_1, \text{ and}\)

(5.25) \(\psi(t) \in W_0 \subset A_1,\)

we should be able to write \(\phi(t)\), and \(\psi(t)\) in terms of the bases that generate \(A_1\). In other words, there exist two sequences \(\{g_0[k]\}\), \(\{g_1[k]\} \in l^2\) such that

(5.26) \(\phi(t) = \sum_k g_0[k] \phi(2t - k),\)

(5.27) \(\psi(t) = \sum_k g_1[k] \phi(2t - k).\)

Equations (5.26) and (5.27) are referred to as *two-scale relations*. In general, for any \(j \in \mathbb{Z}\), the relationship between \(A_j, W_j\) with \(A_{j+1}\) is governed by

\(\phi(2^j t) = \sum_k g_0[k] \phi(2^{j+1} t - k),\)
\(\psi(2^j t) = \sum_k g_1[k] \phi(2^{j+1} t - k).\)

By taking the Fourier transform of the two-scale relations, we have