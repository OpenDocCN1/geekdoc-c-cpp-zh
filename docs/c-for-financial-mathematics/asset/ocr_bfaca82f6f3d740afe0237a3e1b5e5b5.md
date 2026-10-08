stock price when one can make risk-free investments at a rate of $ r $. This means that a trader who prices derivatives using this model cannot be arbitraged. However, this is only a minimum requirement for a Q-measure model. It is also important to check if it fits market prices for derivatives well. To check this we should compute the risk-neutral prices of put and call options. One simply needs to compute the expected value of the payoff

$\mathrm{max}(\exp(z_t) - K, 0)$

using the formula for $ p(z_t) $ given in Equation (A.3). This is another exercise in integration.

# **Theorem 1. The Black–Scholes Formulae** If one uses the Q-measure geometric Brownian motion model (A.5) to price stock options, then the price of a European call option at time $ 0 $ with maturity $ T $ and strike $ K $ is

$\begin{aligned}C &= N(d_1)S_0 - N(d_2)K\exp(-rT) \end{aligned}\tag{A.6}$

where $ N $ is the cumulative distribution function of the standard normal distribution,

$d_1 = \frac{1}{\sigma\sqrt{T}}\left(\log\left(\frac{S}{K}\right) + \left(r + \frac{\sigma^2}{2}\right)\sqrt{T}\right),$

and

$d_2 = \frac{1}{\sigma\sqrt{T}}\left(\log\left(\frac{S}{K}\right) + \left(r - \frac{\sigma^2}{2}\right)\sqrt{T}\right).$

$\textit{The corresponding formula for a European put option is:}$

$P = N(-d_2)K\exp(-rT) - N(-d_1)S.$\tag{A.7}

To see if our Q-measure model accurately fits market data, we should see if we can find parameter values so that the prices given by the formulae above match real market prices for options. This is left as a rather tricky exercise for you to try out using the C++ skills developed in this book (Exercise 19.4.5). The answer is that our Q model gives a basic crude fit to the market data for options, but a more sophisticated model is needed in practice.

We should emphasise that Black and Scholes used a far more elaborate argument to derive these formulae based on P-measure models in their seminal paper [2]. We have simply assumed that the pricing model takes a particular form and then computed some integrals. We will discuss Black and Scholes' original argument in more detail when we discuss hedging.

# **Tip: Dimensional analysis**

It is conventional to use the year as the unit of time in finance calculations. Often the units are omitted when writing financial formulae. For example, one