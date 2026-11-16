definitely not be codewords. A generator matrix for the repetition code is

$G = [1 | 1 \cdots 1]$,

which is of course in standard form. The corresponding parity check matrix from Theorem 1.2.1 is

$H = \begin{bmatrix} 1 \\ 1 \\ \vdots \\ 1 \end{bmatrix} \quad I_{n-1} \end{bmatrix}$

The first coordinate is an information set and the last \(n-1\) coordinates form a redundancy set.

**Exercise 2** How many information sets are there for the \([n, 1]\) repetition code of Example 1.2.2?

**Example 1.2.3** The matrix \(G = [I_4 | A]\), where

\(G = \begin{bmatrix} 1 & 0 & 0 & 0 & 0 & 1 & 1 \\ 0 & 1 & 0 & 0 & 1 & 0 & 1 \\ 0 & 0 & 1 & 0 & 1 & 1 & 0 \\ 0 & 0 & 0 & 1 & 1 & 1 & 1 \end{bmatrix}\)

is a generator matrix in standard form for a \([7,4]\) binary code that we denote by \(\mathcal{H}_3\). By Theorem 1.2.1 a parity check matrix for \(\mathcal{H}_3\) is

\(H = [A^T | I_3] = \begin{bmatrix} 0 & 1 & 1 & 1 & 1 & 0 & 0 \\ 1 & 0 & 1 & 1 & 0 & 1 & 0 \\ 1 & 1 & 0 & 1 & 0 & 0 & 1 \end{bmatrix}\)

This code is called the \((7, 4)\) _Hamming code_.

**Exercise 3** Find at least four information sets in the \((7, 4)\) code \(\mathcal{H}_3\) from Example 1.2.3. Find at least one set of four coordinates that do not form an information set.

Often in this text we will refer to a _subcode_ of a code \(\mathcal{C}\). If \(\mathcal{C}\) is not linear (or not known to be linear), a subcode of \(\mathcal{C}\) is any subset of \(\mathcal{C}\). If \(\mathcal{C}\) is linear, a subcode will be a subset of \(\mathcal{C}\) which must also be linear; in this case a subcode of \(\mathcal{C}\) is a subspace of \(\mathcal{C}\).

# 1.3 Dual codes

The generator matrix \(G\) of an \([n, k]\) code \(\mathcal{C}\) is simply a matrix whose rows are independent and span the code. The rows of the parity check matrix \(H\) are independent; hence \(H\) is the generator matrix of some code, called the _dual_ or _orthogonal_ of \(\mathcal{C}\) and denoted \(\mathcal{C}^\perp\). Notice that \(\mathcal{C}^\perp\) is an \([n, n-k]\) code. An alternate way to define the dual code is by using inner products.