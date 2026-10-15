
One of the mathematically equivalent ways of expressing the solution, which will reveal its virtues later on, is

```
tan φ = [ (a₁₁ − a₂₂)/(2a₂₁) ± √(((a₁₁ − a₂₂)/(2a₂₁))² + 1) ]⁻¹ .
```

Rather than expressing herefrom the angle φ itself, one can determine numerically most efficiently the function values cos φ = (1 + tan φ)⁻¹/² and sin φ = tan φ cos φ, which are necessary for specifying both the matrices R and A′.

Finally, the eigenvalues of A are obtained by evaluating the diagonal elements of the transformed matrix A′ using the determined cos φ and sin φ, while the corresponding eigenvectors are the columns of the rotation matrix R:

```
λ₁ = a′₁₁,   x⁽¹⁾ = [ cos φ ; sin φ ],
λ₂ = a′₂₂,   x⁽²⁾ = [ − sin φ ; cos φ ].
```

To sum up this case, the diagonalization of (2 × 2) matrices can be performed exactly, by a single orthogonal transformation.

In the n-dimensional space, the rotation matrix can be generalized to operate with respect to the axis defined by the pair of coordinates i and j,

```
R(i,j) = [ 1   ⋮    ⋮   0 ; … cos φ … − sin φ … ] row i
          [ …   ⋮   ⋱   ⋮   ]
          [ … sin φ … cos φ … ] row j
          [ 0   ⋮    ⋮   1 ]
          column i   column j   (8.15)
```

differing from the unit matrix only by the four nonzero elements aᵢᵢ = aⱼⱼ = cos φ and aᵢⱼ = −aⱼᵢ = − sin φ, located at the intersection of rows and columns i and j. The rotation matrix R(i,j) is meant to carry out the orthogonal transformation

```
A′ = Rᵀ(i,j) · A · R(i,j),   (8.16)
```

which makes the off-diagonal elements a′ᵢⱼ and a′ⱼᵢ vanish.

The only elements of A′ which differ from those of A are located on the rows and columns i and j, since, by left-multiplying A with Rᵀ(i,j), only rows i and j get modified, while by the subsequent right-multiplication with R(i,j), only columns i and j are affected. In fact, defining the intermediate matrix Ã, we can rewrite the transformations (8.16) as

```
Ã = A · R(i,j),   A′ = Rᵀ(i,j) · Ã.   (8.17)
```

The detailed calculations for the matrix $\tilde{\mathbf{A}}$,

```
$\tilde{\mathbf{A}} \equiv \begin{bmatrix} \tilde{a}_{1i} & \tilde{a}_{1j} \\ \vdots & \vdots \\ \dots \tilde{a}_{ki} \dots \tilde{a}_{kj} \dots \\ \vdots & \vdots \\ \tilde{a}_{ni} & \tilde{a}_{nj} \end{bmatrix} = \begin{bmatrix} a_{1i} & a_{1j} \\ \vdots & \vdots \\ \dots a_{ki} \dots a_{kj} \dots \\ \vdots & \vdots \\ a_{ni} & a_{nj} \end{bmatrix} \cdot \begin{bmatrix} 1 & \vdots & \vdots & 0 \\ \dots & \cos\varphi & \dots & -\sin\varphi & \dots \\ \vdots & \ddots & \vdots & \\ \dots & \sin\varphi & \dots & \cos\varphi & \dots \\ 0 & \vdots & \vdots & 1 \end{bmatrix}, $
```

yield relevant elements differing from those of $\mathbf{A}$ located solely on columns $i$ and $j$:

```
$\begin{cases} \tilde{a}_{ki} = a_{ki}\cos\varphi + a_{kj}\sin\varphi, & k = 1,2,\dots,n, \\ \tilde{a}_{kj} = -a_{ki}\sin\varphi + a_{kj}\cos\varphi. \end{cases}$ (8.18)
```

Furthermore, the matrix $\mathbf{A}'$ may be expressed as

