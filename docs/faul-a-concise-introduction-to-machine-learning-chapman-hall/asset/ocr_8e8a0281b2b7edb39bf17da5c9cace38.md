![](bbox=[0.33, 0.1, 0.67, 0.28])

(a) Gaussian kernel, \(\theta_1 \approx 2.81, \theta_2 \approx 2.85\)

![](bbox=[0.15, 0.35, 0.48, 0.53])

(b) Exponential kernel, \(\theta_1 \approx 1.75, \theta_2 \approx 1.66\)

![](bbox=[0.52, 0.35, 0.85, 0.53])

(c) Inverse multiquadric kernel, \(\theta_1 \approx 3.21, \theta_2 \approx 4.74\)

Figure 8.14: Draws from the posterior Gaussian process for different kernels.

Thus the derivative of the kernel with regards to its parameters is needed. For the Gaussian kernel

```
\(k(\mathbf{x}, \mathbf{y}) = \theta_1^2 \exp \left( - \frac{\|\mathbf{x} - \mathbf{y}\|^2}{2\theta_2^2} \right),\)
```

this is for example

```
\(\frac{\partial}{\partial \theta_1} k(\mathbf{x}, \mathbf{y}) = 2\theta_1 \exp \left( - \frac{\|\mathbf{x} - \mathbf{y}\|^2}{2\theta_2^2} \right) = \frac{2}{\theta_1} k(\mathbf{x}, \mathbf{y}),\)
\(\frac{\partial}{\partial \theta_2} k(\mathbf{x}, \mathbf{y}) = \frac{\|\mathbf{x} - \mathbf{y}\|^2}{\theta_2^3} \theta_1^2 \exp \left( - \frac{\|\mathbf{x} - \mathbf{y}\|^2}{2\theta_2^2} \right) = \frac{\|\mathbf{x} - \mathbf{y}\|^2}{\theta_2^3} k(\mathbf{x}, \mathbf{y}).\)
```

Setting the gradient of \(\mathcal{L}\) to zero and solving for the parameters is generally not straight forward. However, since the gradient is known, it can be used to approximate the maximum iteratively (see for example [2]).