# SOLVING LINEAR EQUATIONS

proceed from right to left in the sweeping process: the first submatrix is {a_{ij}}\{i,j=2:n}, the second is the transformed version of {a_{ij}}\{i,j=3:n}, etc.

The new method for Matrix given below uses the ideas that have just been discussed.

```
Vector Matrix::gauss(const Vector & RHS) const {
  double multiplier = 0;
  Matrix G(nRows, nRows, pA);
  Vector h(nRows, RHS.pA);

  for(int j = 0; j < nCols; j++)//column to be swept
    for(int jj = j + 1; jj < nCols; jj++)//current operation column
      if(G[j][jj] == 0) {
        cout << "Oops! Division by 0!" << endl;
        exit(1);
      }

      for(int i = j + 1; i < nRows; i++)//work down rows
        multiplier = G[i][j]/G[j][j];
        pA[i][jj] = pA[i][jj] - multiplier*G.pA[j][jj];
    }

  for(int i = j + 1; i < nRows; i++)//do the same to the RHS
    multiplier = G[i][j]/G[j][j];
    h.pA[i] = h.pA[i] - multiplier*h.pA[j];

  Vector b = G.backward(h);
  return b;
}
```

The roles of ATemp and cTemp in our R calculations are occupied by G and h in this listing. These quantities are initialized using the (calling) matrix for the left-hand side and the right-side vector that is supplied as an argument to the method. The algorithm proceeds through the columns of G working only with elements below the diagonal also carrying out the same calculations on h using the backward method from the previous section. At the end of the recursion G is upper-triangular and the system is solved. One may now check that an application of this C++ routine to the matrix and vector created in R for our examples proves the statement.

The sweep algorithm O(n^3) flops (Exercise 7.3). Problems can arise with this approach when one of the diagonal elements of A or one of its Gauss transforms is small. This can be avoided by implementing a suitable row interchange strategy such as partial pivoting ensures that no multiplier can exceed one in magnitude (Exercise 7.2).

# 7.2.3 Cholesky decomposition

When the matrix A in our linear equation system is positive-definite, it can be transformed to upper-triangular form using the Cholesky decomposition. While this method can exhibit some numerical inaccuracies when the matrix in question is near singular, it is still useful today and occupies an important role in statistics.

To appreciate the basic premise before the Cholesky algorithm, suppose it is possible to