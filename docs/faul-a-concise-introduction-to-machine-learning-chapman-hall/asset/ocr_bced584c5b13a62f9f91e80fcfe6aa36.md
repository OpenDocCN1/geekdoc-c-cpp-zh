which depends on v.

The Expectation-Maximization algorithm calculates the expectation of the logarithm of the joint data likelihood with respect to the conditional probability distribution of the latent variables \(\mathbf{u}_1, \dots, \mathbf{u}_N\). The logarithm of the joint data likelihood is

\(\mathcal{L} = \log \prod_{n=1}^N p(\mathbf{v}_n, \mathbf{u}_n) = -\frac{1}{2} \sum_{n=1}^N \left[ (K+D) \log(2\pi) + D \log(\sigma^2) + \mathbf{u}_n^T \mathbf{u}_n + \sigma^{-2} (\mathbf{v}_n - \boldsymbol{\mu})^T (\mathbf{v}_n - \boldsymbol{\mu}) - 2\sigma^{-2} \mathbf{u}_n^T \mathbf{W}^T (\mathbf{v}_n - \boldsymbol{\mu}) + \sigma^{-2} \mathbf{u}_n^T \mathbf{W}^T \mathbf{W} \mathbf{u}_n \right].\)

When taking the expectation with respect to the latent variables, we have

\(\mathbb{E}[\mathbf{u}_n] = \boldsymbol{\mu}_{\mathbf{u}|\mathbf{v}_n}.\) (7.8)

To find the expectation of the inner product of \(\mathbf{u}_n\) with itself, we use the cyclic permutation property of the trace and the fact that the operations of calculating the trace and expectation commute,

\(\mathbb{E}[\mathbf{u}_n^T \mathbf{u}_n] = \mathbb{E}[\text{tr}(\mathbf{u}_n^T \mathbf{u}_n)] = \mathbb{E}[\text{tr}(\mathbf{u}_n \mathbf{u}_n^T)] = \text{tr}(\mathbb{E}[\mathbf{u}_n \mathbf{u}_n^T]).\)

Similarly,

\(\mathbb{E}[\mathbf{u}_n^T \mathbf{W}^T \mathbf{W} \mathbf{u}_n] = \mathbb{E}[\text{tr}(\mathbf{u}_n^T \mathbf{W}^T \mathbf{W} \mathbf{u}_n)] = \mathbb{E}[\text{tr}(\mathbf{W}^T \mathbf{W} \mathbf{u}_n \mathbf{u}_n^T)]\)
\(= \text{tr}(\mathbf{W}^T \mathbf{W} \mathbb{E}[\mathbf{u}_n \mathbf{u}_n^T]).\)

We can then use (2.10) to calculate

\(\mathbb{E}[\mathbf{u}_n \mathbf{u}_n^T] = \boldsymbol{\Sigma}_{\mathbf{u}|\mathbf{v}} + \mathbb{E}[\mathbf{u}_n] \mathbb{E}[\mathbf{u}_n]^T = \boldsymbol{\Sigma}_{\mathbf{u}|\mathbf{v}} + \boldsymbol{\mu}_{\mathbf{u}|\mathbf{v}_n} \boldsymbol{\mu}_{\mathbf{u}|\mathbf{v}_n}^T.\) (7.9)

The expectation of the logarithm of the joint data likelihood is therefore

\(\mathbb{E}[\mathcal{L}] = -\frac{1}{2} \sum_{n=1}^N \left[ (K+D) \log(2\pi) + D \log(\sigma^2) + \text{tr}(\mathbb{E}[\mathbf{u}_n \mathbf{u}_n^T]) + \right.\)
\(\left. \sigma^{-2} \|\mathbf{v}_n - \boldsymbol{\mu}\|^2 - 2\sigma^{-2} \mathbb{E}[\mathbf{u}_n]^T \mathbf{W}^T (\mathbf{v}_n - \boldsymbol{\mu}) + \right.\)
\(\left. \sigma^{-2} \text{tr}(\mathbf{W}^T \mathbf{W} \mathbb{E}[\mathbf{u}_n \mathbf{u}_n^T]) \right].\)

Now, employing the cyclic permutation property of the trace, the formulae given in Appendices A.2.6 and A.2.9 and the symmetry of \(\mathbb{E}[\mathbf{u}_n \mathbf{u}_n^T]\), the derivative with respect to \(\mathbf{W}\) is

\(\frac{\partial}{\partial \mathbf{W}} \mathbb{E}[\mathcal{L}] = -\frac{1}{2} \sum_{n=1}^N \left[ -2\sigma^{-2} (\mathbf{v}_n - \boldsymbol{\mu}) \mathbb{E}[\mathbf{u}_n]^T + 2\sigma^{-2} \mathbf{W} \mathbb{E}[\mathbf{u}_n \mathbf{u}_n^T] \right].\)