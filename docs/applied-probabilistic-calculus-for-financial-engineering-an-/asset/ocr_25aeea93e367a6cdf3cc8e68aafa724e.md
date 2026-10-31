call option. The call option gives the buyer the right to buy 100 shares, since each option contract is for 100 shares.

The seller's position could be hedged by buying 0.85 × 100 = 85 shares. The gain (or loss) on the option position would then tend to be offset by the loss (or gain) on the stock position. If the stock price goes up by $1 (producing a gain of $85 on the shares purchased) the option price would tend to go up by 0.85× $1 = $0.85 (producing a loss of $0.85 × 100 = $85 on the call option written) [Hull, 2000].

# Stock Price Model

Stock prices move randomly because of the efficient market hypothesis. There are different forms of this hypothesis, but all refer to two factors:

+   1) The history of the stock is fully reflected in the current price.
+   2) The markets respond immediately to new information about the stock.

With the previous two assumptions, changes in a stock price follow a Markov process. A Markov process is a stochastic process where only the present value of the variable is relevant for predicting the future. Thus, the stock model states that predictions for the future price of the stock should be unaffected by the price one day, one week, one month, or one year ago.

As stated above, a Markov process is a stochastic process (viz., one based on probabilities). In the real world, stock prices are restricted to discrete values, and changes in the stock prices can only be realized during specified trading hours. Nevertheless, the continuous-variable, continuous-time model proves to be more useful than a discrete model.

Another important observation is the absolute change in the price of a stock is by itself, not a useful quality. For example, an increase of one dollar in a stock is much more significant on a stock worth $10 than a stock worth $1000. The relative change of the price of a stock is the information that is more valuable. The relative change is defined as the change in the price divided by the original price. Now consider the price of a stock S at time t. Consider a small time interval dt during which the price of the underlying asset S changes by an amount dS. The most common model separates the return on the asset, dS/S into two parts. The first part is completely deterministic, and it is usually the risk free interest rate on a Treasury Bill issued by the government.

This part yields a contribution of μdt to dS/S. Here μ is a measure of the average growth rate of the stock, known as the drift, and μ is the assumed risk-free interest rate on a bond, and it may also be represented as a function of S and t. The second part of the model accounts for the random changes in the stock price owing to external effects, such as unanticipated catastrophic news. It may be modeled by a random sample drawn from a normal distribution with mean zero and contributes σdB to dS/S. In this formula σ is the volatility of the stock, which measures the standard deviation of the returns. Like the term μ, σ can be