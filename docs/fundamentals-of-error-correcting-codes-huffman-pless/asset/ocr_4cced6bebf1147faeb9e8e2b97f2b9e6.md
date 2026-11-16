both over the same finite field $\mathbb{F}_q$. The $(\mathbf{u} \mid \mathbf{u} + \mathbf{v})$ construction produces the $[2n, k_1 + k_2, \min\{2d_1, d_2\}]$ code

```
$\mathcal{C} = \{(\mathbf{u}, \mathbf{u} + \mathbf{v}) \mid \mathbf{u} \in C_1, \mathbf{v} \in C_2\}.$
```

If $C_i$ has generator matrix $G_i$ and parity check matrix $H_i$, then generator and parity check matrices for $\mathcal{C}$ are

```
\(\begin{bmatrix} G_1 & G_1 \\ O & G_2 \end{bmatrix} \text{ and } \begin{bmatrix} H_1 & O \\ -H_2 & H_2 \end{bmatrix} . \quad (1.5)\)
```

+   **Exercise 32** Prove that generator and parity check matrices for the code obtained in the $(\mathbf{u} \mid \mathbf{u} + \mathbf{v})$ construction from the codes $C_i$ are as given in (1.5). $\diamond$

# **Example 1.5.9** Consider the $[8, 4, 4]$ binary code $\mathcal{C}$ with generator matrix

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

+   **Exercise 33** Prove that the $(\mathbf{u} \mid \mathbf{u} + \mathbf{v})$ construction using $[n, k_i, d_i]$ codes $C_i$ produces a code of dimension $k = k_1 + k_2$ and minimum weight $d = \min\{2d_1, d_2\}$. $\diamond$

# 1.6 Permutation equivalent codes

In this section and the next, we ask when two codes are “essentially the same.” We term this concept “equivalence.” Often we are interested in properties of codes, such as weight