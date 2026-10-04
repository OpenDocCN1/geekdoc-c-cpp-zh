# 16.2.2 Normal

The normal distribution is one of the most well-known and commonly applied probability distributions in modeling continuous random variables. Characterized by a distinctive “bell-shaped” curve, it's also referred to as the Gaussian distribution.

For a continuous random variable $-\infty < X < \infty$, the normal density function $f$ is

```
f(x) = \frac{1}{\sigma\sqrt{2\pi}} \exp\left{\nfrac{(x-\mu)^2}{2\sigma^2}\}\right\} (16.6)
```

$\mu$ and $\sigma$ are parameters of the distribution, $\pi$ is the familiar geometric value $3.1415...$, and $\exp[\cdot]$ is the exponential function (refer to Section 2.1.2). The notation

$X \sim N(\mu,\sigma)$

is used to indicate that “X follows a normal distribution with mean $\mu$ and standard deviation $\sigma$.$

The following are the key points to remember:

+   * Theoretically, X can take any value from $-\infty$ to $\infty$.
* As hinted earlier, the parameters $\mu$ and $\sigma$ directly describe the mean and the standard deviation of the distribution, with the square of the latter, $\sigma^2$, being the variance.
* In practice, the mean parameter is finite $-\infty < \mu < \infty$, and the standard deviation is strictly positive and $0 < \sigma < \infty$.
* If you have a random variable $X \sim N(\mu,\sigma)$, then you can create a new random variable $Z = (X-\mu)/\sigma$, which makes $Z \sim N(0,1)$. This is known as standardization of $X$.

The two parameters noted earlier fully define a particular normal distribution. They are always symmetric, unimodal, and centered on the mean $\mu$, and they have a degree of “spread” defined using the standard deviation $\sigma$.

The top image of Figure 16-6 provides the density functions for four normal distributions. You can see that altering the mean results in a translation, where the center of the distribution is simply shifted to the specific value of $\mu$. The effect of a smaller standard deviation is to reduce the spread, resulting in a taller, skinnier appearance of the density. Increasing $\sigma$ flattens the density around the mean.

The bottom image zooms in on the N(0,1) distribution when you have a normal density centered on $\mu=0$ and with a standard deviation of $\sigma=1$. This distribution, known as the standard normal, is frequently used as a standard reference to compare normally distributed random variables with one another on the same scale of probabilities. It’s common practice to scale, or standardize, some variable $X \sim N(\mu_X,\sigma_X)$ to a new random variable $Z$ that $Z \sim N(0,1)$ (you’ll see this practiced in Chapter 18). Vertical lines in the plot show plus or minus two, and three times the standard deviation away from the mean of zero. This serves to highlight the fact that for any