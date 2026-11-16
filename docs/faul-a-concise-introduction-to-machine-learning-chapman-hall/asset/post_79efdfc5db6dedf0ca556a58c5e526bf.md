
Hence, K is positive semi-definite, and the product of two kernels is a kernel. From this we can deduce that, if $p$ is a polynomial with non-negative coefficients, then $p(k(\mathbf{x}, \mathbf{y}))$ is a valid kernel, if $k(\mathbf{x}, \mathbf{y})$ is a valid kernel function. Also $\exp(k(\mathbf{x}, \mathbf{y}))$ is a valid kernel as the limit of a polynomial with positive coefficients.

Since the positive semi-definiteness has to hold for any set of points, it has to also hold for $\{\psi(\mathbf{a}_1), \dots, \psi(\mathbf{a}_N)\}$, where $\psi: \mathbb{R}^e \rightarrow \mathbb{R}^M$ is any mapping and $\{\mathbf{a}_1, \dots, \mathbf{a}_N\}$ is any set in $\mathbb{R}^e$. Therefore, if $k(\mathbf{x}, \mathbf{y})$ is a valid kernel, so is $k(\psi(\mathbf{a}), \psi(\mathbf{b}))$ on $\mathbb{R}^e \times \mathbb{R}^e$. In particular, $\psi$ can be the restriction onto a subset of components of $\mathbf{x}$. Let $\mathbf{x}_a, \mathbf{y}_a \in \mathbb{R}^e$ and $\mathbf{x}_b, \mathbf{y}_b \in \mathbb{R}^e$ be such restrictions. They do not necessarily need to be disjoint or use all components of $\mathbf{x}$. Let $k_a(\mathbf{x}_a, \mathbf{y}_a)$ and $k_b(\mathbf{x}_b, \mathbf{y}_b)$ be the kernels obtained by the restrictions; then
$$k(\mathbf{x}, \mathbf{y}) = k_a(\mathbf{x}_a, \mathbf{y}_a) + k_b(\mathbf{x}_b, \mathbf{y}_b) \quad \text{and} \quad k(\mathbf{x}, \mathbf{y}) = k_a(\mathbf{x}_a, \mathbf{y}_a)k_b(\mathbf{x}_b, \mathbf{y}_b)$$
are valid kernels on $\mathbb{R}^M \times \mathbb{R}^M$.

Thus, there is a multitude of possibilities to construct kernels. Some popular examples of kernels are:

- **Linear (trivial) kernel** $k(\mathbf{x}, \mathbf{y}) = \theta_1^2 + \theta_2^2 \mathbf{x}^T \mathbf{y}$.

- **Quadratic kernel** $k(\mathbf{x}, \mathbf{y}) = (\theta_1^2 + \theta_2^2 \mathbf{x}^T \mathbf{y})^2$.

- **Polynomial kernel (of degree d)** $k(\mathbf{x}, \mathbf{y}) = (\theta_1^2 + \theta_2^2 \mathbf{x}^T \mathbf{y})^d$.

- **Hyperbolic tangent (Sigmoid) kernel** $k(\mathbf{x}, \mathbf{y}) = \tanh(\theta_1^2 + \theta_2^2 \mathbf{x}^T \mathbf{y})$.

Additive and multiplicative constants have to be positive. To ensure this, squared parameters are chosen. This also helps, when the parameters are optimized, since then this is an unconstrained optimization problem, while otherwise it would be a constrained optimization problem.

Considering the inner product $\mathbf{x}^T \mathbf{y}$ for a given vector x, vectors $\mathbf{y}$ lying on the line orthogonal to $\mathbf{x}$ are given the value zero for this relationship. Samples lying on the same side of this line as $\mathbf{x}$ are given a positive value, while samples on the other side are given a negative value. The absolute values increase with the distance from this line. The additive constant $\theta_1$ shifts the zero line, while the multiplicative constant $\theta_2$ controls the rate of this increase. For the linear kernel the shift is absorbed in the bias. Hence setting $\theta_1$ to zero in this context suffices.

The hyperbolic tangent kernel addresses the problem that absolute values of the inner product increase with the distance from the zero line. As the arguments of the hyperbolic tangent tend to plus or minus infinity, the result tends to +1 or -1 respectively. The values of the hyperbolic tangent are illustrated in Figure 5.3 for different multiplicative constants $\theta_2$, but fixed $\mathbf{y} = (1, 1)^T$ and $\theta_1 = 0$. For smaller $\theta_2$ the change from -1 to +1 is less rapid. The additive and multiplicative constants are parameters which need to be optimized or tuned for the specific application. When tuning, a validation set ![](img/d3c00252180686426c9e63ab889b535b_137_0.png) is used to ensure the resulting classifier generalizes well to unseen data. It is important to note that for certain choices of \(\theta_1\) and \(\theta_2\), the hyperbolic tangent is not a valid kernel. For example, for \(\theta_1 = \theta_2 = 1\) and \(\mathbf{x}_1 = (0.5, 0)^T\) and \(\mathbf{x}_2 = (1, 0)\), the Gram matrix is

```
\(\mathbf{K} = \begin{pmatrix} \tanh(1.25) & \tanh(1.5) \\ \tanh(1.5) & \tanh(2) \end{pmatrix}\)
```

