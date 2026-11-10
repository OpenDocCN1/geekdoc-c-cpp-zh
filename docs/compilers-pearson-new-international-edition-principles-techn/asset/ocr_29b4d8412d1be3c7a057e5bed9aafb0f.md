# 11.4.1  Affine Accesses

We say that an array access in a loop is *affine* if

+   1. The bounds of the loop are expressed as affine expressions of the surrounding loop variables and symbolic constants, and
+   2. The index for each dimension of the array is also an affine expression of surrounding loop variables and symbolic constants.

**Example 11.16:** Suppose *i* and *j* are loop index variables bounded by affine expressions. Some examples of affine array accesses are \(Z[i]\), \(Z[i+j+1]\), \(Z[0]\), \(Z[i,j]\), and \(Z[2*i+1,3*j-1]\). If *n* is a symbolic constant for a loop nest, then \(Z[3*n,n-j]\) is another example of an affine array access. However, \(Z[i*j]\) and \(Z[n*j+i]\) are not affine accesses.

Each affine array access can be described by two matrices and two vectors. The first matrix-vector pair is the **B** and **b** that describe the iteration space with the access, as in the inequality of Equation (11.1). The second pair, which we usually refer to as **F** and **f**, represent the function(s) of the loop-index variables that produce the array index(es) used in the various dimensions of the array access.

Formally, we represent an array access in a loop nest that uses a vector of index variables **i** by the four-tuple \(\mathcal{F}=\langle F,f,B,b\rangle\); it maps a vector **i** within the bounds

\[B\mathbf{i}+\mathbf{b}\ge 0\]

to the array element location

\[F\mathbf{i}+\mathbf{f}\]

**Example 11.17:** In Fig. 11.18 are some common array accesses, expressed in matrix notation. The two loop indices are *i* and *j*, and these form the vector **i**. Also, *X*, *Y*, and *Z* are arrays with 1, 2, and 3 dimensions, respectively.

The first access, \(X[i-1]\), is represented by a \(1\times2\) matrix **F** and a vector **f** of length 1. Notice that when we perform the matrix-vector multiplication and add in the vector **f**, we are left with a single function, \(i-1\), which is exactly the formula for the access to the one-dimensional array *X*. Also notice the third access, \(Y[j,j+1]\), which, after matrix-vector multiplication and addition, yields a pair of functions, \((j,j+1)\). These are the indexes of the two dimensions of the array access.

Finally, let us observe the fourth access \(Y[1,2]\). This access is a constant, and unsurprisingly the matrix **F** is all 0’s. Thus, the vector of loop indexes, **i**, does not appear in the access function.