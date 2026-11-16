
both over the same finite field $\mathbb{F}_q$. The $(\mathbf{u} \mid \mathbf{u} + \mathbf{v})$ construction produces the $[2n, k_1 + k_2, \min\{2d_1, d_2\}]$ code

```
$\mathcal{C} = \{(\mathbf{u}, \mathbf{u} + \mathbf{v}) \mid \mathbf{u} \in C_1, \mathbf{v} \in C_2\}.$
```

If $C_i$ has generator matrix $G_i$ and parity check matrix $H_i$, then generator and parity check matrices for $\mathcal{C}$ are

```
\(\begin{bmatrix} G_1 & G_1 \\ O & G_2 \end{bmatrix} \text{ and } \begin{bmatrix} H_1 & O \\ -H_2 & H_2 \end{bmatrix} . \quad (1.5)\)
```

### Exercise 32 Prove that generator and parity check matrices for the code obtained in the $(\mathbf{u} \mid \mathbf{u} + \mathbf{v})$ construction from the codes $C_i$ are as given in (1.5). $\diamond$

### Example 1.5.9 Consider the $[8, 4, 4]$ binary code $\mathcal{C}$ with generator matrix

```
\(G = \begin{bmatrix} 1 & 1 & 0 & 1 & 0 & 1 & 0 & 1 \\ 0 & 0 & 1 & 0 & 1 & 0 & 1 & 0 \\ 0 & 0 & 1 & 1 & 0 & 0 & 1 & 1 \\ 0 & 0 & 0 & 0 & 1 & 1 & 1 & 1 \end{bmatrix} .\)
```

Then $\mathcal{C}$ can be produced from the $[4, 3, 2]$ code $C_1$ and the $[4, 1, 4]$ code $C_2$ with generator matrices

```
\(G_1 = \begin{bmatrix} 1 & 0 & 1 & 0 \\ 0 & 1 & 0 & 1 \\ 0 & 0 & 1 & 1 \end{bmatrix} \text{ and } G_2 = [1 \quad 1 \quad 1 \quad 1],\)
```

respectively, using the $(\mathbf{u} \mid \mathbf{u} + \mathbf{v})$ construction. Notice that the code $C_1$ is also constructed using the $(\mathbf{u} \mid \mathbf{u} + \mathbf{v})$ construction from the $[2, 2, 1]$ code $C_3$ and the $[2, 1, 2]$ code $C_4$ with generator matrices

```
\(G_3 = \begin{bmatrix} 1 & 0 \\ 0 & 1 \end{bmatrix} \text{ and } G_4 = [1 \quad 1],\)
```

respectively. $\blacksquare$

Unlike the direct sum construction of the previous section, the $(\mathbf{u} \mid \mathbf{u} + \mathbf{v})$ construction can produce codes that are important for reasons other than theoretical. For example, the family of Reed-Muller codes can be constructed in this manner as we see in Section 1.10. The code in the previous example is one of these codes.

### Exercise 33 Prove that the $(\mathbf{u} \mid \mathbf{u} + \mathbf{v})$ construction using $[n, k_i, d_i]$ codes $C_i$ produces a code of dimension $k = k_1 + k_2$ and minimum weight $d = \min\{2d_1, d_2\}$. $\diamond$

## 1.6 Permutation equivalent codes

In this section and the next, we ask when two codes are “essentially the same.” We term this concept “equivalence.” Often we are interested in properties of codes, such as weight distribution, which remain unchanged when passing from one code to another that is essentially the same. Here we focus on the simplest form of equivalence, called permutation equivalence, and generalize this concept in the next section.

One way to view codes as “essentially the same” is to consider them “the same” if they are isomorphic as vector spaces. However, in that case the concept of weight, which we will see is crucial to the study and use of codes, is lost: codewords of one weight may be sent to codewords of a different weight by the isomorphism. A theorem of MacWilliams [212], which we will examine in Section 7.9, states that a vector space isomorphism of two binary codes of length \(n\) that preserves the weight of codewords (that is, send codewords of one weight to codewords of the same weight) can be extended to an isomorphism of \(\mathbb{F}_2^n\) that is a permutation of coordinates. Clearly any permutation of coordinates that sends one code to another preserves the weight of codewords, regardless of the field. This leads to the following natural definition of permutation equivalent codes.

Two linear codes \(C_1\) and \(C_2\) are permutation equivalent provided there is a permutation of coordinates which sends \(C_1\) to \(C_2\). This permutation can be described using a permutation matrix, which is a square matrix with exactly one 1 in each row and column and 0s elsewhere. Thus \(C_1\) and \(C_2\) are permutation equivalent provided there is a permutation matrix \(P\) such that \(G_1\) is a generator matrix of \(C_1\) if and only if \(G_1 P\) is a generator matrix of \(C_2\). The effect of applying \(P\) to a generator matrix is to rearrange the columns of the generator matrix. If \(P\) is a permutation sending \(C_1\) to \(C_2\), we will write \(C_1 P = C_2\), where \(C_1 P = \{ \mathbf{y} \mid \mathbf{y} = \mathbf{x} P \text{ for } \mathbf{x} \in C_1 \}\).

