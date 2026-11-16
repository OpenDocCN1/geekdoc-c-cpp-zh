may have other zeros that are points at infinity in $\mathbb{P}^n(\mathbb{F})$. Furthermore, part (iii) indicates that the concept of a point in $\mathbb{P}^n(\mathbb{F})$ being a zero of a homogeneous polynomial is well-defined.

**Exercise 765** Give the one-to-one correspondence between the homogeneous polynomials of degree 2 in two variables over $\mathbb{F}_2$ and the polynomials of degree 2 or less (the zero polynomial is not included) in one variable over $\mathbb{F}_2$ as indicated in the proof of Theorem 13.1.3.(iv).

# ## 13.2 Some classical codes

Before studying algebraic geometry codes it is helpful to examine some classical codes that will motivate the definition of algebraic geometry codes.

# ### 13.2.1 Generalized Reed–Solomon codes revisited

In Section 5.2 we first defined Reed–Solomon codes as special cases of BCH codes. Theorem 5.2.3 gave an alternative formulation of narrow-sense RS codes, which we now recall.

For $k \ge 0$, $\mathcal{P}_k$ denotes the set of polynomials of degree less than $k$, including the zero polynomial, in $\mathbb{F}_q[x]$. If $\alpha$ is a primitive $n$th root of unity in $\mathbb{F}_q$ where $n = q - 1$, then the code

```
$$\mathcal{C} = \{ (f(1), f(\alpha), f(\alpha^2), \dots, f(\alpha^{n-2})) \mid f \in \mathcal{P}_k \}$$
```

is the narrow-sense $[n, k, n-k+1]$ RS code over $\mathbb{F}_q$. From Section 5.3, we saw that $\mathcal{C}$ could be extended to an $[n+1, k, n-k+2]$ code given by

```
$$\widehat{\mathcal{C}} = \{ (f(1), f(\alpha), f(\alpha^2), \dots, f(\alpha^{n-2}), f(0)) \mid f \in \mathcal{P}_k \}$$
```

We now recall the definition of the generalized Reed–Solomon (GRS) codes. Let $n$ be any integer with $1 \le n \le q$, $\boldsymbol{\gamma} = (\gamma_0, \dots, \gamma_{n-1})$ an $n$-tuple of distinct elements of $\mathbb{F}_q$, and $\mathbf{v} = (v_0, \dots, v_{n-1})$ an $n$-tuple of nonzero elements of $\mathbb{F}_q$. Let $k$ be an integer with $1 \le k \le n$. Then the codes

```
$$\text{GRS}_k(\boldsymbol{\gamma}, \mathbf{v}) = \{ (v_0 f(\gamma_0), v_1 f(\gamma_1), \dots, v_{n-1} f(\gamma_{n-1})) \mid f \in \mathcal{P}_k \}$$
```

are the GRS codes. The narrow-sense RS code $\mathcal{C}$ is the GRS code with $n = q - 1$, $\gamma_i = \alpha^i$, and $v_i = 1$; the extended code $\widehat{\mathcal{C}}$ is the GRS code with $n = q$, $\gamma_i = \alpha^i$ for $0 \le i \le q - 2$, $\gamma_{q-1} = 0$, and $v_i = 1$. By Theorem 13.1.3.(iv), there is a one-to-one correspondence between the homogeneous polynomials of degree $k-1$ in two variables over $\mathbb{F}_q$ and the nonzero polynomials of $\mathcal{P}_k$. We denote the homogeneous polynomials of degree $k-1$ in two variables over $\mathbb{F}_q$ together with the zero polynomial by $\mathcal{L}_{k-1}$. If $f(x_1) \in \mathcal{P}_k$ with $f$ nonzero of degree $d \le k-1$, then $g(x_1, x_2) = x_2^{k-1-d} f(x_1/x_2) \in \mathcal{L}_{k-1}$ and $g(x_1, 1) = f^{h}(x_1, 1) = f(x_1)$ by (13.1). Therefore we can redefine the GRS codes as follows using homogeneous polynomials and projective points. Let $P_i = (\gamma_i, 1)$, which is a representative of the projective point $(\gamma_i : 1) \in \mathbb{P}^1(\mathbb{F}_q)$. Then

```
$$\text{GRS}_k(\boldsymbol{\gamma}, \mathbf{v}) = \{ (v_0 g(P_0), v_1 g(P_1), \dots, v_{n-1} g(P_{n-1})) \mid g \in \mathcal{L}_{k-1} \} \quad (13.2)$$
```