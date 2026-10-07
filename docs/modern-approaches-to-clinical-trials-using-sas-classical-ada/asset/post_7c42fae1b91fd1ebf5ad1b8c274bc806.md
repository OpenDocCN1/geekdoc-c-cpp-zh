
## 4.5 Specification of Prior Distributions

### 4.5.1 Fitting Priors

We extend the fitting prior in (4.8) to the partial borrowing power prior approach formally proposed in [6] and [10]. The partial borrowing prior is that the historical data are borrowed only through the common parameters shared in the model for the historical data and the current data. Thus, the strength of the historical data is borrowed only through the common parameters. The fitting prior for $(\gamma, \theta)$ under the metaregression survival model in (4.3) is 

```
$\pi^{(f)}(\gamma, \theta|D_0, a_0) \propto \prod_{j=1}^{K_0} \pi_{j=0}^{K_k}(\exp\{ij_j+l_k(\gamma_0 + \gamma_1 + \theta_k)\}) \times \exp\{-(\gamma_0 + \gamma_1 + \theta_k)/a_0+l_k\} \pi_0^{(f)}(\theta_0)d\theta_0 \pi_0^{(f)}(\gamma, \theta).$ (4.10)
```

where $0 \le a_0 \le 1$, $\pi_0^{(f)}(\theta_0)$ and $\pi_0^{(f)}(\gamma)$ are the initial priors. In (4.10), independent initial priors, $N(0,\sigma_{\theta_0}^2)$, $N(0,\sigma_{\gamma}^2)$, $N(0,\tau_{\theta_k}^2)$ and $N(0,\tau_{\gamma}^2)$ are assumed for $\gamma_0, \gamma_1, \theta_k$, and $\gamma_k$.

In (4.10), the parameter $a_0$ controls the influence of the historical metaserial data $D_0$ on the current data $D_K$. The parameter $a_0$ can be interpreted as a discounting parameter for the historical meta-survival data. It is reasonable to restrict the range of $a_0$ between 0 and 1, and thus we take $0 \le a_0 \le 1$. One of the main roles of $a_0$ is that it controls the heaviness of the tails for the prior for $\gamma_0$ and $\gamma_1$ in the model. As $a_0$ becomes smaller, the tails of (4.10) become heavier. If $a_0=0$, the prior does not depend on historical meta-survival data. That is, $a_0=0$ is equivalent to a prior specification with no incorporation of historical meta-survival data for the current study. Thus, the parameter $a_0$ controls the influence of the historical meta-survival data on the current study. Such control is important in the case where there is heterogeneity between the historical and current meta-survival data, or when the sample sizes of the historical and current meta-survival data are quite different.

In (4.10), we prefer to consider a fixed $a_0$. When $a_0$ is fixed, we know exactly how much historical meta-data are incorporated in the new meta-experimental trial, and also how the type I error and power are related to $a_0$. As shown in the simulation study in 4.7 SAS MACRO BSMED, a fixed $a_0$ provides us additional flexibility in controlling the type I error. In addition, our informative prior specification only allows us to borrow historical meta-experimental data for the models for the historical and current data. Thus, the historical meta-experimental data has the most influence on $\gamma_0$ and $\gamma_1$. For this reason, [6] and [10] call the power priors given in (4.10) "partial borrowing power priors."

### 4.5.2 Sampling Priors

Now, we turn to our attention to specify the sampling priors. Under the proposed model in (4.3), we take the sampling priors

$\pi^{(S)}[\gamma_l, \theta_l] \propto \alpha^{(S)}(\gamma_0) \pi^{(S)}(\theta_l) \pi_l^{(S)}(\gamma_1)$ for $l=0,1$. In the sampling prior, we first specify a point mass prior for $\gamma_1$ as $\pi^{(S)}(\gamma_1) = \Delta{\{\gamma_1=\log(\zeta)\}}$ for $l=0$ and

$\pi^{(S)}(\gamma_1) = \Delta{\{\gamma_1=0\}}$ for $l=1$, where $\Delta{\{\gamma_1=\gamma_1^*}}$ denotes a degenerate distribution at $\gamma_1=\gamma_1^*$, i.e., $P[\gamma_1=\gamma_1^*]=1$. We then specify a point mass prior for each of $\pi^{(S)}(\gamma_0)$ and $\pi^{(S)}(\theta_0)$ as well. Note that the choices of design values, $\{\gamma_0, \theta_0\}$ are obtained by solving the following simultaneous equations:

$1-\exp{\exp{\gamma_0+\theta_k\}}=r_k$ and $\sum_{k=1}^K\theta_k=0$.

where $r_k$ is a pre-determined annualized event rate for $k=1..K$. As in the example discussed in 4.7 SAS MACRO BSMED, we assume that the number of studies is $K=9$ and the annualized event rates are $r_k=0.012$ for $k=1..8$ and $r_g=0.015$. Then, by solving the above equations, we obtain $\gamma_0=-4.392, \theta_k=-0.025$ for $k=1..8$, and $\theta_g=-0.2$. Therefore, we can specify the point mass priors based on design values.

