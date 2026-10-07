# 238
NUMERICAL LINEAR ALGEBRA

stored in n(q+1) memory locations without any loss of information. Memory efficient
storage of symmetric matrices is the topic of Exercise 7.21.

The C++ code below implements the banded Cholesky algorithm for a given matrix with
s specified bandwidth. The companion methods bandBack and bandFor for backward and
forward of banded systems are given in Appendix D.

```
Vector Matrix::bandChol(const Vector& RHS, Matrix& G,
    int bwidth) const {
    double temp = 0;
    int low, up;

    for(int j = 0; j < nCols; j++){
        if(pa[j][j] == 0){
            cout << "Singular system!" << endl;
            exit(1);
        }
        temp = pa[j][j];
    }
    low = std::max(0, j - bwidth);

    for(int k = low; k < j; k++)
        temp -= G[j][k]*G[j][k];

    G.pa[j][j] = sqrt(temp);

    up = std::min(j + bwidth, nRows);

    for(int i = j + 1; i <= up; i++){
        temp = pa[i][i];
        for(int k = low; k < j; k++)
            temp -= G[j][k]*G[i][k];
        G.pa[i][j] = temp/G[j][j];
    }
    Vector h = G.bandFor(RHS, bwidth);
    Vector b = G.trans().bandBack(h, bwidth);
    return b;
}
```

In contrast to the banded Cholesky method from the previous section, our banded
Cholesky explicitly returns the Cholesky factor to the user in a Matrix object that
p passed in (by reference) from the calling program. The reason for this stems from an
application for this method that will run in the next section.

The bandChol method uses min and max functions that become available by
in the algorithm header. Thus, we need to add

```
#include <algorithm>
```

to the beginning of the file that contains the method definitions for class Matrix.
The R package Sparse provides access to tools for computing with sparse matrices.
The routines in this work on matrices that are stored in a compressed sparse row
(csr) format that efficiently adapts to the structure of the matrix. matrix.csr class has
been created to efficiently store sparse matrix objects with method functions for t, %*,
backsolve, chol and solve that apply to objects of this class. The library can be installed
from the CRAN website

+   > install.packages("SparseM")