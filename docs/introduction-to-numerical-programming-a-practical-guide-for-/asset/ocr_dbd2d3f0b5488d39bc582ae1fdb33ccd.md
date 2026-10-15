# ## 8.6 Problems

The Python and C/C++ programs for the following problems may import the functions developed in this chapter from the modules `eisgys.py` and, respectively, `eisgys.h`, which are available as supplementary material. In addition, the utility routines contained in files `matutil.py` and `matutil.h` can be used to perform basic operations with one- and two-dimensional arrays. For creating runtime plots, the graphical routines contained in the libraries `graphlib.py` and `graphlib.h` may be employed.

# ### PROBLEM 8.1

Use the function Jacobi to prove for a random invertible symmetric matrix A of order n = 100 the general property that the eigenvalues of the inverse A⁻¹ are the inverses 1/λᵢ of the eigenvalues λᵢ of the original matrix, while the eigenvectors coincide.

Invert the matrix A using the routine MatInv from the module `linsys.py` (respectively, `linsys.h`), and, employing the function EigSort, sort the eigenvectors of A and A⁻¹ by the corresponding eigenvalues before comparing them.

# ### Solution

The Python and C/C++ implementations are given in Listings 8.6 and 8.7.

```
```python
# Eigenvalues and eigenvectors of inverse of symmetric matrix
from random import *
from linsys import *
from eigsys import *
from matutil import *

n = 100                                      # order of matrix
a  = [[0]*(n+1) for i in range(n+1)]        # coefficient matrix
a1 = [[0]*(n+1) for i in range(n+1)]        # inverse of a
x  = [[0]*(n+1) for i in range(n+1)]        # eigenvectors of a
x1 = [[0]*(n+1) for i in range(n+1)]        # eigenvectors of a1
d  = [[0]*(n+1); d1 = [0]*(n+1)             # eigenvalues of a and a1

seed()                                       # initialize random number generator
for i in range(1,n+1):                       # generate random coefficient matrix
    for j in range(1,i+1):
        a[i][j] = a[j][i] = random()
        a1[i][j] = a1[j][i] = a[i][j]       # copy a in a1

Jacobi(a,x,d,n)                              # solve eigenvalue problem for a
EigSort(x,d,n,1)                             # sort eigenvalues and eigenvectors

MatInv(a1,n)                                 # a1 = a^(-1)
```
```