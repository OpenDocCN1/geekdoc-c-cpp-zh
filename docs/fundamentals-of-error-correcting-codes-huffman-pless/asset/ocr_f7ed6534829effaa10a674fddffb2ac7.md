Example 11.6.2 In this example we find a subcode \(\mathcal{C}_0\) of codimension 1 of a code \(\mathcal{C}\) where \(\rho(\mathcal{C}_0) = 2\rho(\mathcal{C}) + 1\). In the next theorem we will see that this is as large as possible. Let \(m \ge 2\) be an integer and let \(H_m\) be the \(m \times (2^m - 1)\) parity check matrix of the \([2^m - 1, 2^m - 1 - m, 3]\) binary Hamming code \(\mathcal{H}_m\). Let \(H'_m\) be the \(m \times (2^m - 2)\) matrix obtained from \(H_m\) by deleting its column of all 1s. Let \(r\) be a positive integer. Then the \(rm \times (r(2^m - 2) + 1)\) matrix

| 1 | \(H'_m\) | \(O\) | \(\cdots\) | \(O\) |
|---|---|---|---|---|
| 1 | \(O\) | \(H'_m\) | \(\cdots\) | \(O\) |
| \(\vdots\) | \(\vdots\) | \(\vdots\) | \(\ddots\) | \(\vdots\) |
| 1 | \(O\) | \(O\) | \(\cdots\) | \(H'_m\) |

is a parity check matrix of a code \(\mathcal{C}\) (which in fact is an ADS of \(r\) Hamming codes) of length \(r(2^m - 2) + 1\) with \(\rho(\mathcal{C}) = r\) by Exercise 657. The matrix

| \(H\) |
|---|
| \(1 \ 0 \ \cdots \ 0\) |

is a parity check matrix of a subcode \(\mathcal{C}_0\) of codimension 1 in \(\mathcal{C}\) with covering radius \(2r + 1\) also by Exercise 657.

+   **Exercise 657** With the notation of Example 11.6.2 do the following:
+   (a) Prove that \(\rho(\mathcal{C}) = r\).
+   (b) Prove that the syndrome of weight 1 with a 1 in its last position is not the sum of \(2r\) or fewer columns of \(H_0\).
+   (c) Prove that \(\rho(\mathcal{C}_0) = 2r + 1\).

In these last two examples we have produced codes \(\mathcal{C}\) and subcodes \(\mathcal{C}_0\) of codimension 1 where \(\rho(\mathcal{C}_0)\) is as small as possible (namely \(\rho(\mathcal{C})\)) and also as large as possible (namely \(2\rho(\mathcal{C}) + 1\)) as the following theorem found in [1] shows.

# **Theorem 11.6.3 (Adams Bound)** Let \(\mathcal{C}_0\) be a subcode of codimension 1 in a binary linear code \(\mathcal{C}\). Then

\(\rho(\mathcal{C}_0) \le 2\rho(\mathcal{C}) + 1.\) (11.14)

**Proof:** Suppose that \(\mathcal{C}\) is an \([n, n-m]\) code. Let \(H\) be an \(m \times n\) parity check matrix for \(\mathcal{C}\). We can add one row \(\mathbf{v} = v_1 \cdots v_n\) to \(H\) to form an \((m+1) \times n\) parity check matrix

\(H_0 = \begin{bmatrix} H \\ \mathbf{v} \end{bmatrix}\) (11.15)

For \(\mathcal{C}_0\), for \(j = 1, 2, \dots, n\), let the columns of \(H_0\) and \(H\) be denoted \(h_0^j\) and \(h^j\), respectively. Let \(\rho = \rho(\mathcal{C})\) and \(\rho_0 = \rho(\mathcal{C}_0)\). Assume (11.14) is false; so \(\rho_0 \ge 2\rho + 2\). There is a syndrome \(s_0 \in \mathbb{F}_2^{m+1}\) of \(\mathcal{C}_0\) which is the sum of \(\rho_0\) columns of \(H_0\) but no fewer. Rearrange the columns of \(H_0\) so that

\(s_0^T = \sum_{j=1}^{\rho_0} h_0^j.\) (11.16)