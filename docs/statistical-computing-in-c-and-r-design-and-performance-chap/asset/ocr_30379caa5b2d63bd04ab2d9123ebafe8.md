# 260 NUMERICAL LINEAR ALGEBRA

summarized $\in Algorithm 7.3 below. The algorithm depends on user-specified values of the tuning parameters $\delta$ and $itMax$ that represent the desired level of approximation and maximum number of iterations, as well as a starting vector $v$ with $v^T v_1 
eq 0$.

# Algorithm 7.3 Power method

```
$v^{(0)} = Av/\|Av\|; \lambda^{(0)} = (v^{(0)})^T Av^{(0)}, niter = 0, change = \infty$
while change > \delta and niter < itMax do
niter := niter + 1
v^{(n)} := Av^{(n-1)}/\|Av^{(n-1)}\|;
\lambda^{(n)} := (v^{(n)})^T Av^{(n)}\nchange := := |\lambda^{(n)} - \lambda^{(n-1)}|;
end
return $v^{(n)}, \lambda^{(n)}$
```

Algorithm 7.3 successfully applies $A$ to the vector $v$, renormalizes and evaluates the ratio of quadratic forms in $A$ that provides the changes in $\lambda_i$ from successive iterations. If the magnitude of change falls below the specified tolerance $\delta$, execution is terminated. The value of change is initialized at $\infty$ so that the *while* loop will begin.

To illustrate how Algorithm 7.3 works we use the positive-definite matrix $A$ that was used for demonstrating the Gauss transform in Section 2 and choose $v$ as the vector

$v$

[1.6866933 0.8378770 0.1537331 -1.138169 1.253814] as that the right-side example. The condition that is needed for $v$ that it has a nonzero inner product with the first eigenvector of $A$. Random selection seems a good strategy to produce $v$ with this property.

The eigenvalues and eigenvectors

| [1] | [2] | [3] | [4] | [5] |
| --- | --- | --- | --- | --- |
| [1,] | 2.8183730 | -3.1452537 | -0.2082637 | -4.9131724 | -1.0287284 |
| [2,] | -3.1452537 | 5.4246530 | 1.9229179 | 5.5110075 | 0.1453005 |
| [3,] | -0.2082637 | 1.9229179 | 2.1096700 | 1.9187222 | -1.5299840 |
| [4,] | -4.9131724 | 5.5110075 | 1.9187222 | 8.0239285 | -0.2145681 |
| [5,] | -1.0287284 | 0.1453005 | -1.5299840 | -0.2145681 | 3.1624022 |

can be obtained using the R function. The results from eigen are returned as a list with the *values* and vectors containing the eigenvalues and eigenvectors, respectively. For the current matrix of interest this gives

# **eigen($A$)**

$values$

[1] 15.199405175 0.47788146 1.34465045 0.41326152 0.003868751

# $vectors$

| [1,] | [2,] | [3,] | [4,] | [5,] |
| --- | --- | --- | --- | --- |
| [1,] | 0.385560633 | -0.32572975 | 0.1754596 | 0.2667121 | 0.80222575 |
| [2,] | -0.56072105 | -0.0243260 | 0.6461808 | -0.4438871 | 0.26551988 |
| [3,] | -0.19942614 | -0.5061978 | 0.0403680 | 0.6156238 | -0.4058819 |
| [4,] | -0.70715782 | -0.02592954 | -0.5284342 | 0.3267940 | 0.33647946 |
| [5,] | -0.004488373 | 0.79774734 | 0.3305018 | 0.4964037 | 0.08905776 |

With this basis for a comparison, let us see how the method performs in terms of computing $\lambda_1 = 15.199405175$ and its associated eigenvector.