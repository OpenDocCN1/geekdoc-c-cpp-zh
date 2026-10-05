# Sec. 14.1 Summation Techniques

which in turn yield $c_1=1/2$ and $c_2=1/2$. Thus, if the closed-form solution for the summation is a polynomial, it is indeed correct, as the solution is a simple only be

$1/2n^2 + 1/2n + 0$

which is more commonly written

$\frac{n(n+1)}{2}$

At this point, we must still do the "test" part of the guess-and-test approach. We can use an induction proof to verify whether our candidate closed-form solution is correct. In this case it is indeed correct, as shown by Example 2.11. The induction proof is necessary because our initial assumption that the polynomial could be wrong. For example, it might have been that the true solution includes a logarithmic term, such as $cn^2+c2 \log n$. The process shown here is essentially fitting a curve to a fixed number of points. Because there is always an $n$-degree polynomial that fits $n+1$ points, we do not have enough to be sure that we know the true equation without the induction proof.

Guess-and-guess is useful when the solution for $\sum_{i=1}^n i^2$, or more generally $\sum_{i=1}^nc$ for any positive integer. Why is this not a universal approach to solving summations? Because many summations do not have a polynomial as their closed form.

A more general approach is based on the subtract-and-guess and divide-and-guess strategies. One of such subtract-and-guess is known as the shifting method. The shifting method subtracts the summation from a variation on the summation. The variation selected for the subtraction should be one that makes most of the terms cancel out. Thus so we pick a known function $g$ and find a pattern in $f(n)-g(n)$ or $f(n)/g(n)$.

**Example 14.1** Find the closed form solution for $\sum_{i=1}^{n-1} i^2$ using the divide-and-guess approach. We will try two example functions to illustrate the divide-and-guess method: dividing by $n$ and dividing by $f(n-1)$. Our goal is to find patterns that we can use to guess a closed-form expression as our candidate for testing with an induction proof. If we do in finding such patterns, we construct a table showing the first few numbers of each, and the result of dividing one by the other, as follows:

| | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |
|---|---|---|---|---|---|---|---|---|---|---||
| $f(n)$ | 1 | 3 | 6 | 10 | 15 | 21 | 28 | 36 | 46 | 57 |
| $n$ | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |
| $f(n)/n$ | 2/2 | 3/2 | 4/2 | 5/2 | 6/2 | 7/2 | 8/2 | 9/2 | 10/2 | 11/2 |
| $f(n)/f(n-1)$ | | 0 | 1 | 3 | 6 | 10 | 15 | 21 | 28 | 36 | 46 |
| $f(n)/f(n-1)$ | | | 3/1 | 4/2 | 5/3 | 6/4 | 7/5 | 8/6 | 9/7 | 10/8 | 11/9 |