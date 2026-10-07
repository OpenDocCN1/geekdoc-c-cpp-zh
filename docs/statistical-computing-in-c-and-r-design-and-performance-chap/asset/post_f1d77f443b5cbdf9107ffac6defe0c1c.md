
## COMPUTING A SAMPLE VARIANCE

A direct application of the definitional formula would suggest a two-pass algorithm where $\bar{x}$ is obtained first and then used to calculate the RSS. The pseudo-code description of the recursive process is given below.

```
Algorithm 2.1 Two-pass algorithm for the standard deviation
$\bar{x} = 0$
for $j = 1$ to $n$ do
  $\bar{x} := \bar{x} + x_j$
end for
$\bar{x} := \bar{x}/n$
RSS = 0
for $j = 1$ to $n$ do
  RSS := RSS + (x_j - \bar{x})^2$
end for
return $\sqrt{\frac{RSS}{n-1}} \bar{x}$
```

As an alternative to the two-pass formula, it is standard pedagogical practice to describe the use of a “computational” formula for RSS that stems from the identity

> $RSS = \sum_{j=1}^n x_j^2 - n^{-1} \left(\sum_{j=1}^n x_j\right)^2$

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

If $S$ is small relative to $|\bar{x}|$, $\kappa$ is approximately $\bar{x}/S$. This quantity is recognized as the inverse of the coefficient of variation that provides a scale-free measure of data variation. This can be indicative of instances where the “computational formula” may be problematic. The cases we visit where data are all (relatively) close to their mean value with the consequence that $\sum_{j=1}^n x_j^2$ and $n^{-1} (\sum_{j=1}^n x_j)^2$ may be sufficiently close to create cancellation problems.

Suppose that the original data $x_1, \dots, x_n$ are replaced by $x_1(1+E_1), \dots, x_n(1+E_n)$ might occur on a computer through the use of floating-point approximations. Then, Chan and Lewis (1979) establish that the standard deviation $S$ computed (without round-off error) from the altered data will satisfy $\hat{S} = S(1+\delta)$

```
$|delta| \le \gamma^2 + O(n\gamma^4) \quad (2.17)$
```

for

```
$\gamma = \max_{1 \le j \le n} |E_j|$
```

For small $\gamma$ the lead term in the bound on $|delta|$ is linear in $\kappa$ which indicates an increase in the round-off error in the data will be by a proportional increase (in the bound for relative absolute error for computing $S$ with condition number representing the proportionality factor). We can view $\kappa$ as a measure of the inherent sensitivity of $S$ for particular data set with the effect of floating-point approximation error.

The analysis that led to (2.17) was in the ideal setting where the computation of $\hat{S}$ can be carried out without error. Or, the ideal case does not hold in practice and additional errors will be introduced whatever algorithm is used to compute an approximation to $S$. To measure this let $\hat{S}_e$ be the approximation to $S$ that is obtained by a computational algorithm to $x_1(1+E_1), ..., x_n(1+E_n)$. We define the relative absolute error to be

```
RAE = $|\hat{S} - S|/S. \quad (2.18)$
```

RAE = $2\kappa\gamma(\frac{n}{2}+1)\gamma$ for the two-pass algorithm. A similar bound for the "computational" formula is

```
RAE $\le \frac{3}{2}(n+1)\kappa^2$.
```

Figures 2.1-2 show the bounds (of the base 10 logarithm of) for the two-pass and "computational" formula, respectively. In doing this we $n=100, \gamma=2^{-24}$ (as would be expected for single precision round-off errors), those true mean for the data be and let the standard deviation range from $10^{-5}$ to 1. For simplicity $\kappa$ is represented here by $\sigma^{-1}$ and the horizontal axis is in of $-log_{10}\sigma$ in the figures.

## 28 REPRESENTATION OF NUMBERS

Figures 2.1-2 show the bounds (of the base 10 logarithm of) for the two-pass and "computational" formula, respectively. In doing this we $n=100, \gamma=2^{-24}$ (as would be expected for single precision round-off errors), those true mean for the data be and let the standard deviation range from $10^{-5}$ to 1. For simplicity $\kappa$ is represented here by $\sigma^{-1}$ and the horizontal axis is in of $-log_{10}\sigma$ in the figures.

The two-pass method is less sensitive to growth in $\kappa$ both it and the West algorithm appear to behave when $\kappa$ becomes large.

## 30 REPRESENTATION OF NUMBERS

The two-pass method is less sensitive to growth in $\kappa$ both it and the West algorithm appear to behave when $\kappa$ becomes large.

There are also updating algorithms that can be used to compute RSS. For example, an algorithm developed by West (1979) and others (see, e.g., Chan, et. 1983) takes the form

```
Algorithm 2.3 West algorithm for the standard deviation
$\bar{x} = x_1$
RSS = 0
for $j = 2$ to $n$ do
  RSS := RSS + \frac{1}{j-1}(x_j - \bar{x})^2$
  $\bar{x} := \bar{x} + (x_j - \bar{x})/j$
end for
return $\frac{RSS}{\sqrt{n-1}}, \bar{x}$
```

The Chan/Lewis upper bound for this is

> $RAE \le (\frac{n}{2} + 2)\gamma + (\frac{\sqrt{2}}{3}n + 7\sqrt{n} + 1)\kappa$.

Like the two-pass method, the error bound for West algorithm involves only $\kappa$ rather than $\kappa^2$. The analog of Figures 2.1–2.2 that applies to the West algorithm is in Figure 2.3. The empirical results in the figure were obtained using the same simulation methods that were employed to produce Figures 2.1–2.2.

## 2.7 Storage in R

To conclude this let us mention a few things about the data types and precision of computations in R. First, the “primitive” data types in R include character, double, integer and logical. The double and integer types are analogs of the types with the same names in C++ while logical corresponds to the C++ boolean data type. The character designation in R indicates a variable that holds strings rather than a single character as C++. The double type in R also goes by equal, and more frequently used, name of numeric. To access the storage mode of a given object, one uses either the mode or storage functions. Machine specific details concerning storage, etc., are held in the R list .Machine.
