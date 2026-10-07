# 490 AN INTRODUCTION TO R

1]> evaluates TRUE for the first column with the consequence that the first row is selected. Selection of 2 for the column indexのである returns the (1, 2) matrix element. A discussion of R subscribing is provided by Spector (2008).

+ - operators applied to matrices give matrix addition and subtraction the matrices involved have the same row and column dimensions. Matrix transposition is accomplished with the t function while matrix multiplication is obtained through the operator %*. To illustrate the idea we create two matrix objects using

```
> set.seed(123)
A <- matrix(runif(15), 3, 5)
B <- matrix(runif(15), 3, 5)
```

| | [1] | [2] | [3] | [4] | [5] |
|---|---|---|---|---|--|
| A | [1] | 0.2857375 | 0.8831074 | 0.5281055 | 0.4566147 | 0.677706 |
| | [2] | 0.2783051 | 0.9406473 | 0.8924190 | 0.9568333 | 0.5726334 |
| | [3] | 0.4089679 | 0.0455565 | 0.5513450 | 0.4533342 | 0.1029243 |
| B | [1] | 0.8988247 | 0.3279207 | 0.6928034 | 0.6557058 | 0.5941420 |
| | [2] | 0.2468077 | 0.9845036 | 0.6405068 | 0.7085305 | 0.2891957 |
| | [3] | 0.0420593 | 0.8859353 | 0.9924268 | 0.5440660 | 0.1471136 |

The R random number generator runif was used to create two 3 x 5 matrices A and B. At the outset the seed for the random number generator ensures that our calculations can be replicated from incarn of R function provided the same seed and default random number generator (i.e., Incarn of Mersenne twister). Now R is used to evaluate a matrix expression as

```
> (cos(A) + B)*%t(B^2) - 2*A
| | [1] | [2] | [3] |
|---|---|---|--|
| [1] | 2.8319103 | -4.4961831 | 3.643643 |
| [2] | 0.1706415 | -2.247529 | 4.930415 |
| [3] | -0.0323345 | -2.361368 | 6.782212 |
```

When applied to an array max and min functions will return the largest and smallest element. In the case of our matrices this produces

```
> max(A); max(B)
[1] 0.9568333
[1] 0.9942698
> min(A); min(B)
[1] 0.0455565
[1] 0.0420593
```

Note the use of semicolon to allow more than one element to be entered from a single prompt.
Both the seq and c functions can be used to specify array or column indices. As demonstrated above with the > operator, logical operators can also be used in this capacity.
R logical operators include

+   ! for not,
< and >= for logical binary less than, enc,
== for logical binary equal,
& for logical binary AND
| for logical binary OR.