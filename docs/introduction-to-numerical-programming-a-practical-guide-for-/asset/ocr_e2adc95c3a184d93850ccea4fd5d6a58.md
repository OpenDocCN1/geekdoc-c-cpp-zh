and A′, we find that Relations 8.18 and 8.19 actually share the same structure. Finally, the elements of the matrix A′ modified as a result of the transformation R(i,j) may be cast under the form:

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