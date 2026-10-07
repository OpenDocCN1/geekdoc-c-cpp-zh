
## Lifetime Data Analysis

Therefore

```
$$\frac{\partial \ln(L(\mu, \sigma|t_1, t_2, \dots, t_n))}{\partial \sigma} =-\frac{n}{\sigma} + \frac{1}{\sigma^3}\sum_{i=1}^n(t_i-\mu)^2. \quad (25.3.22)$$
```

Now, take the Equation 25.3.21 and let

```
$$\frac{\partial \ln(L(\mu, \sigma|t_1, t_2, \dots, t_n))}{\partial \mu} =0,$$
```

then,

```
$$\hat{\mu} =\frac{\sum_{i=1}^n t_i}{n} \quad (25.3.23)$$
```

thus

Likewise, take the Equation 25.3.22 and

```
$$\frac{\partial \ln(L(\mu, \sigma|t_1, t_2, \dots, t_n))}{\partial \sigma} =0,$$
```

then,

```
$$-\frac{n}{\sigma}+\frac{1}{\sigma^2}\sum_{i=1}^n(t_i-\mu)^2=0,$$
$$+\frac{n}{\sigma^2}\sum_{i=1}^n(t_i-\mu)^2=0.$$
```

Thus

```
$$\sigma^2=\frac{\sum_{i=1}^n(t_i-\mu)^2}{n} \quad (25.3.24)$$
```

Hence

```
$$\hat{\sigma}=\sqrt{\frac{\sum_{i=1}^n(t_i-\mu)^2}{n}}$$
```

**Example 25.3.9.** Consider the experiment depicted in Example 25.3.5. As described, the failure time of each cell phone is depicted in Columns ($X_i$) of Table 25.17. As already the exploratory analysis did not reject the normal distribution. Applying Equation 25.3.23 and Equation 25.3.24, the normal distribution parameters are estimated:

```
$$\hat{\mu}=\frac{\sum_{i=1}^n t_i}{n}=\frac{20394.39}{100}=2039.44h$$
$$\hat{\sigma}=\sqrt{\frac{\sum_{i=1}^n(t_i-\mu)^2}{n}}=\sqrt{\frac{1740129.24}{100}}=417.16h.$$
```

The goodness of fit tests fails to reject the normal distribution with parameters $\mu=2039.44h$ and $\sigma=417.16h$ to represent the times to failure with 95% degree of confidence.

## Performance, Reliability, and Availability Evaluation of Computational Systems

### Exponential Distribution

Now let us assume an independent set of measures, a sample, $\{t_1, t_2, \dots, t_n\}$, was collected from an exponentially distributed population with true but unknown parameter $\lambda$.

```
$$f(t) = \lambda e^{-\lambda t}, \quad t \ge 0.$$
```

The likelihood function considered to estimate the distribution parameter is represented by joint distribution with a $\hat{\lambda}$ that maximizes likelihood function for the sample $\{t_1, t_2, \dots, t_n\}$. Therefore, as the set of measures of the sample are i.i.d., then

```
$$L(\lambda | t_1, t_2, \dots, t_n) = f(t_1) \times f(t_2) \times \dots \times f(t_n).$$
```

```
$$L(\lambda | t_1, t_2, \dots, t_n) = \lambda e^{-\lambda t_1} \times \lambda e^{-\lambda t_2} \times \dots \times \lambda e^{-\lambda t_n}.$$
```

```
$$L(\lambda | t_1, t_2, \dots, t_n) = \prod_{i=1}^{n} \lambda e^{-\lambda t_i}.$$
```

```
$$L(\lambda | t_1, t_2, \dots, t_n) = \lambda^n e^{-\lambda \sum_{i=1}^{n} t_i}; \quad (25.3.25)$$
```

Now let us take the $\ln(\lambda | t_1, t_2, \dots, t_n)$, then

```
$$\ln(\lambda | t_1, t_2, \dots, t_n) = \ln(\lambda^n e^{-\lambda \sum_{i=1}^{n} t_i}).$$
```

```
$$\ln(\lambda | t_1, t_2, \dots, t_n) = n \ln\lambda - \lambda \sum_{i=1}^{n} t_i.$$ 
``` (Note: The OCR had a sign error here, corrected to minus based on log rules).

```
$$\ln(\lambda | t_1, t_2, \dots, t_n) = n \ln\lambda - \lambda \sum_{i=1}^{n} t_i; \quad (25.3.26)$$
```

Now, take the derivative of $\ln(\lambda | t_1, t_2, \dots, t_n)$ with respect to $\lambda$:

```
$$\frac{\partial}{\partial\lambda}\ln(\lambda | t_1, t_2, \dots, t_n) = \frac{\partial (n \ln\lambda - \lambda \sum_{i=1}^{n} t_i)}{\partial\lambda},$$
```

thus

```
$$\frac{\partial}{\partial\lambda}\ln(\lambda | t_1, t_2, \dots, t_n) = \frac{\partial n \ln\lambda}{\partial\lambda} - \frac{\partial \lambda \sum_{i=1}^{n} t_i}{\partial\lambda},
```

