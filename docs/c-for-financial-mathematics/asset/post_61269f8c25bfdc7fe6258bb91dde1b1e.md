
![](img/c60a618fcc2a2ed9d1e8d96a1b4157ff_391_0.png)

FIGURE A.3: A “strangle” consisting of a put and a call option.

that this figure shows the total profit and not just the payoff of the options because we have taken into account the cost of buying the options.

If the stock price stays the same, the speculator will lose money (the amount spent buying the options), but if the stock price either moves up sufficiently or down sufficiently, the speculator will make money. By trading in options, the speculator is able to formulate a bet that closely matches their beliefs. It is much easier to predict when a stock will move significantly than to predict whether it will go up or down, so this type of strategy is a powerful tool for a trader. This particular strategy is called a “strangle”.

Notice that by buying and selling combinations of puts and calls with different strikes, it is possible to approximate pretty much any shape of payoff curve you would like. Figure A.3 is just one simple example. This explains why simple put and call options are so popular; they can be used to construct very precisely targeted bets on the future of the stock market.

Another important point is that although the word bet seems rather negative, bets can be used for insurance. Derivatives are often used for insurance.

**Example 2:** Consider a pension investor who is approaching retirement. It is unlikely they will want all of their wealth to be invested in the stock market as it is too risky. On the other hand, they wouldn’t want all of their wealth locked up in government bonds as the interest rate is too low. One obvious solution is to invest some money in stocks and some in bonds. The problem with this approach is that it turns out you have to frequently rebalance your portfolio between stocks and bonds if you wish to invest optimally (this question was famously studied by Merton [12]). Frequently rebalancing your portfolio requires active management of your pension. In addition, rebalancing a portfolio incurs significant transaction costs. An alternative approach is to use derivatives to create a portfolio that has a risk somewhere between stocks and bonds. If you assume that puts and call options are available at all possible strikes, then it turns out that you can replicate Merton’s strategy by trading in derivatives at time 0 and then simply waiting till the maturity.

Importantly, when it comes to a practical implementation of these strategies, buying derivatives can allow you to reduce the transaction costs and largely eliminate the need for active management.

## A.3 Risk-neutral pricing

Banks wish to provide the financial products desired by their customers. To make their customers happy and to ensure that there is a liquid market in their financial products, banks are typically willing to either buy or sell the same financial product. Due to the intense competition in the market, banks can only charge slightly different amounts for buying and selling the same product. Of course, they do always charge slightly different amounts for buying and selling. This difference reflects the requirement of the bank to make a profit. This willingness to both buy and sell at similar prices is perhaps the most immediately apparent difference between banks and speculators.

Banks behave very much like bookmakers in that they are willing to take either side of a bet. As a result they price their financial products in a very similar way to bookmakers.

One very interesting fact about the odds offered by bookmakers is that these odds do not necessarily reflect the chance of a particular event happening. Instead, bookmaker’s odds tell you more about which bets are selling well and which are selling badly.

As an example, many people are willing to bet on their favourite football team for emotional reasons rather than because of any serious belief that they will win. They bet on what they *want* to happen rather than on what they think *will* happen. Similarly, many people don’t like to bet on a firm favourite. This is because even if their horse wins they might not make enough money to make it exciting. Most people bet for entertainment as much as profit. A 1% return on an investment in a day is, from a financial markets point of view, an excellent rate of return. However, if you are at a race track and bet £100 on the only four-legged horse running a particular race in the hope of making £1 profit, then you probably won’t find your watching the race to be particularly exciting.

As a result, bookmakers do not trouble themselves with carefully studying the physiques and pedigrees of horses when they choose what odds to offer. Instead they simply match up the bets between different parties in such a way that they are guaranteed to make a profit. This profit comes from the small difference in the price offered by bookmakers when taking the different sides in any particular bet.

The derivatives desks of banks operate in almost exactly the same way.

Derivatives traders are largely indifferent to whether a stock goes up or down in much the same way as bookmakers are indifferent as to which horse wins a race.

Since the margin between the buy and sell prices of both bookmakers and banks are rather small, they find it a useful approximation to think of themselves as offering a single price at which they will either buy or sell. In practice, both banks and bookmakers can first choose a self-consistent set of prices at which they are willing to either buy or sell. Then when a customer asks to buy a particular product, they quote a slightly higher price, and a slightly lower price when their customer wishes to sell. In this way, they expect to make a small profit from each event that their customers bet on.

It is vital that the prices offered by the bank or the bookmaker are self-consistent in some sense. What they don’t want to happen is for a customer to be able to place a complex bet that the customer knows they are guaranteed to win. Such a bet is called an arbitrage.

To ensure that such a bet is impossible, bookmakers price their bets *as if* the cost of a bet was determined by the expected payoff in some probability model. As one knows, the odds offered by bookmakers *look* as though they are derived from the probability of each horse winning. Yet as we have discussed, those prices are derived by considering the market for bets and not by considering the real chance of those events occurring.

Derivatives traders work in exactly the same way. One slight difference is that derivatives traders offer bets over longer time periods than bookmakers, so they factor charging and paying interest into their calculations.

The probability model used by bookmakers and derivatives traders is called a $\mathbb{Q}$-measure model. This is a model that looks exactly like an ordinary probability model, but the values it computes are measures of price and not measures of the chance of an event happening. A classical probability model that attempts to measure the chance of an event taking place is called a $\mathbb{P}$-measure model.

If the interest rate for a risk-free bank account is at a constant level *r* so that a principal *P* invested is worth *Pe* ${}^{rt}$ at time *t*, then the amount charged by a derivatives trader for an option that pays *f*(*S* ${}_{T}$) at time *T* is given by the following formula:

Risk neutral price $: = e^{-rT} \mathbb{E}_{\mathbb{Q}}(f(S_T))$.

Here $\mathbb{E}_{\mathbb{Q}}$ denotes the expectation taken using the $\mathbb{Q}$-measure model. The factor *e* ${}^{-rT}$ is a discount factor to take account of interest payments. The motivation for calling this price the “risk neutral price” will be explained shortly.

Notice that if you invest an initial sum *P* in the risk-free bank account, then the payoff will be *Pe* ${}^{rT}$ and is independent of the stock price. Hence, its expectation in the $\mathbb{Q}$-measure model will also be *Pe* ${}^{rT}$. So the “risk neutral” valuation of a bank account in which *P* is invested at time 0 is:

*e* ${}^{-rT}\ \mathbb{E}_{\mathbb{Q}}(Pe^{rT}) = P$.
