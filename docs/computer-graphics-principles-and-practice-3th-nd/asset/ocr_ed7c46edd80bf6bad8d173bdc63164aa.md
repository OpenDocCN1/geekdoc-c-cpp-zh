# Listing 30.5: Estimating the integral of the real-valued function $f$ on an interval, version 2.

```
```c
def integrate2(double *f (double), double a, double b):
    // estimate the integral of f on [a, b]
    x1 = uniform(a, b)   // random real number in [a, b]
    x2 = uniform(a, b)   // second random real number in [a, b]
    y = 0.5 * ((*f) (x1) + (*f) (x2)) // average the results
    return y * (b - a)    // multiply by length of interval
```
```

It seems intuitively obvious that the expected value here is still the integral of $f$ on $[a, b]$. Let's verify that. In mathematical terms, we have two random variables, $X_1$ and $X_2$, each with a uniform distribution on $[a, b]$. We then compute $Y = \frac{1}{2}(f(X_1)+f(X_2))$. What is $\mathbf{E}[(b-a)Y]$? Using the linearity of expectation, we see that

\[
\begin{aligned}
\mathbf{E}[(b-a)Y] &= \mathbf{E}\left[(b-a)\frac{1}{2}(f(X_1)+f(X_2))\right] &\qquad (30.52)\\
&= \frac{1}{2}\mathbf{E}[(b-a)(f(X_1)+f(X_2))] &\qquad (30.53)\\
&= \frac{1}{2}\left(\mathbf{E}[(b-a)f(X_1)] + \mathbf{E}[(b-a)f(X_2)]\right) &\qquad (30.54)\\
&= \frac{1}{2}\left(2\mathbf{E}[(b-a)f(X_1)]\right) &\qquad (30.55)
\end{aligned}
\]

The last equality follows because $X_1$ and $X_2$ have the same distribution. Thus it follows that

\[
\begin{aligned}
\mathbf{E}[(b-a)Y] &= \mathbf{E}[(b-a)f(X_1)] &\qquad (30.56)\\
&= \int_a^b f(x)\,dx. &\qquad (30.57)
\end{aligned}
\]

What about the variance?

\[
\begin{aligned}
\mathbf{Var}[Y] &= \mathbf{Var}\left[\frac{1}{2}(f(X_1)+f(X_2))\right] &\qquad (30.58)\\
&= \frac{1}{4}\mathbf{Var}[f(X_1)+f(X_2)] &\qquad (30.59)\\
&= \frac{1}{4}\left(\mathbf{Var}[f(X_1)] + \mathbf{Var}[f(X_2)]\right) &\qquad (30.60)\\
&= \frac{1}{4}\left(2\mathbf{Var}[f(X_1)]\right) &\qquad (30.61)\\
&= \frac{1}{2}\mathbf{Var}[f(X_1)]. &\qquad (30.62)
\end{aligned}
\]

When we averaged two samples, the expectation remained the same, but the variance went down by a factor of two. (The standard deviation went down by a factor of $\sqrt{2}$). If we define $Y_n$ by

\[
Y_n = \frac{1}{n}\sum_{i=1}^n f(X_i), \qquad (30.63)
\]