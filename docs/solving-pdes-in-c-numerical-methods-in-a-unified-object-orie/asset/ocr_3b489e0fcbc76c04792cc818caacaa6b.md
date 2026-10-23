Here, only the nonzero blocks are indicated. Blocks that are not indicated are zero blocks. Blocks of the form B_i and Q_i correspond to the i th time step in the time-space grid and depend on the particular strategy of time marching.

More specifically, let A_i be the N × N matrix containing the discrete convection-diffusion spatial derivatives at the i th time step. (A_i is the same as D^(1) in Chapter 7, Section 3.) If the explicit scheme in Chapter 7, Section 5, is used, then

```
B_i = (Δt)^{-1} I and Q_i = (Δt)^{-1} I - A_i.
```

If, on the other hand, the implicit scheme in Chapter 7, Section 6, is used, then

```
B_i = (Δt)^{-1} I + A_i and Q_i = (Δt)^{-1} I.
```

Finally, if the semi-implicit scheme in Chapter 7, Section 7, is used, then

```
B_i = (Δt)^{-1} I + A_i / 2 and Q_i = (Δt)^{-1} I - A_i / 2.
```

Define the block-diagonal matrix B by

```
B = ( B1  B2  B3  ... )
```

Define also the matrix Q, whose only nonzero blocks lie below the main block diagonal:

```
Q = ( 0  Q1 B1^{-1}  0  Q2 B2^{-1} 0 ... )
```

With these definitions, the coefficient matrix A that governs the time marching can be decomposed as the product

```
A = (I - Q) B.
```

This decomposition will be useful in the stability analysis below.

In what follows, we consider the semi-implicit scheme, which is the most complex one. The explicit and implicit schemes can be analyzed in a similar way. In order to have stability for the explicit scheme, however, one must make sure that Δt is not too large in comparison to the meshsize h. This condition indicates that the explicit scheme may require many more time levels than the implicit and semi-implicit schemes, which can use larger Δt.

# 8.3 Stability in Time Marching

Marching in time in the time-space grid is equivalent to inverting the block-bidiagonal matrix A = (I - Q) B. Of course, in practice A is never inverted explicitly: by “inverting” we mean solving the linear system A u = F for the unknown vector u. Although A^{-1} is never computed explicitly, its mathematical properties are important in the stability analysis.