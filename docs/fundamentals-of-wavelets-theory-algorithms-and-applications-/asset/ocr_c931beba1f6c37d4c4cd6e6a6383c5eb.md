If m = n, A is a square matrix. An N × 1 column matrix (only one column) represents an N-dimensional vector.

# 2. Transposition: The transpose of A is A' whose element is Aji. If the dimension of A is m × n, the dimension of A' is n × m. The transposition of a column (N × 1) matrix is a row (1 × N) matrix.

# 3. Matrix sum and difference: Two matrices may be summed together if they have the same dimensions.

```
C = A ± B => Cij = Aij ± Bij
```

# 4. Matrix product: Multiplication of two matrices is meaningful only if their dimensions are compatible. Compatibility means the number of columns in the first matrix must be the same as the number of rows in the second matrix. If the dimensions of A and B are m × p and p × q respectively, the dimension of C = AB is m × q. The element Cij is given by

```
Cij = \sum_{k=1}^{p} A_{ik} B_{kj}
```

The matrix product is not commutative since p × q is not compatible with m × p. In general, AB ≠ BA.

# 5. Identity matrix: An identity matrix is a square matrix whose major diagonal elements are ones and the off-diagonal elements are zeros.