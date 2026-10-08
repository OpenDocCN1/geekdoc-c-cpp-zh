The trader’s strategy is to delta hedge this liability. They delta hedge at $N$ discrete time steps. So each time step has length $\delta t = \frac{T}{N}$. We label the times at which the trader hedges with integers $i \in \{0, N - 1\}$. So time point $i$ takes place at time $i\delta t$. At time point $i$, the trader will ensure that they hold precisely $\Delta_{i}$ units of stock where $\Delta_{i}$ is the Black–Scholes delta of the call option at time point $i$. Any remaining money is invested in a risk-free account which grows at a fixed interest rate of $r$.

We write $b_{i}$ for the trader’s bank balance at each time point $i$. At time point 0 the trader puts

```
$$ b_{0} = P - \Delta_{0} S_{0} \tag{14.1} $$
```

into their risk-free account and invests the remainder of the principal, $\Delta_{0} S_{0}$ in stock. We can then calculate the bank balance of the trader at subsequent time points $i$ using the difference equation

```
$$ b_{i} = e^{r \delta t} b_{i-1} - (\Delta_{i} - \Delta_{i-1}) S_{i \delta t}. \tag{14.2} $$
```

This equation follows because the money they have in the bank grows at the interest rate $r$ giving rise to the term $e^{r \delta t} b_{i-1}$ representing the amount in the bank before the trader rebalances their portfolio. The trader then needs to rebalance their portfolio to ensure they are holding $\Delta_{i}$ units of stock. This means that they will need to buy $\left(\Delta_{i} - \Delta_{i-1}\right)$ units of stock. This explains the $-\left(\Delta_{i} - \Delta_{i-1}\right) S_{i \delta t}$ term.

At time point $N$, the option reaches maturity. The trader does not delta hedge. Instead they sell off any remaining stock holding and pay off the liability. This tells us that

```
$$ b_{N} = e^{r \delta t} b_{N-1} + \Delta_{N-1} S_{T} - \max\{S - K, 0\}. \tag{14.3} $$
```

This final bank balance represents the profit or loss of the trader. Equations (14.1) to (14.3) have been derived using nothing more complex than the definition of the delta hedging strategy and basic accounting calculations. These calculations are no more complex than the ones you use to understand your own personal bank accounts and shopping purchases.

We can use the difference equations (14.1) to (14.3) to compute the profit and loss of the trader given a set of simulated stock prices. The one additional ingredient we need is an explicit formula for $\Delta_{i}$. By definition, $\Delta = \frac{\partial C}{\partial S}$ where $C$ is the price of the call option and $S$ is the current stock price. This means that one can compute $\Delta$ simply by differentiating the Black–Scholes formula (A.6) for the call price. The result is

```
$$ \Delta = N(d_{1}) \tag{14.4} $$
```

where $N$ and $d_{1}$ are as defined in Equation (A.6). Together the formulae in this section allow us to explicitly calculate the profit or loss of the trader in a given scenario. By generating multiple scenarios