```
$\mathbf{A}' \equiv \begin{bmatrix} \vdots \\ a'_{i1} \dots a'_{ik} \dots a'_{in} \\ \vdots \\ a'_{j1} \dots a'_{jk} \dots a'_{jn} \\ \vdots \end{bmatrix} = \begin{bmatrix} 1 & \vdots & \vdots & 0 \\ \dots & \cos\varphi & \dots & \sin\varphi & \dots \\ \vdots & \ddots & \vdots & \\ \dots & -\sin\varphi & \dots & \cos\varphi & \dots \\ 0 & \vdots & \vdots & 1 \end{bmatrix} \cdot \begin{bmatrix} \vdots \\ \tilde{a}_{i1} \dots \tilde{a}_{ik} \dots \tilde{a}_{in} \\ \vdots \\ \tilde{a}_{j1} \dots \tilde{a}_{jk} \dots \tilde{a}_{jn} \\ \vdots \end{bmatrix}, $
```

and has as relevant elements differing from those of $\tilde{\mathbf{A}}$ situated only on rows $i$ and $j$:

```
$\begin{cases} a'_{ik} = \tilde{a}_{ik}\cos\varphi + \tilde{a}_{jk}\sin\varphi, & k = 1,2,\dots,n, \\ a'_{jk} = -\tilde{a}_{ik}\sin\varphi + \tilde{a}_{jk}\cos\varphi. \end{cases}$ (8.19)
```

To express the modified elements of the transformed matrix $\mathbf{A}'$ in terms of those of the initial matrix $\mathbf{A}$, one has to bear in mind that the elements at the intersections of rows and columns $i$ and $j$ result by applying both transformations (8.18) and (8.19), whereas the rest of the elements of these rows and columns are obtained by applying just one of the transformations. Considering also the symmetry of $\mathbf{A}$ and A′, we find that Relations 8.18 and 8.19 actually share the same structure. Finally, the elements of the matrix A′ modified as a result of the transformation R(i,j) may be cast under the form:

```
a'_{jk} = a'_{ki} = a_{ik} cos φ + a_{jk} sin φ,    k = 1,2,...,n,
a'_{jk} = a'_{kj} = -a_{ik} sin φ + a_{jk} cos φ,    k ≠ i,j,
a'_{ii} = a_{ii} cos² φ + 2a_{ji} sin φ cos φ + a_{jj} sin² φ,
a'_{jj} = a_{ii} sin² φ - 2a_{ji} sin φ cos φ + a_{jj} cos² φ,
a'_{ij} = a'_{ji} = a_{ji}(cos² φ - sin² φ) + (a_{jj} - a_{ii}) sin φ cos φ.  (8.20)
```

Imposing the condition that the elements a'_{ij} and a'_{ji} given by the last relation vanish, results in a second-order algebraic equation in cot φ:

```
cot² φ + (a_{jj} - a_{ii})/a_{ji} cot φ - 1 = 0.  (8.21)
```

Its solution can be inverted to give

```
tan φ = [ (a_{ii} - a_{jj})/(2a_{ji}) ± sqrt( ((a_{ii} - a_{jj})/(2a_{ji}))² + 1 ) ]^{-1},  (8.22)
```

by the use of which one can evaluate the functions

```
cos φ = 1 / sqrt(1 + tan² φ),    sin φ = cos φ tan φ,  (8.23)
```

necessary for specifying the transformed elements from Formulas 8.20. Still, one is faced with the problem of justifying the choice of one of the signs in Equation 8.22.

On the basis of the pattern defined by Equation 8.16, one can define a sequence of similar matrices,

```
A₀ = A,    A₁ = R₁ᵀ · A₀ · R₁, ...,    Aₗ = Rₗᵀ · Aₗ₋₁ · Rₗ, ...,  (8.24)
```

which, by virtue of Theorem 8.2, have the same set of eigenvalues. At each stage, the rotation Rₗ ≡ R(iₗ,jₗ) corresponds to a sequentially chosen combination of indexes (iₗ ≠ jₗ) and its purpose is to make the two symmetric off-diagonal elements located at the intersection of the rows and columns iₗ and jₗ vanish. Even though, according to Equations 8.20, possible zeros created by previous transformations are partially destroyed, they are nevertheless replaced by linear combinations of off-diagonal elements, weighted with subunitary functions (sin φₗ and cos φₗ) and, hence, an overall reduction of the off-diagonal elements results.

