
## Chapter 4 Likelihood Models for Overdispersed Binomial Responses 79

$$Var(T) = mn(1-\pi)[1+\rho(m-1)]$$

Note that the unconditional variance of T is written as sum of the expected value of the conditional variance and variance of the conditional expectation. Consequently, one can expect the unconditional variance to be larger than the conditional variance of T. Thus, appropriate prior on P would lead to a model with overdispersion. In particular, when the Beta prior is chosen, the Beta-binomial distribution will be used. Therefore, one may consider the Beta-binomial to be a general way (not tied to a specific mechanism) of modeling overdispersion. As stated in Chapter 1, the last two equations represent a common characterization of overdispersion relative to the Binomial distribution. This formulation clearly allows a Bayesian framework. The distribution $f(P)$ can be viewed as a prior distribution on the success probability P of the Binomial random variable $T$.

Under the prior distribution $f(P)$, for any $t = 0,1,\dots,m$, it follows that

$$Pr(T=t) = E_f[Pr(T=t)] = \int \binom{m}{t}P^t(1-P)^{m-t}f(P)dP$$

A distribution of the form (4.6) is said to be a mixture, with the mixing distribution. If $f(P)$ is continuous, the unconditional distribution of T is an infinite mixture. If the prior $f(P)$ is discrete and finite, the integral symbol in (4.6) changes to a finite sum, and the resulting distribution is a finite mixture. Each of the overdispersion models discussed in this chapter can be realized by choosing mixing distributions. We will first present the well-known Beta-binomial distribution, originally used by Skellam (1948), which corresponds to a choice of Beta as the mixing prior. The second model, called the Random clumped Binomial distribution, proposed by Morel and Nagaraj (1993), is a mixture of two Binomials and corresponds to choosing a discrete distribution as the prior. Two additional distributions will be considered in this chapter. We first discuss the Beta-binomial distribution.

Let $f(P)$ be the density function of a Beta distribution with parameters $a=C\pi$ and $b=C(1-\pi)$,

$$f(P)=\frac{\Gamma(a+b)}{\Gamma(a)\Gamma(b)}P^{a-1}(1-P)^{b-1} = \frac{\Gamma(C)}{\Gamma(C\pi)\Gamma(C(1-\pi))}P^{C\pi-1}(1-P)^{C(1-\pi)-1}$$

where $\Gamma(\cdot)$ is a gamma function and $C=(1-\rho^2)/\rho^2$, $\rho$ the overdispersion parameter. Under the Beta distribution,

$$E_r(P) = \frac{a}{a+b} = \pi$$

and

$$V_r(P) = \frac{ab}{(a+b+1)(a+b)} = \rho^2\pi(1-\rho),$$

so the first two moments satisfy equations (4.1) and (4.3). If $P\sim \text{Binomial}(\pi;m)$ and $P\sim \text{Beta}\{C,C(1-\rho)\}$, then it can be the probability function of the unconditional distribution of T

$$Pr(T=t) = \frac{\binom{m}{t} \frac{\Gamma(t+C)}{\Gamma(m+C)} \frac{\Gamma\{m-t+C(1-\pi)\}}{\Gamma(C)\Gamma\{C(1-\pi)\}}, \quad t=0,1,\dots,m,\quad 4.8$$

where, as before, $C=(1-\rho^2)/\rho^2$. The probability function of equation (4.4) defines the Binomial distribution with parameters $\pi$, $\rho$ and $m$, and denoted as Beta-binomial($\pi,\rho;m$). The density function (4.7) is the conjugate prior of Binomial. This makes derivation of (4.8) relatively straightforward. Since the first two moments of the Beta distribution satisfy equations (4.1) and (4.3), the first three moments of the Beta-binomial are as equations (4.4) and (4.5), then $E(T)=m\pi$ and $Var(T)=m\pi(1-\pi)\{1+\rho^2(m-1)\}$. In Section 4.10 we provide a SAS program for generating data from the Beta-binomial distribution for any given configuration of $\pi$, $\rho$ and $m$.

## 4.3 The Random-clumped Binomial Distribution

The Random clumped Binomial distribution results from an effort to model meaningfully the physical mechanism behind extra variation. It was informally introduced in Section 1.5 of Chapter 1. We provide a formal derivation here.

Let $Y_1, Y_2,\dots,Y_m$ be independent and identically distributed Bernoulli($\pi$) random variables. For each $i$, $i=1,\dots,m$, define $Y_i$ as $Y$ with probability $\rho$, or as $Y_i^0$ with probability $(1-\rho)$, $0<\rho<1$. $Y_i$ can be represented as

$$Y_i = Y I(\rho) + Y_i^0 I(1-\rho), \quad i=1,\dots,m,\quad 4.9$$

## Chapter 4 Likelihood Models for Overdispersed Binomial Responses 93

where $I(\cdot)$ is an indicator function. In terms of $T = \sum Y_i$, it can be shown that for $m$ independent units

$$Pr(T=t) = \pi \binom{m}{t}(\rho\pi)^t(1-\rho\pi)^{m-t} + (1-\pi) \binom{m}{t}((1-\rho)\pi)^t(1-(1-\rho)\pi)^{m-t}, \quad t=0,1,\dots,m,\quad 4.10$$

This is a mixture of two Binomial distributions. As pointed out in the previous section, overdispersed binomial distributions might arise by placing the appropriate prior on the probability of success P of a Binomial distribution. The Beta-binomial distribution is one example where the prior placed on P is the Beta distribution. The distribution given in (4.11) was proposed by Morel and Nagaraj (1993) for modeling overdispersion where the unconditional distribution of the total number of successes T is obtained from placing on P a two-point prior on the points $P_1 = (1-\rho)\pi$ and $P_2 = \rhopi$, with probabilities $\pi$ and $(1-\pi)$, respectively. If T has the distribution given by equation (4.11), it will be denoted as $nT \sim \text{Random-clumped Binomial}(\pi, \rho;m)$.

## 82 Overdispersion Models in SAS

**Figure 4.1:** Two possible outcomes for a cluster of size m=7 under the Random clumped Binomial distribution. Some units provide identical responses, either “1,” as in (a), or “0,” as in (b).

![](img/fa69b64c17ad451eb7eb4d8d92f5fb_94_0.png)
