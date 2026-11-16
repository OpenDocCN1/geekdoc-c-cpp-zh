![](bbox=[0.18, 0.1, 0.8, 0.38])

Figure 2.18: The Laplace probability density function for various values of \(\mu\) and \(b\), chosen such that the mean and variance are the same as in Figure 2.2.

In practical terms, this means that the time one has to wait for an event is not influenced at all by the time one has spent waiting so far. This means the exponential distribution is memoryless, a property it shares with the geometric distribution. The exponential distribution is the continuous equivalent of the geometric distribution which describes the number of attempts of a binary experiment to succeed. Instead of thinking about failures and successes, it is more convenient to think about a change of state. \(\lambda\) gives the rate of change over a unit time interval, and the exponential distribution describes the probability of how much time passes until the states changes. Constant rate of change is a crucial assumption not often satisfied by real-world processes. For example, the rate of emergency calls increases on Friday and Saturday nights and staffing levels need to be adjusted compared to other times. If the rate is constant, it is used in queueing theory. The exponential distribution is inappropriate to model the overall lifetime of organisms or technical devices, where the event of death or failure depends on the lifetime so far.

Using integration by parts, the expectation is given by

```
\mathbb{E}[x] = \int_0^\infty \frac{x}{\beta} \exp\left(-\frac{x}{\beta}\right) dx
= \left[ \frac{x}{\beta} \left( -\beta \exp\left(-\frac{x}{\beta}\right) \right) \right]_0^\infty + \int_0^\infty \exp\left(-\frac{x}{\beta}\right) dx
= \left[ -\beta \exp\left(-\frac{x}{\beta}\right) \right]_0^\infty = \beta.
```

The variance can be calculated similarly and is

```
\text{var}[x] = \beta^2.
```