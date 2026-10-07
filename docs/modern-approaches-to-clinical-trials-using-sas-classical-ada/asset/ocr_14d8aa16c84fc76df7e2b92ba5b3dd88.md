# 10.5 Power and Sample Size for Response-Adaptive Randomization

For a randomized design with a fixed predetermined allocation $ho$ (e.g. $ho=1/2$ or $ho=2/3$), both the total sample size $n$ and the treatment group sizes $n_E=np$ and $n_C=n(1-ho)$ are fixed quantities, appropriately chosen to achieve the desired power of a test. A RAR trial, the total sample size $n$ is fixed, but the treatment group sizes $N_E(n)$ and $N_C(n)$ are random. Therefore, when planning a RAR trial, some special considerations are required for sample size and power.

Hu and Rosenberger in [14] presented an approach to determine an appropriate sample size for a RAR design with target allocation $p_E, p_C$. Considering the one-sided hypothesis $H_0: p_E=p_C$ versus $H_a: p_E>p_C$. For a given significance $\alpha$, $H_0$ is rejected if the test statistic

```
$\frac{\hat{p}_E-\hat{p}_C}{\sqrt{\frac{\hat{p}_E}{N_E(n)}+\frac{\hat{p}_C}{N_C(n)}}} > z_{1-\alpha}}$
```

where $z_{1-\alpha}$ is the $100(1-\alpha)$th quantile of the standard normal distribution. Under the assumptions $N_k(n) \to \infty$ almost surely, $\hat{p}_k\hat{q}_k \to p_kq_k$ in probability, and $\sqrt{n_k}(\hat{p}_k-p_k) \to N(0, p_kq_k)$ in distribution for $k=E,C$ (which holds true for RAR procedures considered in Sections 10.3.2, 10.3.3, and 10.3.4), the power function can be approximated as

```
$P[p_E, p_C. N_E(n), N_C(n)] = Pr \left( \frac{\hat{p}_E-\\hat{p}_C}{\sqrt{\frac{\hat{p}_E}{N_E(n)}+\frac{\hat{p}_C}{N_C(n)}}} > z_{1-\alpha} \right) = \Phi \left( \frac{p_E-p_C}{\sqrt{\frac{p_E}{N_E(n)}+\frac{p_C}{N_C(n)}}} - z_{1-\alpha} \right), (10.11)$
```

where $\Phi{\cdot$ is the cumulative distribution function of the standard normal distribution.

Importantly, quantity (10.11) is a random variable because $N_E(n)$ and $N_C(n)$ are random. Under further asymptotic assumptions (that are met for RAR procedures considered thus far):