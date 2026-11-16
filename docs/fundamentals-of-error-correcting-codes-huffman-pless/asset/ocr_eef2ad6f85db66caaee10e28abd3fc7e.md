# Table 11.5 Covering radius \(\rho\) of extremal Type II binary codes of length \(n \le 64\)

| n | 8 | 16 | 24 | 32 | 40 | 48 | 56 | 64 |
|---|---|---|---|---|---|---|---|---|
| k | 4 | 8 | 12 | 16 | 20 | 24 | 28 | 32 |
| d | 4 | 4 | 8 | 8 | 8 | 12 | 12 | 12 |
| \(\rho\) | 2 | 4 | 4 | 6 | 6-8 | 8 | 8-10 | 8-12 |

the extended quadratic residue code; see Research Problem 9.3.7. Part of the coset weight distribution of the extended quadratic residue code is given in [62]; from this the complete coset distribution can be computed.

There are many similarities between the coset distributions of the length 32 Type II codes discussed in Exercise 643 and those of length 48. For example, the cosets of weights 1 through 5 and 7 in the length 48 codes have uniquely determined coset distributions and uniquely determined numbers of cosets. The cosets of weight 8 also have uniquely determined distributions but not number of cosets of weight 8.

**Exercise 644** Verify the bounds given in Table 11.5 for \(n = 40, 56,\) and \(64\). When \(n = 40\), the number of weight 8 codewords in an extremal Type II code is 285. When \(n = 56\), the number of weight 12 codewords in an extremal Type II code is 8190. When \(n = 64\), the number of weight 12 codewords in an extremal Type II code is 2976.

Near the end of Section 9.4 we defined the child of a self-dual code. Recall that if \(\mathcal{C}\) is an \([n, n/2, d]\) self-dual binary code with \(d \ge 3\), then a child \(\mathcal{C}''\) of \(\mathcal{C}\) is obtained by fixing two coordinates, taking the subcode \(\mathcal{C}'\) that is 00 or 11 on those two coordinates, and then puncturing \(\mathcal{C}'\) on those fixed coordinates. This produces an \([n-2, (n-2)/2, d^*]\) self-dual code with \(d^* \ge d-2\). The child of a self-dual code can have a larger covering radius than the parent as the following result shows.

**Theorem 11.4.2** Let \(\mathcal{C}\) be an \([n, n/2, d]\) self-dual code with \(d \ge 3\). Suppose that \(\mathcal{C}''\) is a child of \(\mathcal{C}\). Then \(\rho(\mathcal{C}'') \ge d - 1\).

**Proof:** Suppose that the two fixed coordinates which are used to produce \(\mathcal{C}''\) are the two left-most coordinates. Let \(\mathcal{C}'\) be as above. Choose \(\mathbf{x} \in \mathcal{C}\) to have minimum nonzero weight among all codewords of \(\mathcal{C}\) which are 10 or 01 on the first two coordinates. So \(\mathbf{x} = 10\mathbf{y}\) or \(01\mathbf{y}\). As adding a codeword \(\mathbf{c}'\) of \(\mathcal{C}'\) to \(\mathbf{x}\) produces a codeword \(\mathbf{c} = \mathbf{c}' + \mathbf{x}\) of \(\mathcal{C}\) with first two coordinates 01 or 10, wt(\(\mathbf{y}\)) by the choice of \(\mathbf{x}\). This means that \(\mathbf{y}\) must be a coset leader of the coset \(\mathbf{y} + \mathcal{C}''\). Since wt(\(\mathbf{y}\)) \(\ge d - 1\), the result follows.

A child of the \([24, 12, 8]\) extended binary Golay code is a \([22, 11, 6]\) extremal Type I code discussed in Example 9.4.12. Its covering radius is three more than that of its parent as Exercise 645 shows.

**Exercise 645** Let \(\mathcal{C}\) be the \([24, 12, 8]\) extended binary Golay code and \(\mathcal{C}''\) its child. Prove that \(\rho(\mathcal{C}'') = 7\).