### Exercise 34 Prove that if \(G_1\) and \(G_2\) are generator matrices for code \(C\) of length \(n\) and \(P\) is an \(n \times n\) permutation matrix, then \(G_1 P\) and \(G_2 P\) are generator matrices for \(C P\).

### Exercise 35 Suppose \(C_1\) and \(C_2\) are permutation equivalent codes where \(C_1 P = C_2\) for some permutation matrix \(P\). Prove that:

- (a) \(C_1^T P = C_2^T\), and
- (b) if \(C_1\) is self-dual, so is \(C_2\).

### Example 1.6.1 Let \(C_1\), \(C_2\), and \(C_3\) be binary codes with generator matrices

```
\(G_1 = \begin{bmatrix} 1 & 1 & 0 & 0 & 0 & 0 \\ 0 & 0 & 1 & 1 & 0 & 0 \\ 0 & 0 & 0 & 0 & 1 & 1 \end{bmatrix}, \quad G_2 = \begin{bmatrix} 1 & 0 & 0 & 0 & 0 & 1 \\ 0 & 0 & 1 & 0 & 0 & 0 \\ 0 & 1 & 0 & 0 & 1 & 0 \end{bmatrix}, \quad \text{and}\)
```

```
\(G_3 = \begin{bmatrix} 1 & 1 & 0 & 0 & 0 & 0 \\ 1 & 0 & 1 & 0 & 0 & 0 \\ 1 & 1 & 1 & 1 & 1 & 1 \end{bmatrix}.\)
```

respectively. All three codes have weight distribution \(A_0 = A_6 = 1\) and \(A_2 = A_4 = 3\). (See Example 1.4.4 and Exercise 17.) The permutation switching columns 2 and 6 sends \(G_1\) to \(G_2\), showing that \(C_1\) and \(C_2\) are permutation equivalent. Both \(C_1\) and \(C_2\) are self-dual, consistent with (a) of Exercise 35. \(C_3\) is not self-dual. Therefore \(C_1\) and \(C_3\) are not permutation equivalent by part (b) of Exercise 35.

The next theorem shows that any code is permutation equivalent to one with generator matrix in standard form.

### Theorem 1.6.2 Let C be a linear code.

- (i) C is permutation equivalent to a code which has generator matrix in standard form.
- (ii) If I and R are information and redundancy positions, respectively, for C, then R and I are information and redundancy positions, respectively, for the dual code C^\perp.

Proof: For (i), apply elementary row operations to any generator matrix of C. This will produce a new generator matrix of C which has columns the same as those in I_k, but possibly in a different order. Now choose a permutation of the columns of the new generator matrix so that these columns are moved to the order that produces [I_k | A]. The code generated by [I_k | A] is equivalent to C.

If I is information set for C, then by row reducing a generator matrix for C, we obtain columns in the information positions that are the columns of I_k in some order. As above, choose a permutation matrix P to move the columns so that C P has generator matrix [I_k | A]; P has moved I to the first k coordinate positions. By Exercise 1.2.1, (C P)^\perp has the last n - k coordinates as information positions. By Exercise 35, (C P)^\perp = C^\perp P, implying that R is a set of information positions for C^\perp, proving (ii).

It is often more convenient to use permutations (in cycle form) rather than permutation matrices to express equivalence. Let Sym_n be the set of all permutations of the set of n coordinates. If \sigma \in Sym_n and x = x_1 x_2 ... x_n, define

```
x\sigma = y_1 y_2 ... y_n, where y_j = x_{j\sigma^{-1}} for 1 \le j \le n.
```

So x\sigma = xP, where P = [p_{i,j}] is the permutation matrix given by

```
p_{i,j} = \begin{cases} 1 & \text{if } j = i\sigma, \\ 0 & \text{otherwise.} \end{cases} (1.6)
```

This is illustrated in the next example.

### Example 1.6.3 Let n = 3, x = x_1 x_2 x_3, and \sigma = (1, 2, 3). Then 1\sigma^{-1} = 3, 2\sigma^{-1} = 1, and 3\sigma^{-1} = 2. So x\sigma = x_3 x_1 x_2. Let

```
P = \begin{bmatrix} 0 & 1 & 0 \\ 0 & 0 & 1 \\ 1 & 0 & 0 \end{bmatrix}.
```

Then xP also equals x_3 x_1 x_2.

### Exercise 36 If \sigma, \tau \in Sym_n, show that x(\sigma\tau) = (x\sigma)\tau.

### Exercise 37 Let S be the set of all codes over F_q of length n. Let C_1, C_2 \in S. C_1 \sim C_2 to mean that there exists an n \times n permutation matrix P such that C_1 P = C_2. Prove that \sim is an equivalence relation on S. Recall that \sim is an equivalence relation on a
