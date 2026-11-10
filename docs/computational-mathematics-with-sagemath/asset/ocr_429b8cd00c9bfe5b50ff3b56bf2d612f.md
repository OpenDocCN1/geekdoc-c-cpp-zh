# # A

# Answers to Exercises

# ## A.1 First Steps

**Exercise 1 page 14.** The command `R.var('u')` creates the symbolic variable $u$ and assigns it to the computer variable `u`. The computer variable `u` receives twice in a row its current value plus one, that is $u+1$, then $u+2$ (where $u$ remains the symbolic variable).

# ## A.2 Analysis and Algebra

**Exercise 2 page 28.** (*Computing a sum by recurrence*)

```
~~~sage
sage: n = var('n'); pmax = 4; s = [n + 1]
sage: for p in [1..pmax]:
....:     s += [factor((n+1)^(p+1) - sum(binomial(p+1, j) * s[j]
....:         for j in [0..p-1])) / (p+1)]
sage: s
~~~
```

Thus we obtain:

$$\sum_{k=0}^n k = \frac{1}{2}(n+1)n, \qquad \sum_{k=0}^n k^2 = \frac{1}{6}(n+1)(2n+1)n,$$
$$\sum_{k=0}^n k^3 = \frac{1}{4}(n+1)^2 n^2, \qquad \sum_{k=0}^n k^4 = \frac{1}{30}(n+1)(2n+1)(3n^2+3n-1)n.$$

**Exercise 3 page 31.** (*Computing a symbolic limit*) To answer this question, we use a symbolic function, and we compute its Taylor polynomial at 0 up to order 3: