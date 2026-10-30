# Definition 4.2. Definiteness of a Matrix.

Let $H$ be $f$’s Hessian matrix. Then $H$ is

+   1. **positive definite** iff $H > 0$ for every nonzero vector $z \in \operatorname{domain}(f)$,
+   2. **positive semi-definite** iff $H \geq 0$ for every nonzero vector $z \in \operatorname{domain}(f)$,
+   3. **negative definite** iff $H < 0$ for every nonzero vector $z \in \operatorname{domain}(f)$,
+   4. **negative semi-definite** iff $H \leq 0$ for every nonzero vector $z \in \operatorname{domain}(f)$,
+   5. **indefinite** otherwise.

We can relate definiteness to the signs of the leading principal minors.

**Positive Definite:** All leading principal minors are positive.

**Positive Semi-definite:** All leading principal minors are non-negative (some may be zero).

**Negative Definite:** The leading principal minors follow the signs of $(-1)^k$, where $k$ is the order of the leading principal minor. Even order leading principal minors are positive, and odd order leading principal minors are negative.

**Negative Semi-definite:** All nonzero leading principal minors follow the signs of $(-1)^k$, where $k$ is the order of the leading principal minor. Even order nonzero leading principal minors are positive, and odd order nonzero leading principal minors are negative. Some may be zero.

**Indefinite:** Some leading principal minors do not follow any of the rules above.

If the Hessian is also a function of the independent variables, its definiteness might vary from one point to another. To test the definiteness of the Hessian at a point $x^*$, evaluate the Hessian at the point. For example, in the matrix

```
$$H(x_1,x_2)=\begin{bmatrix}2x_1 & x_2 \\ x_2 & 4\end{bmatrix},$$
```

the specific values of $x_1$ and $x_2$ determine whether $H$ is positive definite, positive semi-definite, negative definite, negative semi-definite, or indefinite at $[x_1,x_2]$. **Give an example of each case!**

*Table 4.2* summarizes the relationship between the Hessian matrix definiteness and the classification of stationary points (extrema) as maximum, minimum, saddle points, or ‘inconclusive.’