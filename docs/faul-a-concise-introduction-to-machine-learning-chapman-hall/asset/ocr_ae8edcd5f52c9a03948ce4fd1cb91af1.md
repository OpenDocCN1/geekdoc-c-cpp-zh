![](bbox=[0.18, 0.1, 0.48, 0.29])

![](bbox=[0.52, 0.1, 0.82, 0.29])

![](bbox=[0.18, 0.31, 0.48, 0.5])

![](bbox=[0.52, 0.31, 0.82, 0.5])

# Figure 7.8: Kernel Principal Component Analysis.

Hence the vector

```
\(\tilde{\mathbf{w}}_k = (\mathbf{I} - \frac{1}{N}\mathbf{E})\mathbf{\Phi}^T \mathbf{w}_k\) (7.14)
```

is an eigenvector of the \(N \times N\), symmetric matrix \((\mathbf{I} - \frac{1}{N}\mathbf{E})\mathbf{\Phi}^T \mathbf{\Phi}(\mathbf{I} - \frac{1}{N}\mathbf{E})\) with eigenvalue \(\tilde{\lambda}_k = N \lambda_k\). Note that due to \(\mathbf{I} - \frac{1}{N}\mathbf{E}\) being idempotent, we have \((\mathbf{I} - \frac{1}{N}\mathbf{E})\mathbf{w}_k = \mathbf{w}_k\). Thus, the components of \(\tilde{\mathbf{w}}_k\) sum to zero.

The \((i,j)\) entry of \(\mathbf{\Phi}^T \mathbf{\Phi}\) is the inner product

```
\(\phi(\mathbf{v}_i)^T \phi(\mathbf{v}_j) = k(\mathbf{v}_i, \mathbf{v}_j)\).
```

\(\mathbf{K} = \mathbf{\Phi}^T \mathbf{\Phi}\) is known as the kernel matrix. Kernel Principal Component Analysis calculates the eigenvalues \(N \lambda_k\) and eigenvectors \(\tilde{\mathbf{w}}_k\) of \((\mathbf{I} - \frac{1}{N}\mathbf{E})\mathbf{K}(\mathbf{I} - \frac{1}{N}\mathbf{E})\).

Multiplying Equation (7.14) from the left with \(\mathbf{\Phi}/N\), gives

```
\(\frac{1}{N}\mathbf{\Phi}\tilde{\mathbf{w}}_k = \frac{1}{N}\mathbf{\Phi}(\mathbf{I} - \frac{1}{N}\mathbf{E})\mathbf{\Phi}^T \mathbf{w}_k = \mathbf{\Sigma} \mathbf{w}_k = \lambda_k \mathbf{w}_k\).
```

Hence, \(\mathbf{w}_k\) is a linear combination of the images \(\phi(\mathbf{v}_1), \dots, \phi(\mathbf{v}_N)\), since

```
\(\mathbf{w}_k = \frac{1}{N\lambda_k} \sum_{n=1}^N \hat{w}_{kn} \phi(\mathbf{v}_n)\),
```