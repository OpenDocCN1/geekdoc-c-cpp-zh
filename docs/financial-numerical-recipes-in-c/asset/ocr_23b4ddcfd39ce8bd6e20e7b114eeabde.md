![](bbox=[0.283, 0.023, 0.715, 0.246])

which has the same time series properties as a (continuous time) process with the same mean and volatility? There is actually any number of ways of constructing this, hence one uses one degree of freedom on imposing that the nodes *reconnect*, by imposing \(u = \frac{1}{d}\).

(To value an option using this approach, we specify the number \(n\) of periods to split the time to maturity \((T - t)\) into, and then calculate the option using a binomial tree with that number of steps.

Given \(S, X, r, \sigma, T\) and the number of periods \(n\), calculate

```
\(\Delta t = \frac{T - t}{n}\)
\(u = e^{\sigma \sqrt{\Delta t}}\)
\(d = e^{-\sigma \sqrt{\Delta t}}\)
```

We also redefine the “risk neutral probabilities”

```
\(R = e^{r \Delta t}\)
\(q = \frac{R - d}{u - d}\)
```

To find the option price, will “roll backwards.” At node \(t\), calculate the call price as a function of the two possible outcomes at time \(t + 1\). For example, if there is one step,

![](bbox=[0.3, 0.663, 0.7, 0.783])

find the call price at time 0 as

```
\(C_0 = e^{-r\tau}(qC_u + (1 - q)C_d)\)
```

With more periods one will “roll backwards” as discussed in chapter 8

# 12.2 Pricing of options in the Black Scholes setting

Consider options on underlying securities not paying dividend.