By defining the orthogonal matrices

```
Xₗ = R₀ · R₁ ⋯ Rₗ,    l = 0,1,2,...,  (8.25)
```

with X₀ ≡ R₀ ≡ E, the sequence of orthogonal transformations (8.24) may be rewritten:

```
A₀ = A,    A₁ = X₁ᵀ · A · X₁, ...,    Aₗ = Xₗᵀ · A · Xₗ, ...  (8.26)
```

At the limit, Aₗ is identified with the matrix Λ, having on the diagonal the eigenvalues of the original matrix A, while Xₗ is identified with the modal matrix X, having on the columns the corresponding eigenvectors:

```
lim_{l→∞} Aₗ = Λ,    lim_{l→∞} Xₗ = X.
```

Establishing the recurrence relation

X_l = X_{l-1} · R_l(i,j),

the modified elements of X_l can be obtained in terms of the elements of X_{l-1} from equations similar to (8.18):

x'_{ki} = x_{ki} cos φ + x_{kj} sin φ,   k = 1,2,…,n,
 x'_{kj} = -x_{ki} sin φ + x_{kj} cos φ.   (8.27)

In practical implementations, the sequence of approximations (8.26) is interrupted at some step l, for which the absolute values of the off-diagonal elements of matrix A_l have dropped in absolute value below a predefined tolerance ε > 0. The stopping condition of this iterative process can be thus formulated as

max_{i≠j} |a'_{ij}| ≤ ε,   (8.28)

and, when satisfied, one can consider the diagonal elements of A_l to approximate “sufficiently well” the eigenvalues of matrix A, and the columns of X_l to approximate the corresponding eigenvectors.

The discussion about the appropriate sign in Expression 8.22 of tan φ is nontrivial. In fact, the convergence of the Sequence 8.26 and, at the same time, the numerical stability of the method is ensured by choosing at each step in Formula 8.22 the minimal solution (tan φ ≤ 1), implying a rotation of the basis vectors by a minimal angle (φ ≤ π/4). This choice implies maximizing the absolute value of the denominator in Equation 8.22 by considering the “+” sign, if (a_{ii} − a_{jj})/a_{ji} > 0, and the “−” sign in the opposite case. Herewith, the tangent of the rotation angle takes the effective form:

tan φ = sign( (a_{ii} − a_{jj})/(2a_{ji}) ) [ | (a_{ii} − a_{jj})/(2a_{ji}) | + sqrt( ((a_{ii} − a_{jj})/(2a_{ji}))^2 + 1 ) ]^{-1}.   (8.29)

Regarding the stability of the Jacobi method, interesting insights can be gained by taking a different route to solving Equation 8.21. Rewriting it first as an equation in tan φ, it leads directly to the alternative solution

tan φ = (a_{jj} − a_{ii})/(2a_{ji}) ± sqrt( ((a_{jj} − a_{ii})/(2a_{ji}))^2 + 1 ),

which is perfectly equivalent from a pure mathematical perspective with the previous Result 8.22. However, since minimizing this expression implies rewriting it under the form

tan φ = sign( (a_{jj} − a_{ii})/(2a_{ji}) ) [ | (a_{jj} − a_{ii})/(2a_{ji}) | − sqrt( ((a_{jj} − a_{ii})/(2a_{ji}))^2 + 1 ) ]

and thus performing subtractions with operands close in absolute value, using the above relation instead of Equation 8.29 favors the onset of instabilities due to the propagation of the roundoff errors.

Listing 8.1 presents the coding of the Jacobi method for calculating the eigenvalues and eigenvectors of real symmetric matrices according to the algorithm described above.

To reduce the storage requirements, the implementation makes use of the symmetry of the matrices A_l. Specifically, for the 2n(n + 1)/2 = n² + n relevant elements of both matrices A and A_l, the routine employs just a single array a with n rows and n columns, supplemented by a vector d with n components. With a view to subsequent calculations, the elements of the original matrix A are secured in the upper triangle of array a, including the diagonal. The off-diagonal elements of the matrices A_l are temporarily
