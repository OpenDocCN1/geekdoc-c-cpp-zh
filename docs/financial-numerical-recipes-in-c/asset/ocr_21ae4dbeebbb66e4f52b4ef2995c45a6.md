# 8.3 Multiperiod binomial pricing

Of course, an assumption of only two possible future states next period is somewhat unrealistic, but if we iterate this assumption, and assume that every date, there are only two possible outcomes next date, but then, for each of these two outcomes, there is two new outcomes, as illustrated in the next figure:

![](bbox=[0.25, 0.12, 0.75, 0.35])

Iterating this idea a few times more, the number of different terminal states increases markedly, and we get closer to a realistic distribution of future prices of the underlying at the terminal date. Note that a crucial assumption to get a picture like this is that the factors u and d are the same on each date.

![](bbox=[0.25, 0.45, 0.75, 0.7])

Pricing in a setting like this is done by working backwards, starting at the terminal date. Here we know all the possible values of the underlying security. For each of these, we calculate the payoffs from the derivative, and find what the set of possible derivative prices is one period before. Given these, we can find the option price one period before this again, and so on. Working ones way down to the root of the tree, the option price is found as the derivative price in the first node.

For example, suppose we have two periods, and price a two period call option with exercise price K.