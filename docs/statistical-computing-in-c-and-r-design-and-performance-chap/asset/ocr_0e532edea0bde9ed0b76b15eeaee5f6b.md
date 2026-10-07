# R AS A CALCULATOR

The rbind cbind functions are particularly useful for working with arrays. These functions combine the rows or columns, respectively, of the arrays that are provided as their arguments. This is how we accomplish manipulations such as

```
> cbind(A[,1], B[,1], A[,c(2, 4)])
  [,1]         [2]         [4]
[1,] 0.2875755 0.89982497 0.8830174 0.4566147
[2,] 0.7883051 0.2460873 0.9404673 0.9568333
[3,] 0.4089769 - rbind(A[1:], B[,3])
> 0.0420593 0.0455565 0.4533342
```

```
> C
  [,1]        [2]        [3]        [4]        [5]
[1,] 0.2875755 0.8830174 0.5281055 0.4566147 0.6775706
[2,] 0.7883051 0.9404673 0.8294190 0.9568333 0.5726334
[3,] 0.0420593 0.8859539 0.9942698 0.5440660 0.1471136
```

Like any good scientific, R has a sum for adding up a group of numbers. But, it is more powerful than its hand-held relative that it can carry out calculations like

```
> sum(seq(-pi, pi, by = .5))
[1] -1.840704
> sum(A)
[1] 8.545771
```

When used in the apply function sum can produce marginal row or column sums for an array. In general the apply function has the form

```
apply(X, MARGIN, FUN)
```

where X is an array, FUN is the function to be applied to the rows or the columns of the array. Using this idea with our previous matrices produces results like

```
> apply(A, 1, sum)
[1] 2.832886 4.150658 1.562227
> apply(B, 2, sum)
[1] 1.187972 2.217194 2.327580 1.908302 1.030415
```

There is nothing special about sum in this example that other choices for the FUN argument not work equally well. For example,

```
> apply(A, 1, min)
[1] 0.2875775 0.5726334 0.0455565
> apply(B, 2, max)
[1] 0.8989250 0.9545036 0.9942698 0.7085305 0.5941420
```

Other calculator-like features of R are the choose factorial functions that calculate the binomial coefficients and factorials. The choose function has two arguments for the number of trials and number of successes in a binomial experiment where factorial takes one integer argument. An illustration of a typical calculation is

```
> choose(10,3); factorial(5)
[1] 120
[1] 120
```

Finally, R includes functions that compute the values of probability density/mass functions, cumulative probabilities, quantiles and random numbers for a rich collection of probability distributions. These functions all have names of the form dDist, pDist, qDist and