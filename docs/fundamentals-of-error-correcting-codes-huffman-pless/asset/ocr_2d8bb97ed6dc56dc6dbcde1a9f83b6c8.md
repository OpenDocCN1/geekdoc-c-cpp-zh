Consider first the case $m_1 = 0, m_2 = m_3 = 1$. By Theorem 14.4.7, $k_L = 3L + 1$ for all $L$. Hence Theorem 14.4.10 shows that

```
$d_{free} \le \min\{\Delta(4, 1), \Delta(8, 4), \Delta(12, 7), \dots \}$.
```

The values $\Delta(4, 1) = \Delta(8, 4) = \Delta(12, 7) = 4$ can be found in [32] or deduced from Table 2.1. Thus $d_{free}$ is at most 4. In fact it can be shown that $d_{free}$ is at most 3 for this code; see [235, Theorem 7.10]. $C_3$ from Exercise 822 is a $(4, 3, 2, 3)$ code with these Forney indices; see Exercise 829.

Next consider the case $m_1 = m_2 = 0, m_3 = 2$. By Theorem 14.4.7, $k_0 = 2$ and $k_L = 3L + 1$ for all $L \ge 1$. So,

```
$d_{free} \le \min\{\Delta(4, 2), \Delta(8, 4), \Delta(12, 7), \dots \}$.
```

Since $\Delta(4, 2)$ is easily seen to be 2, $d_{free} \le 2$. The code $\mathcal{C}_4$ from Exercise 822 is a $(4, 3, 2, 2)$ code with these Forney indices; see Exercise 830.

Section 4 of [235] contains tables showing bounds on the free distance of $(n, k, m)$ codes using a slightly weaker bound similar to that of Theorem 14.4.10 for $(n, k) = (2, 1), (3, 1), (3, 2), (4, 1), \text{and } (4, 3)$ with values of $m$ up to 10. These tables also give codes that come closest to meeting these bounds. The bounds are most often met; when not met, except for one case, the codes have free distance one less than the value from the bound.

# Exercise 831 Let $\mathcal{C}$ be a $(3, 2, 3)$ convolutional code.

+   (a) Find the two possible sets of Forney indices for $\mathcal{C}$.
+   (b) Find the values of $k_L$ for each set of Forney indices found in (a).
+   (c) Give an upper bound on the free distance of $\mathcal{C}$ for each set of Forney indices found in (a).

# 14.5 Catastrophic encoders

When choosing an encoder for a convolutional code, there is one class of generator matrices that must be avoided – the so-called catastrophic encoders. In this section we see the problem that arises with their use.

We digress a bit before discussing catastrophic encoders. Let $G$ be a $k \times n$ matrix over a field $\mathbb{F}$ with $k \le n$. Recall that a right inverse of $G$ is an $n \times k$ matrix $K$ with entries in $\mathbb{F}$ such that $GK = I_k$. By a result of linear algebra $G$ has a right inverse if and only if it has rank $k$. In general, if $k < n$, there are many possible right inverses. Now suppose that $G$ is the generator matrix of either an $[n, k]$ block code or an $(n, k)$ convolutional code. Then $G$ has rank $k$ and hence has a right inverse $K$. If $\mathbf{x}$ is a message of length $k$ that was encoded to produce the codeword $\mathbf{c} = \mathbf{x}G$, then $\mathbf{x}$ can be recovered from $\mathbf{c}$ by observing that $\mathbf{x} = \mathbf{x}I_k = \mathbf{x}GK = \mathbf{c}K$; see also Section 1.11.1.

# Exercise 832 Consider the binary matrix

```
$G = \begin{bmatrix} 1 & 1 & 0 & 1 & 1 \\ 1 & 0 & 1 & 1 & 0 \\ 1 & 0 & 1 & 1 & 0 \end{bmatrix}$.
```