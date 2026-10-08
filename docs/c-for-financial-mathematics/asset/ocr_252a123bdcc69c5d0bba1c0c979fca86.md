![](bbox=[0.25, 0.07, 0.77, 0.25])

**FIGURE A.2:** The payoff of a put option.

$S_{T}-K$. On the other hand, if at time $T$ the stock price is less than $K$, then it doesn’t make sense to buy the stock for more than the market price. So in this case, they don’t exercise the option and so their wealth remains unchanged. Taking both possibilities into account, one sees that they will end up making the amount

$\operatorname{max}\{S_{T}-K, 0\}.$

The word European refers to the fact that the owner of the stock is only allowed to exercise the stock at the maturity time $T$. When derivatives were first traded, this was the convention for option contracts in European markets. In American markets the convention was that one could choose whether or not to exercise the option at any time up to maturity. Since an American option gives you a little more choice than a European option, American option contracts will be at least as expensive as European options.

These days the typical market conventions are not segregated so much by continent. Typically, options on a single stock are American and options on an index of stocks are European. We will mostly be interested in European options in this book as they are easier to price. For this reason we will sometimes omit the word European and just talk about put and call options.

There really are no rules on what a derivatives contract *can* be. If you can invent a contract and find someone who wants to buy it off you, you have just invented a new kind of derivative. You will probably also want to think up a trading strategy for your new derivative so that you don’t go bankrupt! Coming up with interesting new financial contracts is the role of a *structurer*. A structurer works within a bank to devise novel contracts that the bank believes they can hedge successfully and which the bank’s customers will consider an attractive tool for managing their risks and so be willing to buy.

Here are some other derivatives contracts that we will consider in this book. It’s a lot of terminology to take in, but none of the ideas are complicated.

+   *   An Asian option with maturity $T$ and strike $K$. The payoff is determined by taking
    $\operatorname{max} \operatorname{avg}(S)-K$