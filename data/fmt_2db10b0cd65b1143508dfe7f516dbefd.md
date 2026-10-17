
\lim_{n\to\infty} r_n(x) = \frac{C_v(x)}{C_{v-1}(x)} = \frac{x/(2(v+1))}{1-\frac{x^2/(4(v+1)^2)}{\dots}} \quad (9.912a, b)

这对应于 (9.912a, 9.910b)，并且根据 [9.9.5–9.9.6] 的比较，当系数 (9.914a, b) 为实数且正数 (9.914c–d) 时，连分数 (9.911) ≡ (9.879b) 收敛的：

```
$$a_n(x) = \frac{2(v+n)}{x}, \quad b_n(x) = 1; \quad v > 0. \quad (9.914a–d)$$
```

这对于贝塞尔函数 (9.907b) (9.910a) 证明了 (9.911) ≡ (9.912b)

# Convergence of Special Fractions

If the remainder tends to zero (9.912a) as $n \to \infty$ the continued fraction (9.911) converges to (9.912b):

```
\lim_{n\to\infty} r_n(x) = \frac{C_v(x)}{C_{v-1}(x)} = \frac{x/(2(v+1))}{1-\frac{x^2/(4(v+1)^2)}{\dots}} \quad (9.912a, b)
```

It can be proved [9.9.5–9.9.6] that the continued fractions (9.909b) converge for real positive (all complex values). It has been shown that cylinder functions (9.898a–d) can be represented by the equivalent continued fractions (9.909b) that: (i) converge for complex values of the parameters; (ii) imply the limit (9.913):

```
\lim_{n\to\infty} \frac{C_{v+n+1}(x)}{C_{v+n}(x)} = 0, \quad (9.913)
```

that corresponds to (9.912a, 9.910b) and follows from the comparison [9.9.5–9.9.6] the convergence of the continued fraction (9.879b) ≡ (9.911) only if the coefficients (9.914a, b) are real and positive (9.914c–d):

```
$$a_n(x) = \frac{2(v+n)}{x}, \quad b_n(x) = 1; \quad v > 0. \quad (9.914a–d)$$
```

The convergence can be proved both for (9.911) ≡ (9.912b) [(9.872)=(9.874)] [(9.914a, b]] for all complex values of $x$ and parameters, using the following theorem [9.9.13–9.9.15] for continued fractions.

### 9.9.13 Special Limit Continued Fractions

The continued fraction (9.879a) represents a function of the variable $x$: (i) the coefficients $(a_n, b_n)$, and the numerators $p_n$ and denominators $q_n$ depend (9.915a) on $x$; (ii) for $x$ in the domain of the function they converge (9.915b):

```
$$a_0(x) + \frac{b_1(x)}{a_1(x)} + \frac{b_2(x)}{a_2(x)} + \dots + \frac{b_n(x)}{a_n(x) + \frac{p_n(x)}{q_n(x)}} = X_n(x), \lim_{n\to\infty} X_n(x) = X(x). \quad (9.915a, b)$$
```

# Singular Differential Equations and Special Functions

A continued fraction is limit periodic if the coefficients converge for large order (9.916a, b):

```
\lim_{n\to\infty} x_n(x) = a, \quad \lim_{n\to\infty} b_n(x) = b; \quad 0 \leq |a|, |b| \leq \infty, \quad (9.916a-d)
```

where the limit may be (9.916c) zero, finite, or infinity. The continued fraction for the logarithmic derivative of the hypergeometric function (9.872)=(9.874) [the cylinders (9.910a) ≡ (9.912b)] are limit periodic (9.880, c) [(9.914a, b)] with (9.916a, b) (9.917a):

```
\{a,b = \{1,\infty\}; \gamma = \{p_n,q_n\}; \quad 0 = \sigma^2 + a\sigma + b = (\sigma - \sigma_-)(\sigma - \sigma_+)\} \quad (9.917a-e)
```

the recurrence formulas (9.878a, b) for the numerators and denominators (9.917e) suggest the consideration of the quadratic polynomial (9.917d). The roots (9.917e)=(9.918a) of (9.917d) are in case (9.918b, c):

```
\sigma_{\pm} = \pm\frac{1}{2}\sqrt{a^2-4b}; \quad \sigma_- = -\sigma_+; \quad \lim_{n\to\infty}\frac{b_n(x)}{a_n(x)} = 0, \quad (9.916a-d)
```
