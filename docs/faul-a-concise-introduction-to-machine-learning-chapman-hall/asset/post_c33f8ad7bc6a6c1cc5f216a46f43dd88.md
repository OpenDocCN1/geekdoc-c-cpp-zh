
### Addition: In this case,

$$
2\Delta \mathcal{L} = \frac{Q_i^2 - S_i}{S_i} + \log \frac{S_i}{Q_i^2},\\
\tilde{\mathbf{\Sigma}} = \left( \begin{array}{cc} \mathbf{\Sigma} + \sigma^{-1} \mathbf{\Sigma} \mathbf{d}_i^T \mathbf{d}_i \mathbf{\Sigma} & -\sigma^{-2} \mathbf{\Sigma}_i \mathbf{\Sigma} \mathbf{D}^T \mathbf{d}_i \\ -\sigma^{-2} \mathbf{\Sigma} \mathbf{D}^T \mathbf{d}_i^T \mathbf{\Sigma} & \Sigma_{ii} \end{array} \right),\\
\tilde{\mathbf{\mu}} = \left( \begin{array}{c} \mathbf{\mu} - \sigma^{-2} \mu_i \mathbf{\Sigma} \mathbf{D}^T \mathbf{d}_i \\ \mu_i \end{array} \right),
$$

where $\Sigma_{ii} = (\alpha_i + S_i)^{-1}$ and $\mu_i = \Sigma_{ii} Q_i$.

Deletion: The index $j$ denotes the column of $\mathbf{D}$ which needs to be removed, when $d_i$ is removed from the current model. $\mathbf{\Sigma}_j$ is the $j^{th}$ column of $\mathbf{\Sigma}$ and $\Sigma_{jj}$ is the $j^{th}$ diagonal element. The $j^{th}$ element of $\mathbf{\mu}$ is $\mu_j$.

$$
2\Delta \mathcal{L} = \frac{Q_j^2}{S_i - \alpha_i} - \log \left( 1 - \frac{S_i}{\alpha_i} \right),\\
\tilde{\mathbf{\Sigma}} = \mathbf{\Sigma} - \frac{1}{\Sigma_{jj}} \mathbf{\Sigma}_j \mathbf{\Sigma}_j^T,\\
\tilde{\mathbf{\mu}} = \mathbf{\mu} - \frac{\mu_j}{\Sigma_{jj}} \mathbf{\Sigma}_j.
$$

After these updates the $j^{th}$ row and column needs to be removed from $\tilde{\mathbf{\Sigma}}$ and the $j^{th}$ element from $\tilde{\mathbf{\mu}}$.

### Re-estimation: Defining

$$
\kappa_j = (\Sigma_{jj} + (\tilde{\alpha}_i - \alpha_i)^{-1})^{-1}
$$

with $\Sigma_{jj}$ and $\mathbf{\Sigma}_j$ as in the case of deletion, we have

$$
2\Delta \mathcal{L} = \frac{Q_j^2}{S_i + (\tilde{\alpha}_i^{-1} - \alpha_i^{-1})^{-1}} - \log(1 + S_i(\tilde{\alpha}_i^{-1} - \alpha_i^{-1})),\\
\tilde{\mathbf{\Sigma}} = \mathbf{\Sigma} - \kappa_j \mathbf{\Sigma}_j \mathbf{\Sigma}_j^T,\\
\tilde{\mathbf{\mu}} = \mathbf{\mu} - \kappa_j \mu_j \mathbf{\Sigma}_j.
$$

We already noted that a new candidate basis function can be created and evaluated for inclusion in the model at any point in time. The model can also adapt, when a new data sample arrives. Thus, this technique is also suitable for online learning. We can calculate the change in the logarithm of the marginal likelihood for the current model, when a data sample $(t_*, \mathbf{x}_*)$ is added. This means adding a row to the design matrix $\mathbf{D}$ yielding

$$
\mathbf{D}_* = \begin{pmatrix} \mathbf{D} \\ \mathbf{d}(\mathbf{x}_*)^T \end{pmatrix}.
$$

We then have

$$
\mathbf{C}_* = \sigma^2 \mathbf{I} + \begin{pmatrix} \mathbf{D} \\ \mathbf{d}(\mathbf{x}_*)^T \end{pmatrix} \mathbf{A}^{-1} \left( \mathbf{D}^T \quad \mathbf{d}(\mathbf{x}_*) \right) = \begin{pmatrix} \mathbf{C} & \mathbf{v} \\ \mathbf{v}^T & v \end{pmatrix}
$$