```
$$\frac{\partial}{\partial\lambda}\ln(\lambda | t_1, t_2, \dots, t_n) = \frac{n}{\lambda} - \sum_{i=1}^{n} t_i.$$
```

In order to find the parameter $\lambda$ that maximizes $L(\lambda, t_1, t_2, \dots, t_n)$, set

```
$$\frac{\partial \ln(L(\lambda | t_1, t_2, \dots, t_n))}{\partial \lambda} = 0$$
```

and solve for $\lambda$. Therefore

```
$$\hat{\lambda} = \frac{n}{\sum_{i=1}^n t_i} \quad (25.3.27)$$
```

**Example 25.3.10.** Consider the experiment introduced in Example 25.3.1, in which fifty ($n=50$) routers were observed in an accelerated reliability test. The time to failure of each device recorded in Table 25.10. The exploratory analysis did not rule out the exponential distribution as a possible fit to represent the data. Using Equation 25.3.27 to estimate $\lambda$, we get

```
$$\hat{\lambda} = \frac{50}{\sum_{i=1}^{50} t_i} = 1.054 \times 10^{-3} \text{ h}^{-1}.$$
```

As $D_{cal} = 0.091$ and $D_{critical} = 0.192$, the KS test fails to reject the exponential distribution with $\lambda = 1.054 \times 10^{-3} \text{ h}^{-1}$ to represent the data with 95% degree of confidence.

### Geometric Distribution

Consider a sample $\{x_1, x_2, \dots, x_n\}$ of independent measures collected from a geometrically distributed population with true but unknown parameter $p, 0 < p \le 1$. The geometric distribution is a discrete random variable, the probability mass function (pmf) is

```
$$p(x, p) = p(1-p)^{x-1}, \quad x = 1, 2, 3, \dots$$
```

Thus, the likelihood function is

```
$$L(p | x_1, x_2, \dots, x_n) = \prod_{i=1}^n p(1-p)^{x_i-1}.$$
```

```
$$L(p | x_1, x_2, \dots, x_n) = p^n (1-p)^{\sum_{i=1}^n (x_i-1)}.$$
```

Now, take $\ln(p | x_1, x_2, \dots, x_n)$:

```
$$\ln(p | x_1, x_2, \dots, x_n) = n \ln p + \sum_{i=1}^n (x_i-1) \ln(1-p).$$
```

Now take the derivative of $\ln(p | x_1, x_2, \dots, x_n)$ with respect to $p$:

```
$$\frac{\partial}{\partial p}\ln(p | x_1, x_2, \dots, x_n) = \frac{\partial (n \ln p + \sum_{i=1}^n (x_i-1) \ln(1-p))}{\partial p}$$
```

Let us set

```
$$\frac{\partial}{\partial p}\ln(p | x_1, x_2, \dots, x_n) = 0,$$
```

then

```
$$\frac{n}{p} - \frac{\sum_{i=1}^n (x_i-1)}{1-p} = 0,$$
```

```
$$\hat{p} = \frac{n}{\sum_{i=1}^n x_i} \quad (25.3.28)$$
```

**Example 25.3.11.** Consider a set of electronic gadgets placed under a stress test until failure. For each device, the test procedure is repeated until the device fails. Table 25.21 shows the number of trials before each device $i$ fails.

#### Table 25.21 Number of Trials until Failure

| $i$ | $X_1$ | $X_2$ | $X_3$ | $X_4$ | $X_5$ | $X_6$ | $X_7$ | $X_8$ | $X_9$ | $X_{10}$ | $X_{11}$ | $X_{12}$ |
|---|---|---|---|---|---|---|---|---|---|---|---|
| 1 | 19 | 21 | 3 | 12 | 8 | 10 | 11 | 11 | 8 | 13 | | |
| 2 | 3 | 7 | 14 | 24 | 26 | 1 | 6 | 11 | 1 | 7 | | |
| 3 | 8 | 2 | 6 | 9 | 8 | 8 | 4 | 30 | 3 | 12 | | |
| 4 | 8 | 5 | 5 | 6 | 16 | 3 | 7 | 1 | 9 | | | |
| 5 | 3 | 23 | 20 | 32 | 32 | 23 | 1 | 5 | 23 | 7 | | |
| 6 | 7 | 9 | 3 | 27 | 2 | 6 | 4 | 6 | 14 | | | |
| 7 | 8 | 11 | 4 | 6 | 49 | 10 | 10 | 10 | 8 | | | |
| 8 | 2 | 18 | 16 | 18 | 3 | 8 | 4 | 26 | 8 | 15 | | |
| 9 | 3 | 2 | 1 | 4 | 3 | 9 | 15 | | | | | |
| 10| | | | | | | | | | | | |

### Poisson Distribution

A Poisson distribution specifies a random variable representing the probability of a given number of events taking place in a defined time interval. Thus, assume a sample $\{x_1, x_2, \dots, x_n\}$ of independent measures, collected from a Poisson distributed population with true but unknown parameters $\lambda$. The pmf of a random variable is

```
$$p(x, \lambda) = \frac{\lambda^x e^{-\lambda}}{x!}$$
```
