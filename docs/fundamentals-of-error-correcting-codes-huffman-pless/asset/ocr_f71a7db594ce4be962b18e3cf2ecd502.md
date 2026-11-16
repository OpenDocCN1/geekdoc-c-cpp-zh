# Table 12.2 Indecomposable self-dual codes over $\mathbb{Z}_4$ of length $1 \le n \le 16$

| n | Type I | Type II | n | Type I | Type II | n | Type I | Type II |
|---|---|---|---|---|---|---|---|---|
| 1 | 1 | 0 | 7 | 1 | 0 | 13 | 7 | 0 |
| 2 | 0 | 0 | 8 | 2 | 4 | 14 | 92 | 0 |
| 3 | 0 | 0 | 9 | 0 | 0 | 15 | 111 | 0 |
| 4 | 1 | 0 | 10 | 4 | 0 | 16 | ? | 123 |
| 5 | 0 | 0 | 11 | 2 | 0 | | | |
| 6 | 1 | 0 | 12 | 31 | 0 | | | |

exercise you deduced that, up to equivalence, the only self-dual codes of lengths 2 and 3 are $2A_1$ and $3A_1$, respectively, where $2A_1$ is the direct sum of two copies of $A_1$. You also discovered that, up to equivalence, there are two inequivalent self-dual codes of length 4: the decomposable code $4A_1$ and the indecomposable code $D_4$ with generator matrix

```
\(\left[\begin{array}{ c c c c }
1 & 1 & 1 & 1 \\
0 & 2 & 0 & 2 \\
0 & 0 & 2 & 2
\end{array}\right]\)
```

Table 12.2 contains the number of inequivalent indecomposable Type I and Type II codes of length $n$ with $1 \le n \le 16$; this data is taken from [59, 85, 276]. While the real work in the classification is to find the indecomposable codes, using the mass formula requires a list of both the indecomposable and the decomposable codes.

# **Exercise 740**

Let $\mathcal{C}$ be a self-orthogonal code of length $n$ over $\mathbb{Z}_4$. Suppose that $\mathcal{C}$ contains a codeword with one component equal to 2 and the rest equal to 0. Prove that $\mathcal{C}$ is equivalent to a direct sum of $A_1$s and a self-dual code of length $n-1$. $\unknown$

# **Exercise 741**

Let $\mathcal{C}$ be equivalent to a direct sum $\mathcal{C}_1 \oplus \mathcal{C}_2$ of the indecomposable codes $\mathcal{C}_1$ and $\mathcal{C}_2$. Also let $\mathcal{C}$ be equivalent to a direct sum $\mathcal{D}_1 \oplus \mathcal{D}_2$ of the indecomposable codes $\mathcal{D}_1$ and $\mathcal{D}_2$. Prove that $\mathcal{C}_1$ is equivalent to either $\mathcal{D}_1$ or $\mathcal{D}_2$, while $\mathcal{C}_2$ is equivalent to the other $\mathcal{D}_j$. $\unknown$

# **Exercise 742**

Construct one indecomposable self-dual code of length 6 over $\mathbb{Z}_4$. Also construct one indecomposable self-dual code of length 7. Hint: For length 7, check Table 12.1. $\unknown$

Table 12.3 presents the total number of inequivalent Type I and Type II codes of length $n$ with $1 \le n \le 16$. The Type II codes represented in this table all have minimum Euclidean weight 8 and hence are Euclidean-extremal by Theorem 12.5.1.

# **Example 12.5.9**

From Table 12.2, there are four indecomposable Type II codes of length 8 and two indecomposable Type I codes. The decomposable self-dual codes of length 8 are $8A_1$, $4A_1 \oplus D_4$, $2A_1 \oplus E_6$, $A_1 \oplus E_7$, and $2D_4$, where $E_6$ and $E_7$ are the indecomposable codes of lengths 6 and 7, respectively, constructed in Exercise 742. All the decomposable