where \(\mathbf{v} = \mathbf{D}\mathbf{A}^{-1}\mathbf{d}(\mathbf{x}_*)\) and \(v = \mathbf{d}(\mathbf{x}_*)^T \mathbf{A}^{-1} \mathbf{d}(\mathbf{x}_*) + \sigma^2\). Note that \(\mathbf{C}_*\) is symmetric.

Using the formulae for block matrices we have

$$
|\mathbf{C}_*| = |\mathbf{C}| |v - \mathbf{v}^T \mathbf{C}^{-1} \mathbf{v}|
$$

and

$$
\mathbf{C}_*^{-1} = \begin{pmatrix} \mathbf{C}^{-1} + \frac{\mathbf{C}^{-1} \mathbf{v} \mathbf{v}^T \mathbf{C}^{-1}}{v - \mathbf{v}^T \mathbf{C}^{-1} \mathbf{v}} & -\mathbf{C}^{-1} \mathbf{v} \frac{1}{v - \mathbf{v}^T \mathbf{C}^{-1} \mathbf{v}} \\ -\mathbf{v}^T \mathbf{C}^{-1} \frac{1}{v - \mathbf{v}^T \mathbf{C}^{-1} \mathbf{v}} & \frac{1}{v - \mathbf{v}^T \mathbf{C}^{-1} \mathbf{v}} \end{pmatrix}
$$

Letting \(\mathbf{t}_*^T = (t_1, ..., t_N, t_*)\), we can calculate

$$
\mathbf{t}_*^T \mathbf{C}_*^{-1} \mathbf{t}_* = \mathbf{t}^T \mathbf{C}^{-1} \mathbf{t} + \frac{1}{v - \mathbf{v}^T \mathbf{C}^{-1} \mathbf{v}} (\mathbf{v}^T \mathbf{C}^{-1} \mathbf{t} - t_*)^2
$$

Thus the logarithm of the marginal likelihood \(\log \mathcal{L}(\mathbf{t}|\mathbf{x}, \sigma^2)\) is \(\mathcal{L}(\mathbf{t}|\mathbf{x}, \sigma^2) + \Delta \mathcal{L}\), where

$$
\Delta \mathcal{L} = -\frac{1}{2} \left[ \log 2\pi + \log |v - \mathbf{v}^T \mathbf{C}^{-1} \mathbf{v}| + \frac{1}{v - \mathbf{v}^T \mathbf{C}^{-1} \mathbf{v}} (\mathbf{v}^T \mathbf{C}^{-1} \mathbf{t} - t_*)^2 \right] .
$$

This change can be interpreted probabilistically. Using the Woodbury matrix identity from Appendix A.1.3 again, \(\mathbf{\Sigma}\) is related to \(\mathbf{C}^{-1}\) by

$$
\mathbf{\Sigma} = \mathbf{A}^{-1} - \mathbf{A}^{-1} \mathbf{D}^T \mathbf{C}^{-1} \mathbf{D} \mathbf{A}^{-1} ,
$$

The predictive distribution for \(t_*\) has variance and mean

$$
\begin{aligned}
\sigma_*^2 &= \sigma^2 + \mathbf{d}(\mathbf{x}_*)^T \Sigma \mathbf{d}(\mathbf{x}_*) \\
&= \sigma^2 + \mathbf{d}(\mathbf{x}_*)^T (\mathbf{A}^{-1} - \mathbf{A}^{-1} \mathbf{D}^T \mathbf{C}^{-1} \mathbf{D} \mathbf{A}^{-1}) \mathbf{d}(\mathbf{x}_*) \\
&= \sigma^2 + \mathbf{d}(\mathbf{x}_*)^T \mathbf{A}^{-1} \mathbf{d}(\mathbf{x}_*) - \mathbf{v}^T \mathbf{C}^{-1} \mathbf{v} = v - \mathbf{v}^T \mathbf{C}^{-1} \mathbf{v}, \quad (8.10)
\end{aligned}
$$

