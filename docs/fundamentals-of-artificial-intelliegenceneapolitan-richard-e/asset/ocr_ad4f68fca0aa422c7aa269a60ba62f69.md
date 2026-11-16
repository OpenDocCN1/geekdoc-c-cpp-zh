have added the conditional probabilities of the Expert node to that diagram. (Recall that Netica does not show conditional probabilities.) Notice that we can obtain the EVPI directly from the values listed at decision node E in the influence diagram in Figure 8.41. That is,

```
EVPI = E(consult) – E(do not consult)
= $1345 – $1190 = $155.
```

# 8.7.2 Expected Value of Imperfect Information

Real experts and tests ordinarily are not perfect. Rather, they are only able to give estimates that are often correct. Let’s say we have a financial analyst who has been predicting market activity for 30 years and has had the following results:

+   1. When the market went up, the analyst said it would go up 80% of the time, would be flat 10% of the time, and would go down 10% of the time.
+   2. When the market was flat, the analyst said it would go up 20% of the time, would be flat 70% of the time, and would go down 10% of the time.
+   3. When the market went down, the analyst said it would go up 20% of the time, would be flat 20% of the time, and would go down 60% of the time.

We therefore estimate the following conditional probabilities for this expert:

```
P(Expert = says up | Market = up) = .8
P(Expert = says flat | Market = up) = .1
P(Expert = says down | Market = up) = .1
P(Expert = says up | Market = flat) = .2
P(Expert = says flat | Market = flat) = .7
P(Expert = says down | Market = flat) = .1
P(Expert = says up | Market = down) = .2
P(Expert = says flat | Market = down) = .2
P(Expert = says down | Market = down) = .6.
```

Figure 8.42 shows the influence diagram in Figure 8.40 with the additional decision alternative that we can consult this imperfect expert. We also show the conditional probabilities of the Expert node in that diagram. The increased expected value we realize by consulting such an expert is called the **expected value of imperfect information (EVII)**. It is given by

```
EVII = E(consult) – E(do not consult)
= $1261.50 – $1190 = $71.50.
```

This is the most we should pay for this expert’s information.