9.3.5. To compute the delta, $\Delta$, of an option by Monte Carlo, you can use the following algorithm.

+   * Choose a small value for $h$, say $h = S_0 \times 10^{-6}$.
* Generate $N$ stock price paths.
* Use the Monte Carlo method to compute the price of the option when the initial stock price is taken to be $S_0 + h$.
* Use the Monte Carlo method *with the same price paths* to compute the price of the option when the initial stock price is taken to be $S_0 - h$.
* Estimate the delta using the central difference estimate for the derivative

```
$f'(x) \approx \frac{f(x + h) - f(x - h)}{2h}.$
```

Compute the delta of a call option using this algorithm and write a test for your calculation. You will need to modify the class BlackScholesModel a little to implement this.

Explain why it is essential to use the same random numbers in the calculation of the stock prices.

9.3.6. You can use the central limit theorem to estimate the error in our Monte Carlo estimate. In the Monte Carlo method we have generated a sample of $N$ discounted payoffs and taken the mean to compute an estimate for the true expectation. By the central limit theorem, this sample mean is normally distributed about the true expectation with standard deviation $s N^{-1.2}$ where $s$ is the standard deviation of the discounted payoff. We can estimate $s$ by taking the standard deviation of our sample. Use this to compute a 95% confidence interval for the Monte Carlo price.

9.3.7. There are numerous variance reduction techniques that can be used to improve Monte Carlo calculations. One approach is called antithetic sampling. We first simulate $N$ stock price paths using our Q-measure model Equation (A.4). We recall the formula

```
$\log(S_{t + \delta t}) = \log(S_t) + \left(\mu - \frac{1}{2}\sigma^2\right)\delta t + \sigma(\delta t)^{\frac{1}{2}}\epsilon_t.$
```

We then simulate $N$ further stock price paths using the same random values $\epsilon_t$ but now using the formula

```
$\log(S_{t + \delta t}) = \log(S_t) + \left(\mu - \frac{1}{2}\sigma^2\right)\delta t - \sigma(\delta t)^{\frac{1}{2}}\epsilon_t.$
```

We can compute an estimate for the risk-neutral price by computing the discounted average payoff for all $2N$ paths. It turns out that for many options this gives a more accurate answer than one obtains by simulating $2N$ independent stock paths. Implement antithetic sampling to price a call option.

You should consult the literature on Monte Carlo methods for more information on this and other variance reduction techniques.