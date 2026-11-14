![](bbox=[0.15, 0.02, 0.85, 0.44])

# Figure 11.31: A two-delay-line feedback network.

An equivalent way to look at Figure 11.31 is shown in Figure 11.32. You can see that the feedback coefficients have been grouped together in what looks like a linear algebra matrix. The total energy is preserved if the matrix of coefficients is unitary. A unitary matrix multiplied by its transpose matrix results in the identity matrix. The transpose matrix is formed by turning the rows into columns and vice versa. These matrices are square. The identity matrix is a square matrix whose diagonal values are all 1. An FDN that uses a unitary matrix for its coefficients is called a unitary feedback delay network or UFDN.

Examine the gain matrix $G$ in Equation 11.31:

```
$$ G = \begin{bmatrix} 0 & 1 \\ -1 & 0 \end{bmatrix} $$
```

Then multiplying it by its transpose yields

```
$$ GG^T = \begin{bmatrix} 0 & 1 \\ -1 & 0 \end{bmatrix} \begin{bmatrix} 0 & -1 \\ 1 & 0 \end{bmatrix} = \begin{bmatrix} 1 & 0 \\ 0 & 1 \end{bmatrix} \quad \dots \quad (11.31) $$
```