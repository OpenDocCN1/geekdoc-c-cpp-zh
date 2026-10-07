# COMPUTING A SAMPLE VARIANCE

A direct application of the definitional formula would suggest a two-pass algorithm where $ar{x}$ is obtained first and then used to calculate the RSS. The pseudo-code description of the recursive process is given below.

```
Algorithm 2.1 Two-pass algorithm for the standard deviation
$ar{x} = 0$
for $j = 1$ to $n$ do
  $ar{x} := ar{x} + x_j$
end for
$ar{x} := ar{x}/n$
RSS = 0$
for $j = 1$ to $n$ do
  RSS := RSS + (x_j - ar{x})^2$
end for
return $\sqrt{\frac{RSS}{n-1}} \bar{x}$
```

As an alternative to the two-pass formula, it is standard pedagogical practice to describe the use of a “computational” formula for RSS that stems from the identity

> $RSS = \sum_{j=1}^n x_j^2 - n^{-1} \left(
sum_{j=1}^n x_j\right)^2$

The resulting computations then proceed along the lines of our next algorithm.

```
Algorithm 2.2 “Computational” algorithm for the standard deviation
$T = RSS = 0$
for $j = 1$ to $n$ do
  $T := T + x_j$
  RSS := RSS + x_j^2$
end for
RSS := RSS - T^2/n$
return $\sqrt{\frac{RSS}{n-1}}, \bar{x}$
```

This approach has the advantage of requiring only one pass through the data. The disadvantage is that $\sum_{i=1}^n x_i^2$ and $(\sum_{i=1}^n x_i)^2/n$ can agree across a number of significant digits. This produces inaccuracies when carrying the subtraction at the end of the for loop for reasons that were discussed in the previous section.

Chan and Lewis (1979) define the condition number associated with $S$ to be

> $\kappa = \sqrt{1 + n\bar{x}^2/S}$

If $S$ is small relative to $|ar{x}|$, $\kappa$ is approximately $ar{x}/S$. This quantity is recognized as the inverse of the coefficient of variation that provides a scale-free measure of data variation. This can be indicative of instances where the “computational formula” may be problematic. The cases we visit where data are all (relatively) close to their mean value with the consequence that $\sum_{j=1}^n x_j^2$ and $n^{-1} (\sum_{j=1}^n x_j)^2$ may be sufficiently close to create cancellation problems.

Suppose that the original data $x_1, \dots, x_n$ are replaced by $x_1(1+E_1), \dots, x_n(1+E_n)$ as