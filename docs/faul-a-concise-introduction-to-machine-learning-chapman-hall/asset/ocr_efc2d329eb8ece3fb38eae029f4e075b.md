![](bbox=[0.25, 0.1, 0.75, 0.65])

covariance matrix \(\mathbf{K}\). The point values of \(\mathbf{f}\) are plotted as functions. Figure 8.12 shows the results of four draws for each of the implemented kernels.

Consider the case, when in our model \(d_1(\mathbf{x}) = 1\) and \(d_{d+1}(\mathbf{x}) = x_d\), the \(d^{\text{th}}\) component of \(\mathbf{x}\) for \(d = 1, \dots, D\). This means, the model is a linear polynomial.

In this case,
\(\alpha^{-1}\mathbf{d}(\mathbf{x}_i)^T \mathbf{d}(\mathbf{x}_j) = \alpha^{-1}(1 + \mathbf{x}_i^T \mathbf{x}_j).\)

Thus this is the linear kernel with \(\theta_1 = \theta_2 = \alpha^{-1}\).