## 4.6 Computational Algorithms

### 4.6.1 Predictive Data Generation

In this section, we extend the computational algorithm in [6] and [10] to generate prior survival data by incorporating trial duration $\hat{T}_k^D$ and accrual time $\hat{\tau}_k^A$ discussed in 4.2 Design Setting. Specifically, we use $\hat{D}_k$ and $\hat{\tau}_k^A$ to construct censoring time in the generation of predictive survival data $D_K$ in addition to the sampling prior $\pi^{(S)}(\{\gamma, \theta\})$. Our new predictive data algorithm is given as follows:

- 1. Generate $\{\gamma, \theta\} \sim \pi^{(S)}(\{\gamma, \theta\})$.
- 2. Generate $Y_{ijk} \sim f(Y_{ijk}|\theta, x_{ijk})$ independently for $i=1..n_{jk}, j=1..2, k=1..K$.
- 3. Set $\tau_{ijk}^*=0$ if $\hat{\tau}_k^A=0$ and generate the accrual time $\tau_{ijk}^*=U(0, \hat{\tau}_k^A)$ independently if $\hat{\tau}_k^A>0$ for $i=1..n_{jk}, j=1..2, k=1..K$.
- 4. Set $C_{ijk}^*=\hat{\tau}_k^D-\hat{\tau}_k^A$ for $i=1..n_{jk}, j=1..2, k=1..K$.
- 5. Compute $y_{jk}=\sum_{i=1}^{n_{jk}}\min(Y_{ijk}, C_{ijk}^*)$ and $v_{jk}=\sum_{i=1}^{n_{jk}}1\{Y_{ijk} \le \tau_{ijk}^*\}$, where the indicator function $1\{Y_{ijk} \le \tau_{ijk}^*}=1$ if $Y_{ijk} \le \tau_{ijk}^*$ and 0 otherwise for $i=1..n_{jk}, j=1..2, k=1..K$.
- 6. Set $D_K=\{y_{jk}, v_{jk}, x_{ijk}\}, j=1..2, k=1..K$.

### 4.6.2 Sampling from the Posterior Distributions

Under the model in (4.3), using (4.4) and (4.10), the posterior distribution of $(\gamma, \theta_D, \theta_0)$ is given by

$\pi(\gamma, \theta_D, \theta_0 | D_K, D_0) \propto \prod_{k=1}^K \prod_{j=1}^2 \exp\{v_{jk}(\gamma_0 + \gamma_1 x_{jk} + \theta_k) - (\gamma_0 + \gamma_1 x_{jk} + \theta_k)v_{jk}\} \times \prod_{k=1}^K \prod_{j=1}^2 (\exp\{y_{0,j} + l_k(\gamma_0 + \gamma_1 + \theta_k)\})^{\theta_0} \pi_0^{(f)}(\theta_0)\pi_0^{(f)}(\gamma). (4.11)$

We use the Gibbs sampling algorithm to sample from the posterior distribution in (4.11) given $D_K$ and $D_0$. The Gibbs sampling algorithm requires sampling from the full conditional distribution of each parameter given the other parameters. First, the full conditional density for $[\gamma | \theta_D, \theta_0, D_K, D_0]$ is given by

$\pi(\gamma | \theta_D, \theta_0, D_K, D_0) \propto \prod_{k=1}^K \prod_{j=1}^2 \exp\{v_{jk}(\gamma_0 + \gamma_1 x_{jk} + \theta_k) - (\gamma_0 + \gamma_1 x_{jk} + \theta_k)v_{jk}\} \times \prod_{k=1}^K \prod_{j=1}^2 (\exp\{y_{0,j} + l_k(\gamma_0 + \gamma_1 + \theta_k)\})^{\theta_0} \exp\{-\frac{1}{2} \gamma^T \Sigma_{\gamma}^{-1} \gamma\}, (4.12)$

where $\Sigma_{\gamma} = \text{diag}(\sigma_0^2, \sigma_f^2)$ denotes a $2 \times 2$ covariance matrix of $\gamma$.

The full conditional density for $[\theta_0 | \theta_D, D_0, a_0]$ is given by

$\pi(\theta_0 | \theta_D, D_0, a_0) \propto \prod_{k=1}^K \prod_{j=1}^2 (\exp\{y_{0,j} + l_k(\gamma_0 + \gamma_1 + \theta_k)\})^{\theta_0} \exp\{-exp[\gamma_0 + \gamma_1 j + \theta_k]y_{j}]^{\theta_0}\} \exp\{-\frac{1}{2}\theta_0^T \Sigma_{\theta_0} \theta_0\}, (4.13)$

where $\Sigma_{\theta_0} = \sigma_0^2/K_0$ denotes a $K_0 \times K_0$ covariance matrix of $\theta_0$.

It is easy to show that the full conditional distributions in (4.11) to (4.13) are log-concave in each parameter. Then, we can implement the adaptive rejection algorithm of [15] to sample from the posterior distribution of $[\gamma, \theta, \theta_0]$.
