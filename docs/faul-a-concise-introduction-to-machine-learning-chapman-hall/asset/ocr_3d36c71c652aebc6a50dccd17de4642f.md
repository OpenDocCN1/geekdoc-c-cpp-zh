Hence, K is positive semi-definite, and the product of two kernels is a kernel. From this we can deduce that, if $p$ is a polynomial with non-negative coefficients, then $p(k(\mathbf{x}, \mathbf{y}))$ is a valid kernel, if $k(\mathbf{x}, \mathbf{y})$ is a valid kernel function. Also $\exp(k(\mathbf{x}, \mathbf{y}))$ is a valid kernel as the limit of a polynomial with positive coefficients.

Since the positive semi-definiteness has to hold for any set of points, it has to also hold for $\{\psi(\mathbf{a}_1), \dots, \psi(\mathbf{a}_N)\}$, where $\psi: \mathbb{R}^e \rightarrow \mathbb{R}^M$ is any mapping and $\{\mathbf{a}_1, \dots, \mathbf{a}_N\}$ is any set in $\mathbb{R}^e$. Therefore, if $k(\mathbf{x}, \mathbf{y})$ is a valid kernel, so is $k(\psi(\mathbf{a}), \psi(\mathbf{b}))$ on $\mathbb{R}^e \times \mathbb{R}^e$. In particular, $\psi$ can be the restriction onto a subset of components of $\mathbf{x}$. Let $\mathbf{x}_a, \mathbf{y}_a \in \mathbb{R}^e$ and $\mathbf{x}_b, \mathbf{y}_b \in \mathbb{R}^e$ be such restrictions. They do not necessarily need to be disjoint or use all components of $\mathbf{x}$. Let $k_a(\mathbf{x}_a, \mathbf{y}_a)$ and $k_b(\mathbf{x}_b, \mathbf{y}_b)$ be the kernels obtained by the restrictions; then
$$k(\mathbf{x}, \mathbf{y}) = k_a(\mathbf{x}_a, \mathbf{y}_a) + k_b(\mathbf{x}_b, \mathbf{y}_b) \quad \text{and} \quad k(\mathbf{x}, \mathbf{y}) = k_a(\mathbf{x}_a, \mathbf{y}_a)k_b(\mathbf{x}_b, \mathbf{y}_b)$$
are valid kernels on $\mathbb{R}^M \times \mathbb{R}^M$.

Thus, there is a multitude of possibilities to construct kernels. Some popular examples of kernels are:

# **Linear (trivial) kernel** $k(\mathbf{x}, \mathbf{y}) = \theta_1^2 + \theta_2^2 \mathbf{x}^T \mathbf{y}$.

# **Quadratic kernel** $k(\mathbf{x}, \mathbf{y}) = (\theta_1^2 + \theta_2^2 \mathbf{x}^T \mathbf{y})^2$.

# **Polynomial kernel (of degree d)** $k(\mathbf{x}, \mathbf{y}) = (\theta_1^2 + \theta_2^2 \mathbf{x}^T \mathbf{y})^d$.

# **Hyperbolic tangent (Sigmoid) kernel** $k(\mathbf{x}, \mathbf{y}) = \tanh(\theta_1^2 + \theta_2^2 \mathbf{x}^T \mathbf{y})$.

Additive and multiplicative constants have to be positive. To ensure this, squared parameters are chosen. This also helps, when the parameters are optimized, since then this is an unconstrained optimization problem, while otherwise it would be a constrained optimization problem.

Considering the inner product $\mathbf{x}^T \mathbf{y}$ for a given vector x, vectors $\mathbf{y}$ lying on the line orthogonal to $\mathbf{x}$ are given the value zero for this relationship. Samples lying on the same side of this line as $\mathbf{x}$ are given a positive value, while samples on the other side are given a negative value. The absolute values increase with the distance from this line. The additive constant $\theta_1$ shifts the zero line, while the multiplicative constant $\theta_2$ controls the rate of this increase. For the linear kernel the shift is absorbed in the bias. Hence setting $\theta_1$ to zero in this context suffices.

The hyperbolic tangent kernel addresses the problem that absolute values of the inner product increase with the distance from the zero line. As the arguments of the hyperbolic tangent tend to plus or minus infinity, the result tends to +1 or -1 respectively. The values of the hyperbolic tangent are illustrated in Figure 5.3 for different multiplicative constants $\theta_2$, but fixed $\mathbf{y} = (1, 1)^T$ and $\theta_1 = 0$. For smaller $\theta_2$ the change from -1 to +1 is less rapid. The additive and multiplicative constants are parameters which need to be optimized or tuned for the specific application. When tuning, a validation set