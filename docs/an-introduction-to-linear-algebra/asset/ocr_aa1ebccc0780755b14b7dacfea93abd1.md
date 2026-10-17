# Theorem 22.4.

Let the symmetric matrix $A$ in (22.2) have the eigenvalues $\lambda_1\leq\cdots\leq\lambda_n$ and associated $u^1,\ldots,u^n$ orthonormal eigenvectors. Then, for the quadratic form $q_n(x)=x^tAx$ subject to the constraints $\|x\|_2=1$ and $(x,u^n)=0$, the following hold:

+   (i) maximum value is $\lambda_{n-1}$ and attained at $x=u^{n-1}$,  
+   (ii) minimum value is $\lambda_1$ and attained at $x=u^1$.

# Proof.

From (14.5) for a given $x\in R^n$, we have $x=\sum_{i=1}^n c_i u^i$, where $c_i=(x,u^i)$, $1\leq i\leq n$, but since $c_n=0$ it follows that $x=\sum_{i=1}^{n-1}c_i u^i$, which implies that $\|x\|_2^2=\sum_{i=1}^{n-1}c_i^2=1$ (as given). Now we successively have

```
$$\begin{aligned}
q_n(x)&=x^tAx=x^tA\left(\sum_{i=1}^{n-1}c_i u^i\right)=x^t\left(\sum_{i=1}^{n-1}c_iAu^i\right)\\
&=\left(x,\sum_{i=1}^{n-1}\lambda_i c_i u^i\right)=\left(\sum_{i=1}^{n-1}c_i u^i,\sum_{i=1}^{n-1}\lambda_i c_i u^i\right)\\
&=\sum_{i=1}^{n-1}\lambda_i c_i^2\leq\lambda_{n-1}\sum_{i=1}^{n-1}c_i^2=\lambda_{n-1}.
\end{aligned}$$
```

Next, we note that for $x=u^{n-1}$, $c_{n-1}=1$ and $c_i=0$, $1\leq i\leq n-2$, and hence $q(u^{n-1})=\lambda_{n-1}$, i.e., $q_n(x)$ attains its maximum at $x=u^{n-1}$. The minimum value of $q_n(x)$ by the constraint $(x,u^n)=0$ does not change.

# Example 22.7.

From Example 22.1 and Theorem 22.4, it follows that

```
$$6\leq 11x_1^2+11x_2^2+14x_3^2-2x_1x_2-8x_1x_3-8x_2x_3\leq 12$$
```

provided $x_1^2+x_2^2+x_3^2=1$ and $-x_1-x_2+2x_3=0$. The left equality holds for $x=\left(\frac{1}{\sqrt{3}},\frac{1}{\sqrt{3}},\frac{1}{\sqrt{3}}\right)$ and the right inequality holds for $\left(-\frac{1}{\sqrt{2}},\frac{1}{\sqrt{2}},0\right)$.

The following extension of Theorem 22.4 is immediate.

# Theorem 22.5.

Let $\lambda_i$ and $u^i$, $1\leq i\leq n$ be as in Theorem 22.4. Then, for the quadratic form $q_n(x)=x^tAx$ subject to the constraints $\|x\|_2=1$ and $(x,u^n)=\cdots=(x,u^{n-k+1})=0$ the maximum (minimum) value is $\lambda_{k-1}$ ($\lambda_1$) and attained at $x=u^{k-1}$ ($u^1$).

# Problems

+   22.1. Find the canonical form for the quadratic form $q_3(x)=2x_1x_2+x_1x_3-2x_2x_3$.

+   22.2. Find the canonical form for the quadratic form $q_3(x)=x_1^2+\frac{7}{8}x_2^2-\frac{7}{8}x_3^2+2x_1x_2+2x_1x_3+x_2x_3$.