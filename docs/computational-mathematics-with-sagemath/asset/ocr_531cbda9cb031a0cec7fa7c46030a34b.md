| Basic operations | |
| --- | --- |
| transpose, conjugate | A.transpose(), A.conjugate() |
| scalar product | a*A |
| sum, product, k-th power, inverse | A + B, A * B, A^k, A^-1 or ~A |

TABLE 8.2 - Basic operations and matrix arithmetic.

**Embedding and Extension.** The method `base_extend` of a matrix space makes it possible to embed a matrix space into another matrix space with the same dimensions but over an extension of the base ring. This operation is however only valid for a field or a ring extension. In order to change the ring of a matrix space, following a ring morphism (when it exists), one uses instead the method `change_ring`.

```
```text
sage: MS = MatrixSpace(GF(3),2,3)
sage: MS.base_extend(GF(9,'x'))
Full MatrixSpace of 2 by 3 dense matrices over Finite Field
in x of size 3^2
sage: MS = MatrixSpace(ZZ,2,3)
sage: MS.change_ring(GF(3))
Full MatrixSpace of 2 by 3 dense matrices over Finite Field of size 3
```
```

**Mutability and Caching.** By default, matrix objects are mutable, which means that one can modify their members (namely their coefficients) after their construction. In order to protect the matrix against modification, one can make it immutable with the function `A.set_immutable()`. It is then still possible to create mutable copies of this matrix with the function `copy(A)`. Remark that the caching mechanism for the computed results, such as the rank, the determinant, etc., is always active, regardless of the mutability status.

# ### 8.1.4 Basic Operations on Matrices

Arithmetic operations on matrices are done with the usual operators `+,-,*,^`. The inverse of a matrix `A` is obtained equivalently by `A^-1` or `~A`. For a scalar `a` and a matrix `A`, the operation `a*A` corresponds to the scalar multiplication of the matrix space. For any other operation where a scalar `a` is provided in place of a matrix (as for instance in the operation `a+A`), this scalar is interpreted as the corresponding scalar matrix `aI_n` if `a != 0` if dimensions permit it. Elementwise product of two matrices is achieved by the method `elementwise_product`.

# ## 8.2 Matrix Computations

In linear algebra, matrices are typically used to represent families of vectors, systems of linear equations, linear transformations, or vector subspaces. Consequently, computing properties such as the rank of a family of vectors, the solution