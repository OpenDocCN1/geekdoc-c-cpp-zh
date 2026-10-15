In terms of these, the entries βjj and αij, located on column j on and below the main diagonal, can be expressed in a unifying way:

```
βjj = ãjj,  (7.46)
αij = ãij / βjj,  i = j + 1, …, n.  (7.47)
```

The most advantageous pivot βjj on column j corresponds, evidently, to the largest of the elements ãij and, to ensure the stability of the algorithm, it should be placed on the diagonal.

Pivoting on column j actually starts with calculating in sequence the entries βij for i = 1, …, j − 1 (using Equation 7.42) and the entries ãij for i = j, …, n (from Equation 7.45). It should be noted that the elements ãij involve only already-calculated values of αik (located on the left, on the same row) and of βkj (located above, on the same column).

In parallel with calculating the elements ãij, their maximum also needs to be determined. Assuming the maximum to be ãlj, one has to interchange rows l and j to relocate it on the diagonal. According to Equation 7.46, the new entry ãjj takes on the role of the pivot βjj, while the rest of the elements ãij provide by divisions by βjj the elements αij of matrix L (according to Equation 7.47). It is noteworthy that at this stage, the entries on the right side of column j are still the initial ones of matrix A and the working array has the structure:

[ β11 ⋯ ⋯ β1j a1,j+1 ⋯ ⋯ ⋯ a1n ]
[ α21 ⋱ ⋮ ⋮ ]
[ ⋮ ⋱ ⋱ βj−1,j ⋮ ]
[ αj1 ⋯ ⋱ ãjj a j,j+1 ⋯ ⋯ ⋯ a jn ]
[ ⋮ ãj+1,j ⋱ ⋮ ]
[ ⋮ ⋮ ⋱ ⋱ ⋮ ]
[ αl1 ⋯ ⋯ ãlj a l,j+1 ⋱ ⋱ ⋯ a ln ]
[ ⋮ ⋮ ⋱ ⋱ ⋮ ]
[ αn1 ⋯ ⋯ ãnj a n,j+1 ⋯ ⋯ a n,n−1 a nn ]  (7.48)

We conclude this technical discussion by stressing that pivoting causes in general not the original matrix A being factorized, but rather a row-wise permutation thereof, and this essential aspect should be accounted for when using the LU decomposition to solve systems of linear equations or invert matrices.

The determinant of matrix A can be calculated as the product of the determinants of matrices L and U, which, owing to their triangular shape, amounts to the product of their diagonal elements:

```
det A = ∏_{j=1}^{n} βjj.  (7.49)
```

The LU factorization based on Doolittle’s method, regarded as a distinct task, is coded as the function LUFactor in Listing 7.7. The array a should contain on entry the elements of the original matrix A and it returns on exit the corresponding LU decomposition (7.44). Since, due to the applied pivoting, the decomposition results by factoring a row-wise permutation of A, the information is incomplete without the specification of the sequence of pivot rows. This information is essential when solving systems of linear equations, because the vector of constant terms b must undergo, albeit subsequently, the same permutations as the coefficient matrix A. For storing the indexes of the pivot rows, the routine uses the array ipivot. On the other hand, any permutation of rows is accounted for by changing the sign of the determinant.