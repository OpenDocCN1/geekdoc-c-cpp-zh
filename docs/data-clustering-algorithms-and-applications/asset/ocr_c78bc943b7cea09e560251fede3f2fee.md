# Data Clustering: Algorithms and Applications

![](bbox=[0.27, 0.09, 0.73, 0.365])

**Figure 3.4:** For a concave function log(x), the secant line consists of weighted means of the concave function that lies on or below it.

variables with summation often used by integration as appropriate. Note that the summation over the latent variables appears inside the logarithm, which prevents the logarithm from acting directly on the joint distribution, resulting in complicated expressions for the maximum likelihood solution. The essential trick of the EM algorithm is to maximize a *lower bound* on the log-likelihood instead of the log-likelihood.

*Jensen's inequality* is often used to bound the logarithm of a summation of terms. Given $K$ negative numbers $\pi_1, \dots, \pi_K$ that add up to one (i.e., mixing properties), and $K$ arbitrary numbers $x_1, \dots, x_K$, for a concave function $f$, Jensen's inequality can be stated as

```
$f(\sum_{k=1}^K \pi_k x_k) \le \sum_{k=1}^K \pi_k f(x_k)$
```

and the inequality is reversed if $f$ is a convex function, which is

```
$f(\sum_{k=1}^K \pi_k x_k) \ge \sum_{k=1}^K \pi_k f(x_k)$
```

Let us take the logarithm function, a concave function, as an example. As shown in Figure 3.4, for two points $x_1$ and $x_2$, the concave function of the weighted means $\pi x_1 + (1-\pi)x_2$ is larger than the weighted means of the concave function $\pi\log(x_1) + (1-\pi)\log(x_2)$.

We can introduce an arbitrary distribution $q(z_i)$ defined over the latent variables $(\sum_{z_i} q(z_i) = 1, q(z_i) \ge 0)$, and we observe that, for any choice of $q(z_i)$, the following decomposition holds based