$$
m_* = \mathbf{d}(\mathbf{x}_*)^T \mu = \sigma^{-2} \mathbf{d}(\mathbf{x}_*)^T \Sigma \mathbf{D}^T \mathbf{t} = \mathbf{v}^T \mathbf{C}^{-1} \mathbf{t} ,
$$

where we used the fact that \(\mathbf{D} \mathbf{A}^{-1} \mathbf{D}^T = \mathbf{C} - \sigma^2 \mathbf{I}\). Thus \((\mathbf{v}^T \mathbf{C}^{-1} \mathbf{t} - t_*)^2\) is the square of the difference of the sample measurement and its mean predicted by the current model.

Thus, the change in the log evidence is

$$
\begin{aligned}
\Delta \mathcal{L} &= -\frac{1}{2} \left[ \log 2\pi + \log \sigma_*^2 + \frac{(m_* - t_*)^2}{\sigma_*^2} \right] \\
&= \log \frac{1}{\sqrt{2\pi \sigma_*^2}} \exp \left( - \frac{(m_* - t_*)^2}{2 \sigma_*^2} \right) .
\end{aligned}
$$

Hence the change is the logarithm of the likelihood of the new data value $t_*$ at $\mathbf{x}_*$ given the predictive probability distribution $\mathcal{N}(m_*, \sigma_*^2)$. Since $\sigma_* \ge \sigma$, the change lies between $-\infty$ and $\log(2\pi\sigma^2)^{-1/2}$. It can be positive. In this case, the new sample affirms the model. If the likelihood of the data is small, the marginal likelihood is reduced, indicating that the model should be improved. To do so, all quantities need to be updated first with the new data included.

### New data sample: In this case,

$$
\Delta \mathcal{L} = \log \frac{1}{\sqrt{2\pi\sigma_*^2}} \exp \left( - \frac{(m_* - t_*)^2}{2\sigma_*^2} \right),
$$

$$
\bar{\Sigma} = \Sigma - \frac{1}{\sigma_*^2} \Sigma \mathbf{d}(\mathbf{x}_*) \mathbf{d}(\mathbf{x}_*)^T \Sigma,
$$

$$
\bar{\mu} = \mu - \frac{m_* - t_*}{\sigma_*^2} \Sigma \mathbf{d}(\mathbf{x}_*).
$$

Then the algorithm can continue improving the model by considering the basis functions in turn.

Sparse Bayesian learning infers a predictive distribution for $t_*$ which is $\mathcal{N}(m_*, \sigma_*^2)$ with mean and variance as given in (8.10). This predictive distribution is heavily dependent on the model, since it depends on $\mathbf{d}(\mathbf{x}_*)$ which are the basis functions included in the model evaluated at $\mathbf{x}_*$. It is customary to choose basis functions for the dictionary which decay quickly when moving away from their centre, or basis functions with finite, compact support. Therefore, the degenerate case is possible where $\mathbf{d}(\mathbf{x}_*)$ is close to, or even equal to zero, and in this case the predictive probability distribution becomes $\mathcal{N}(0, \sigma^2)$ which is meaningless. The confidence we place in the predictions should only be informed by the data, and be independent of the dictionary of basis functions.

Let $\mathcal{S}$ be a subset of the samples. This could be all samples or a suitable set of neighbours of $\mathbf{x}_*$. We estimate the probability distribution of $t_*$ to be normal with mean and variance

$$
\bar{m} = \max_{\mathbf{x}_i \in \mathcal{S}} \{t_i\},
$$

$$
\bar{\sigma} = \max_{\mathbf{x}_i \in \mathcal{S}} \{t_i\}.
$$

With this estimate, the expected change, when considering $\mathbf{x}_*$, in the log evidence is

$$
\begin{aligned}
\mathbb{E}[\Delta \mathcal{L}] &= \int_{-\infty}^{\infty} \left[ \log \frac{1}{\sqrt{2\pi\sigma_*^2}} - \frac{(t_* - m_*)^2}{2\sigma_*^2} \right] \\
&\quad \frac{1}{\sqrt{2\pi\sigma^2}} \exp \left( - \frac{(t_* - \bar{m})^2}{2\sigma^2} \right) dt_* \\
&= \log \frac{1}{\sqrt{2\pi\sigma_*^2}} - \frac{\sigma^2 + (\bar{m} - m_*)^2}{2\sigma_*^2}.
\end{aligned}
$$
