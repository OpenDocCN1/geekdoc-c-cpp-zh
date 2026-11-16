Shortly we will list six equivalent forms of the MacWilliams equations, with (7.3) denoted $(M_1)$. This form, as well as the next, denoted $(M_2)$, involves only the weight distributions and binomial coefficients. Both $(M_1)$ and $(M_2)$ consist of a set of $n+1$ equations. The third form, denoted $(M_3)$, is a single identity involving the weight enumerators of a code and its dual. Although we originally called $(M_4)$ the MacWilliams equations, in fact, any of these three forms is generally referred to as the MacWilliams equations. The fourth form is the actual solution of the MacWilliams equations for the weight distribution of the dual code in terms of the weight distribution of the original code; by Corollary 7.1.4 this solution is unique. In order to give the solution in compact form, we recall the definition of the Krawtchouk polynomial

```
$K_k^{r,q}(x) = \sum_{j=0}^k (-1)^j(q-1)^{k-j}\binom{x}{j}\binom{n-x}{k-j} \quad \text{for } 0 \le k \le n$
```

of degree $k$ in $x$ given in Chapter 2. The $n+1$ equations that arise will be denoted $(K)$. The final two sets of equations equivalent to (7.3), which are sometimes more convenient for calculations, involve the *Stirling numbers* $S(r, v)$ *of the second kind*. These are defined for nonnegative integers $r, v$ by the equation

```
$S(r, v) = \frac{1}{v!} \sum_{i=0}^v (-1)^{v-i} \binom{v}{i} i^r;$
```

in addition, they satisfy the recursion

```
$S(r, v) = vS(r-1, v) + S(r-1, v-1) \quad \text{for } 1 \le v < r.$
```

The number $v!S(r, v)$ equals the number of ways to distribute $r$ distinct objects into $v$ distinct boxes with no box left empty; in particular,

```
$S(r, v) = 0 \quad \text{if } r < v$
```

and

```
$S(r, r) = 1$
```

The following is a basic identity for the Stirling numbers of the second kind (see [204]):

```
$j^r = \sum_{v=0}^r v! \binom{j}{v} S(r, v).$
```

The two forms of the equations arising here involve the weight distributions, binomial coefficients, and the Stirling numbers. They will be called the *Pless power moments* and denoted $(P_1)$ and $(P_2)$; they are due to Pless [258]. Each of $(P_1)$ and $(P_2)$ is an infinite set of equations.

# Exercise 376 Compute a table of Stirling numbers $S(r, v)$ of the second kind for $1 \le v \le r \le 6$.

We now state the six families of equations relating the weight distribution of an $[n, k]$ code $C$ over $\mathbb{F}_q$ to the weight distribution of its dual $C^\perp$. The theorem that follows asserts