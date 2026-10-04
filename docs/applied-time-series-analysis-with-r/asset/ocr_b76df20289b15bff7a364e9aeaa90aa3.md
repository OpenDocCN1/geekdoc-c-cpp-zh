# Long-Memory Processes

where

```
$(\alpha)_n = \frac{\Gamma(\alpha + n)}{\Gamma(\alpha)}$
```

and where $[x]$ denotes the greatest integer less than or equal to $x$. Although these polynomials can be defined as in Equation 11.9, it is also useful to define them through their generating function (see Rainville, 1960 and Magnus, Oberhettinger, and Soni, 1966).

# Theorem 11.3

Let $\lambda \neq 0$ and $|z| < 1$. Then for $|u| \leq 1$ the Gegenbauer polynomials, $C_u^{(\lambda)}(u)$, satisfy

```
$(1 - 2uz + z^2)^{-\lambda} = \sum_{j=0}^{\infty} C_j^{(\lambda)}(u)z^j. (11.10)
```

Proof. See Rainville (1960) and Magnus et al. (1966).

# 11.3.2 Gegenbauer Process

In Definition 11.3 follows we define the Gegenbauer process, which is an extension of the fractional process of Definition 11.3. See Gray et al. (1989, 1994).

# Definition 11.5

If $\sum_{k=0}^{\infty} |C_k^{(\lambda)}(u)| < \infty$ where $C_k^{(\lambda)}(u)$ is defined in Equation 11.9, then the general linear process defined by

```
$X_t - \mu = (1 - 2uB + B^2)^{-\lambda} a_t$
```

```
$= \sum_{j=0}^{\infty} C_j^{(\lambda)}(u)a_{t-j}, (11.11)
```

where $a_t$ is white noise, called a Gegenbauer process. If $X_t$ is invertible, the Gegenbauer process is written

```
$(1 - 2uB + B^2)^{\lambda}(X_t - \mu) = a_t. (11.12)
```