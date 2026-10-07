
# SOLVING LINEAR EQUATIONS

proceed from right to left in the sweeping process: the first submatrix is $\{a_{ij}\}\{i,j=2:n\}$, the second is the transformed version of $\{a_{ij}\}\{i,j=3:n\}$, etc.

The new method for Matrix given below uses the ideas that have just been discussed.

```cpp
Vector Matrix::gauss(const Vector & RHS) const {
  double multiplier = 0;
  Matrix G(nRows, nRows, pA);
  Vector h(nRows, RHS.pA);

  for(int j = 0; j < nCols; j++)column to be swept
    for(int jj = j + 1; jj < nCols; jj++)current operation column
      if(G[j][jj] == 0) {
        cout << "Oops! Division by 0!" << endl;
        exit(1);
      }

      for(int i = j + 1; i < nRows; i++)work down rows
        multiplier = G[i][j]/G[j][j];
        pA[i][jj] = pA[i][jj] - multiplier*G.pA[j][jj];
    }

  for(int i = j + 1; i < nRows; i++)do the same to the RHS
    multiplier = G[i][j]/G[j][j];
    h.pA[i] = h.pA[i] - multiplier*h.pA[j];

  Vector b = G.backward(h);
  return b;
}
```

The roles of ATemp and cTemp in our R calculations are occupied by G and h in this listing. These quantities are initialized using the (calling) matrix for the left-hand side and the right-side vector that is supplied as an argument to the method. The algorithm proceeds through the columns of G working only with elements below the diagonal also carrying out the same calculations on h using the backward method from the previous section. At the end of the recursion G is upper-triangular and the system is solved. One may now check that an application of this C++ routine to the matrix and vector created in R for our examples proves the statement.

The sweep algorithm O(n^3) flops (Exercise 7.3). Problems can arise with this approach when one of the diagonal elements of A or one of its Gauss transforms is small. This can be avoided by implementing a suitable row interchange strategy such as partial pivoting ensures that no multiplier can exceed one in magnitude (Exercise 7.2).

## 7.2.3 Cholesky decomposition

When the matrix A in our linear equation system is positive-definite, it can be transformed to upper-triangular form using the Cholesky decomposition. While this method can exhibit some numerical inaccuracies when the matrix in question is near singular, it is still useful today and occupies an important role in statistics.

To appreciate the basic premise before the Cholesky algorithm, suppose it is possible to write $A = \{a_{ij}\} = LL^T$ for

```
$L = \begin{pmatrix} l_{11} & 0 & 0 & 0 \\ l_{21} & l_{22} & 0 & 0 \\ l_{31} & l_{32} & l_{33} & 0 \\ \vdots & \vdots & \vdots & \vdots \\ l_{n1} & l_{n2} & l_{n3} & l_{nn} \end{pmatrix}$
```

But, if that is the case, the system $A = LL^T$ can be solved directly for the elements $l_{ij}$ of $L$ in terms of the elements of $A$. This approach produces

```
$l_{11} = \sqrt{a_{11}}$
$l_{21} = a_{21}/l_{11}$
\vdots
$l_{n1} = a_{n1}/l_{11}$
```

which leads to

```
$l_{22} = \sqrt{a_{22}-l_{21}^2}$
$l_{32} = (a_{32}-l_{31}l_{21})/l_{22}$
\vdots
$l_{n2} = (a_{n2}-l_{n1}l_{21})/l_{22}$
```

The general or $j$th step is

```
$l_{jj} = \sqrt{a_{jj}-\sum_{k=1}^{j-1}l_{jk}^2} \quad (7.2)$
$l_{ij} = (a_{ij}-\sum_{k=1}^{j-1}l_{ik}l_{jk})/l_{jj}, \quad i=j+1,\dots,n. \quad (7.3)$
```

The Cholesky recursion can be summarized in Algorithm 7.2.

**Algorithm 7.2** Cholesky algorithm
$l_{11} = \sqrt{a_{11}}, a_{i1}/l_{11}, i=2,\dots,n$
for $j=2,\dots,n-1$ **do**
$l_{jj} = \sqrt{a_{jj}-\sum_{k=1}^{j-1}l_{jk}^2}$
$l_{ij} = (a_{ij}-\sum_{k=1}^{j-1}l_{ik}l_{jk})/l_{jj}, i=j+1,\dots,n$
**end for**
$l_{nn} = \sqrt{a_{nn}-\sum_{k=1}^{n-1}l_{nk}^2}$

The algorithm uses (7.2)–(7.3) to factorize $A$. Then, given $L$, the system $Ab=c$ is solved as noted in Section 7.2.1 by forward-substitution and back-solving.

