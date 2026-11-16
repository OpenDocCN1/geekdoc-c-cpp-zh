![](bbox=[0.11, 0.1, 0.89, 0.55])

Figure 6.7: Data generated for \(\nu = 10\).

Let \(\mathcal{D} = \{ \mathbf{v}_1, \dots, \mathbf{v}_N \}\) be draws from \(\mathcal{N}(\mathbf{0}, \Sigma)\). The likelihood of this data is given by

```
\(\prod_{n=1}^N \frac{1}{\sqrt{(2\pi)^d |\Sigma|}} \exp \left( -\frac{1}{2} \mathbf{v}_n^T \Sigma^{-1} \mathbf{v}_n \right) = (2\pi)^{-dN/2} |\Sigma|^{-N/2} \exp \left( -\frac{1}{2} \sum_{n=1}^N \mathbf{v}_n^T \Sigma^{-1} \mathbf{v}_n \right).\)
```

The posterior distribution of \(\Sigma\) is proportional to the product of the likelihood and the prior probability density function as given in (6.10) by Bayes' rule. Because of the proportionality, we drop all multiplicative constants in both. These are the factors \((2\pi)^{-dN/2}\), \(|\Psi|^{\nu/2}\), \(2^{-\nu d/2}\) and \(1/\Gamma_d(\nu/2)\). Hence, the posterior is proportional to

```
\(|\Sigma|^{-N/2} \exp \left( -\frac{1}{2} \sum_{n=1}^N \mathbf{v}_n^T \Sigma^{-1} \mathbf{v}_n \right) |\Sigma|^{-(\nu+d+1)/2} \exp \left( -\frac{1}{2} \text{tr}(\Psi \Sigma^{-1}) \right).\)
```