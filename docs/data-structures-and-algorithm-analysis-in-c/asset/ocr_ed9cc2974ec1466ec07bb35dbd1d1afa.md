Another type of common series in analysis is the arithmetic series. Any such series can be evaluated from the basic formula:

```
\sum_{i=1}^N i = \frac{N(N+1)}{2} \approx \frac{N^2}{2}
```

For instance, to find the sum $2 + 5 + 8 + \dots + (3k - 1)$, rewrite it as $3(1 + 2 + 3 + \dots + k) - (1 + 1 + 1 + \dots + 1)$, which is clearly $3k(k+1)/2 - k$. Another way to remember this is to add the first and last terms (total $3k + 1$), the second and next-to-last terms (total $3k + 1$), and so on. Since there are $k/2$ of these pairs, the total sum is $k(3k + 1)/2$, which is the same answer as before.

The next two formulas pop up now and then but are fairly uncommon.

```
\sum_{i=1}^N i^2 = \frac{N(N+1)(2N+1)}{6} \approx \frac{N^3}{3}
```

```
\sum_{i=1}^N i^k \approx \frac{N^{k+1}}{k+1} \quad k \neq -1
```

When $k = -1$, the latter formula is not valid. We then need the following formula, which is used far more in computer science than in other mathematical disciplines. The numbers $H_N$ are known as the harmonic numbers, and the sum is known as a harmonic sum. The error in the following approximation tends to $\gamma \approx 0.57721566$, which is known as Euler's constant.

```
H_N = \sum_{i=1}^N \frac{1}{i} \approx \log_e N
```

These two formulas are just general algebraic manipulations:

```
\sum_{i=1}^N f(i) = N f(N)
\sum_{i=n_0}^N f(i) = \sum_{i=1}^N f(i) - \sum_{i=1}^{n_0-1} f(i)
```

# 1.2.4 Modular Arithmetic

We say that $A$ is congruent to $B$ modulo $N$, written $A \equiv B \pmod N$, if $N$ divides $A - B$. Intuitively, this means that the remainder is the same when either $A$ or $B$ is divided by $N$. Thus, $81 \equiv 61 \equiv 1 \pmod{10}$. As with equality, if $A \equiv B \pmod N$, then $A + C \equiv B + C \pmod N$ and $AD \equiv BD \pmod N$.