Like Gaussian elimination the Cholesky algorithm has complexity on the order of $n^3$. However, one can show that it requires only half the effort of Gaussian elimination (Exercise 7.3).

```cpp
Forward-solve $L=c$ for $h$
Back-solve $L^Tb=h$ for $b$
return $b$
```

# SOLVING LINEAR EQUATIONS

The details required for implementing Algorithm 7.2 have been collected into another new method for class Matrix.

```cpp
Matrix::cholesky(const Vector& RHS) const {
    double temp = 0;
    Matrix G(nRows, nCols);
    for(int j = 0; j < nRows; j++){proceed by columns
        if(pA[j][j] == 0) {
            cout << "Singular system!" << endl;
            exit(1);
        }
        temp = pA[j][j];starting value for diagonal
        if (j > 0) {
            for(int k = 0; k < j; k++)
                temp += G[j][k];
        }
        G.pA[j][j] = sqrt(temp);
    }
    for(int i = j + 1; i < nRows; i++){now the rest
        temp = pA[i];
        for(int k = 0; k < j; k++)
            temp -= G[i][k];
        G.pA[i][j] = temp/G[j][j];
    }
    cout << "Cholesky factor:" << endl;
    G.printMatrix();
    Vector h = G.forward(RHS);
    Vector b = G.backward(h);
    return b;
}
```

The code implements the scheme of Algorithm 7.2 to compute the lower-triangular Cholesky factor and store it in a Matrix. In general there is no need to retain G, although the developments in Section 7.2.5 demonstrate this not always be the case. Once G has obtained it provides the matrix that is used in forward-solving the transpose of G is used for back-solving. An application of our Cholesky method to a matrix constructed for the previous section produces a Cholesky factor

| 1.678801 | 0 | 0 | 0 | 0 |
| -1.873512 | 1.383693 | 0 | 0 | 0 |
| -0.1240544 | 1.22679 | 0.767374 | 0 | 0 |
| -2.497718 | 0.600928 | 1.135503 | 0.362715 | 0 |
| -0.064936 | -0.762812 | -0.869516 | -1.025312 | 0.590260 |

```
-303.8929
-99.34466
153.1515
-128.2426
-33.69567
```The solution agrees with the one returned previously by Gaussian elimination. To check the accuracy of the Cholesky factor we can compare it to answers produced with the R function that performs a Cholesky factorization: namely,

```
> chol(A)
  [1]         [2]         [3]         [4]         [5]
[1] 1.678801 -1.873512 -0.124054 -2.497715 -0.644936
[2] 0.000000  1.383693  1.227898  0.600928 -0.768212
[3] 0.000000  0.000000  0.767374  1.135502 -0.869516
[4] 0.000000  0.000000  0.000000  0.367215 -1.025312
[5] 0.000000  0.000000  0.000000  0.000000  0.590620
```

The two Cholesky factors agree apart from the fact that the R function returns the upper-triangular factor. Thus, to solve a system in R with the Cholesky factorization uses forward-solving with the transpose of the upper-triangular factor and back-solving with the factor returned from chol. In terms of this translates to

```r
> U <- chol(A)
  h <- forwardsolve(t(U), cVector)
  backsolve(U, h)
[1] -30.89287 -99.34466 153.15147 -128.24258 -33.69657
```

A second option is to use the inverse matrix $A^{-1}$ computed via the Cholesky method. This is accomplished with the chol2inv function which takes the Cholesky factor obtained from chol as input. Again, for example this produces

```r
> chol2inv(chol(A))%%Vector
  [1]
[1] -30.89287
[2] -99.34466
[3] 153.15147
[4] -128.24258
[5] -33.69657
```

## 7.2.4 Banded matrices

Of interest is that the matrix $A = \{a_{ij}\}$ is said to be band-limited structure with bandwidth $q$ if $a_{ij} = 0$ whenever $|i - j| > q$. For example, the matrix below is $6 \times 6$ and two-banded

| a11 | a12 | a13 | 0 | 0 | 0 |
| a21 | a22 | a23 | a24 | 0 | 0 |
| a31 | a32 | a33 | a34 | a35 | 0 |
| 0 | a42 | a43 | a44 | a45 | a46 |
| 0 | 0 | a53 | a54 | a55 | a56 |
| 0 | 0 | 0 | a64 | a65 | a66 |

In the case of a positive-definite matrix $A$, it is easy to see that the matrix $L$ in the Cholesky factorization has the same lower bandwidth as $A$ (Exercise 7.6). Thus, the order of computation can be substantially reduced by restricting attention to the nonzero matrix elements.

Suppose, that we are not at the boundary; that is, for a given index $i$, $i \pm q$ are row and column indices. Then, by retracing our previous arguments in the nonbanded