and has a negative eigenvalue and therefore is not positive semi-definite. Nevertheless, the hyperbolic tangent kernel is used in practice. Burges in [7] derives necessary conditions for functions based on the inner product to be valid kernels, as well as giving insight into the construction of kernels.

In some cases, it is possible to recover the mapping \(\phi\). To illustrate this let \(M = 2\) and we consider the quadratic kernel:

```
\(k(\mathbf{x}, \mathbf{y}) = (\theta_1^2 + \theta_2^2 \mathbf{x}^T \mathbf{y})^2\)
\(= (\theta_1^2 + \theta_2^2 x_1 y_1 + \theta_2^2 x_2 y_2)^2\)
\(= \theta_1^4 + \theta_2^4 x_1^2 y_1^2 + \theta_2^4 x_2^2 y_2^2 + 2\theta_1^2 x_1 y_1 x_2 y_2 + 2\theta_1^2 \theta_2^2 x_1 y_1 + 2\theta_1^2 \theta_2^2 x_2 y_2\)
\(= \left( \theta_1^2, \theta_2^2 x_1^2, \theta_2^2 x_2^2, \sqrt{2}\theta_2^2 x_1 x_2, \sqrt{2}\theta_1 \theta_2 x_1, \sqrt{2}\theta_1 \theta_2 x_2, \right.\)
\(\left. \sqrt{2}\theta_2^2 y_1 y_2, \sqrt{2}\theta_1 \theta_2 y_1, \sqrt{2}\theta_1 \theta_2 y_2 \right)\)
\(= \phi(\mathbf{x})^T \phi(\mathbf{y})\).
```

Hence, in this case, the quadratic kernel is an implicit mapping to a six-dimensional space.

It is more intuitive to let the relationship between samples depend on the distance between them, that is the Euclidean norm (\(L_2\) norm) of their difference, \(\|\mathbf{x} - \mathbf{y}\|\). This leads to the class of radial basis function (RBF) kernels.

- **Gaussian kernel** \(k(\mathbf{x}, \mathbf{y}) = \theta_1^2 \exp \left( -\frac{\|\mathbf{x} - \mathbf{y}\|^2}{2\theta_2^2} \right)\).

- **Exponential kernel** \(k(\mathbf{x}, \mathbf{y}) = \theta_1^2 \exp \left( -\frac{\|\mathbf{x} - \mathbf{y}\|}{\theta_2} \right)\).

- **Multiquadric kernel** \(\theta_1^2 \left( 1 + \frac{\|\mathbf{x} - \mathbf{y}\|^2}{2\theta_2^2} \right)^{1/2}\).

- **Inverse multiquadric kernel** \(\theta_1^2 \left( 1 + \frac{\|\mathbf{x} - \mathbf{y}\|^2}{2\theta_2^2} \right)^{-1/2}\).

- **Rational quadratic kernel** \(\theta_1^2 \left( 1 + \frac{\|\mathbf{x} - \mathbf{y}\|^2}{2\alpha\theta_2^2} \right)^{-\alpha}, \alpha > 0\).

- **Thin plate spline kernel** \(\theta_1^2 \|\mathbf{x} - \mathbf{y}\|^2 \log(\|\mathbf{x} - \mathbf{y}\|) + \theta_2^2\).

As an example, we show that the Gaussian kernel is a valid kernel. Firstly, \(\|\mathbf{x} - \mathbf{y}\|^2 = \mathbf{x}^T \mathbf{x} - 2\mathbf{x}^T \mathbf{y} + \mathbf{y}^T \mathbf{y}\)

and the kernel can be written as

```
\(k(\mathbf{x}, \mathbf{y}) = \theta_1 \exp \left( -\frac{1}{2\theta_2^2} \mathbf{x}^T \mathbf{x} \right) \exp \left( \frac{1}{\theta_2^2} \mathbf{x}^T \mathbf{y} \right) \theta_1 \exp \left( -\frac{1}{2\theta_2^2} \mathbf{y}^T \mathbf{y} \right)\)
\(= f(\mathbf{x}) \exp \left( \frac{1}{\theta_2^2} \mathbf{x}^T \mathbf{y} \right) f(\mathbf{y}).\)
```

This is a valid kernel, since it is the exponential of the inner product multiplied by a positive constant, and because of Equation (5.1).

The Gaussian kernel is also known as a squared exponential kernel or exponentiated quadratic kernel. It is an intuitive similarity measure. If the sample \(\mathbf{y}\) happens to be the same as sample \(\mathbf{x}\), the Gaussian kernel evaluates to \(\theta_1^2\), its maximum value. \(\theta_1\) is known as the signal standard deviation. With the Euclidean distance between samples increasing, the similarity measure given by the Gaussian kernel decreases, the rate of decrease being determined by \(\theta_2\), which is the characteristic length scale.

Figure 5.4 gives two examples of Gaussian kernels, for different choices of \(\theta_2\). The choice of \(\theta_2\) is crucial in the performance of the kernel, since it determines the width of the kernel. The larger the \(\theta_2\), the wider the base of the kernel. The kernels are centred at the support vectors. If the width is chosen too narrow, the kernels evaluate to nearly zero for all samples except the ones close to support vectors. If it is chosen too wide, the kernels evaluate to values similar to each other, since the slope is at a low angle. It is then hard to make a distinction between samples.
