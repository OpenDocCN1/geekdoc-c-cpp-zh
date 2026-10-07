# Chapter 6 Likelihood Models for Overdispersed Count Responses 185

Hurdle models can naturally accommodate either overdispersion (i.e., Var(Y)>E(Y)) or under dispersion (i.e., Var(Y) <E(Y)).

Two Hurdle models are commonly found in the literature. They arise when the distribution of $Y_2$ is either Poisson or NB. If $Y_2 \sim \text{Poisson}(\mu)$, the probability function (6.23) becomes

```
$Pr(Y = y) = \begin{cases} \pi_1 & \text{if } y=0 \ (1-\pi_1) \frac{e^{-\mu}\mu^y}{(1-e^{-\mu})\Gamma(y+1)} & \text{if } y \ge 1 \end{cases} \quad (6.27)$
```

$\Gamma(.)$ represents the gamma function. From equations (6.24) and (6.25), the mean and variance of a Poisson Hurdle model turned out to

```
$E(Y) = \frac{1-\pi_1}{1-\pi_2}\mu \quad (6.28)$
```

and

```
$Var(Y) = \frac{1-\pi_1}{1-\pi_2}\mu(\mu+1) - \left(\frac{1-\pi_1}{1-\pi_2}\right)^2\mu^2. \quad (6.29)$
```

Program 6.5 shows the programming statements for plotting the probability functions of a Poisson with parameter $\lambda=3$, and a Poisson Hurdle with parameters $\lambda=3$ and $\pi=0.1$, and again, a Poisson with parameter $\lambda=3$, and a Poisson Hurdle with parameters $\lambda=3$ and $\pi_1=0.025$. The two pairs of plots are depicted in Output 6.5. Note that under the Poisson model the probability of zero is approximately 0.05 (5%). In the first pair, the excess of zeros in the Hurdle model is clearly noticeable—twice as much as that under the Poisson model.

Furthermore, the probabilities associated with the non-zero (1,2,...) in the Hurdle model correspond to those of a Poisson times the factor $\phi = \frac{1-\pi_1}{1-e^{-\mu}} \approx 0.6314$. The second pair of plots

show an interesting characteristic of the Hurdle models: they can accommodate a "deficit" of zeros relative to the Poisson distribution. In this case, the Hurdle model exhibits about half of the zeros allowed by the corresponding Poisson distribution.

More, Jorge, and Nagaraj Neerchal. Overdispersion Models in SAS®. Copyright ©2011, SAS Institute Inc., Cary, North Carolina, USA: ALL RIGHTS RESERVED. For additional SAS resources, visit support.sas.com/publishing.