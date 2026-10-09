where the random variables $X_t$ are independent and normally distributed, with some fixed mean and standard deviation. This model is called the discrete *Bachelier model* after Louis Bachelier, one of the pioneers of financial mathematics. (It is a discrete model because it only models the stock price at discrete time steps $\delta t$.)

The problem with the Bachelier model is that if the stock price is $10 then $1 would be quite a big change in the stock price. Whereas if the stock price is $1000, then $1 would be a relatively small change in the stock price. The Bachelier model assumes the size of the increments are independent of the current stock price and so it doesn't have the correct scaling behaviour. To fix this, we simply assume that the log of the stock price has independent normally distributed increments with a fixed mean and standard deviation. So we write

```
$$\log(S_{t+\delta t}) = \log(S_t) + Y_t \tag{A.1}$$
```

where the $Y_t$ are independent, normally distributed random variables with some fixed mean and standard deviation.

We can now write each $Y_t$ in terms of some other normally distributed random variables $\epsilon_t$ which have mean 0 and standard deviation 1. If $A$ is the mean of each $Y_t$ and $B$ is the standard deviation, we have

```
$$Y_t = A + B\epsilon_t.$$ 
```

Let us suppose there are $N = \frac{1}{\delta t}$ time steps from 0 to 1. Using the formulae for the expectation and variance of a sum of random variables, we can compute the mean and variance of log $S_t$ as follows.

```
$$\mathrm{E}(\log(S_1) - \log(S_0)) = N \mathrm{E}(Y_t) = \frac{A}{\delta t}.$$ 
```

```
$$\mathrm{Var}(\log(S_1) - \log(S_0)) = N \mathrm{Var}(Y_t) = \frac{B^2}{\delta t}.$$ 
```

In finance we use units of one year to measure times. So the first of these formulae says that the log of the stock price grows by $\frac{A}{\delta t}$ on average each year. The second formula can be interpreted similarly in terms of the standard deviation over a year.

Let us write $\bar{\mu}$ for the expected growth in the log of the stock price over a year and $\sigma$ for the variance in the growth of the log of the stock price over a year.

We can then compute $A$ and $B$ in terms of $\bar{\mu}$ and $\sigma$. We have:

```
$$\begin{aligned} A &= \bar{\mu} \delta t \\ B &= \sigma \sqrt{\delta t}. \end{aligned}$$ 
```

This allows us to rewrite our model (A.1) as follows:

```
$$\log(S_{t+\delta t}) = \log(S_t) + \bar{\mu} \delta t + \sigma \sqrt{\delta t} \epsilon_t. \tag{A.2}$$ 
```