# 28 REPRESENTATION OF NUMBERS

might occur on a computer through the use of floating-point approximations. Then, Chan
and Lewis (1979) establish that the standard deviation $S$ computed (without round-off
error) from the altered data will satisfy $\hat{S} = S(1+\delta)$

```
$|delta| \le \gamma^2 + O(n\gamma^4)$ \quad (2.17)$
```

for

```
$\gamma = \max_{1 \le j \le n} |E_j|$
```

For small $\gamma$ the lead term in the bound on $|delta|$ is linear in $\kappa$ which indicates an increase
in the round-off error in the data will be by a proportional increase (in the bound for
t relative absolute error for computing $S$ with condition number representing the
proportionality factor. We can view $\kappa$ as a measure of the inherent sensitivity of $S$ for
particular data set with the effect of floating-point approximation error.

The analysis that led to (2.17) was in the ideal setting where the computation of $\hat{S}$
can be carried out without error. Or, the ideal case does not hold in practice and
additional errors will be introduced whatever algorithm is used to compute an
approximation to $S$. To measure this let $\hat{S}_e$ be the approximation to $S$ that is obtained
 a computational algorithm to $x_1(1+E_1), ..., x_n(1+E_n)$. We define the
relative absolute error to be

```
RAE = $|\hat{S} - S|/S$. \quad (2.18)$
```

RAE = $2\kappa\gamma(\frac{n}{2}+1)\gamma$
for the two-pass algorithm. A similar bound for the "computational" formula is

```
RAE $\le \frac{3}{2}(n+1)\kappa^2$.
```

Figures 2.1-2 show the bounds (of the base 10 logarithm of) for the two-pass and
"computational" formula, respectively. In doing this we $n=100, \gamma=2^{-24}$ (as would
be expected for single precision round-off errors), those true mean for the data be
and let the standard deviation range from $10^{-5}$ to 1. For simplicity $\kappa$ is
represented here by $\sigma^{-1}$ and the horizontal axis is in of $-log_{10}\sigma$ in the figures.
The suggestion from Figure 2.1-2 shows that the "computational" formula is well
urate for data sets with small coefficients of variation or large values of $\kappa$. In fact, the
difference between the bounds for the "computational" and two-pass algorithms is $\kappa^2$.

```
$\frac{1}{2}\gamma^2[\kappa^2-1]+\kappa[(n+1)\kappa-2]$.
```

is not because $\kappa \ge 1$. Of course, the fact that only upper bounds are
involved means that comparisons of this nature are not conclusive.
A empirical study was conducted to investigate the relevance of the
bounds for using the two computational algorithms. Data were generated from
normal distributions with means of one and standard deviations $\sigma$ for which $log_{10}(\sigma)=
$(j-1)/2, j=0,...,10$. To accomplish this Wichmann-Hall algorithm from Section 4.5
was to generate uniform random variables that were transformed using
the Box-Muller transformation in Section 4.7. For each value of $\kappa=1/\sigma$,
10 replicate samples of size $n=100$ were generated and their standard deviations were