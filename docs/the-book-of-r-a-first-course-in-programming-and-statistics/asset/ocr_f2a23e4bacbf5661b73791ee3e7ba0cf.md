```
R> A <- rbind(c(2,5,2),c(6,1,4))
R> A
  [1] [2] [3]
  [1,] 2 5 2
  [2,] 6 1 4
R> t(A)
  [1] [2]
  [1,] 2 6
  [2,] 5 1
  [3,] 2 4
```

If "transpose the transpose" of A, you'll recover the original matrix.

```
R> t(t(A))
  [1] [2] [3]
  [1,] 2 5 2
  [2,] 6 1 4
```

# 3.3.2 Identity Matrix

The identity matrix written as $I_m$ is a particular kind of matrix used in mathematics. It's a square $m 	imes m$ matrix with ones on the diagonal and zeros elsewhere.

Here's an example:

![](bbox=[0.503, 0.526, 0.638, 0.597])

You can create an identity matrix of any dimension using the standard matrix function, but there's a quicker approach using diag. Earlier, used diag on an existing matrix to extract or overwrite its diagonal elements. You can also use it as follows:

```
R> A <- diag(x=3)
R> A
  [1] [2] [3]
  [1,] 1 0 0
  [2,] 0 1 0
  [3,] 0 0 1
```

You can see diag can be used to easily produce an identity matrix. To clarify, the behavior of diag depends on what you supply to its argument x. If, as earlier, x is a matrix, diag will retrieve the diagonal elements of the matrix. If $x$ is a single positive integer, as is the case here, then diag will produce the identity matrix of the corresponding dimension. You can find more uses of diag on its help page.