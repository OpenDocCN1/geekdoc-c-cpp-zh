# 2. Negative binomial distribution

Negative binomial distribution (NBD) is defined by the probability of getting k successes until r failures occur, given by the following expression:

```
P(X = k) = C_{k}^{r+k-1} p^{k} (1 - p)^{r}    (11.4)
```

where n is the number of trials, p is the probability of success (same for each trial), k is the number of successes observed in n trials, and r is the number of failures.

```
Mean = r(1 - p) / p    (11.5)
```

```
Variance = r(1 - p) / p²    (11.6)
```

If k remains as an integer, the distribution is sometimes known as the Pascal distribution. Many engineering problems are elegantly handled with NBD.

In sampling, if the proportion of individuals possessing a certain characteristic is p and we sample until we see r such individuals, then the number of individuals sampled is a negative binomial random variable.

The NBD is one of the most useful probability distributions. It is used to construct models in many fields: biology, ecology, entomology, and information sciences [2].

# Example 11.2: NBD of Right First-Time Delivery

# QUESTION

In a network sensor manufacturing division, the right first-time rate is 0.6. The company wants to deliver 10 sensors to a mission critical application and prefers to ship after choosing from the right first-time lot. What is the probability of delivering 10 right sensors produced for the first time if the production batch size is 12? Plot the negative binomial probability distribution function associated with this problem. Calculate the mean and variance of the distribution.

# ANSWER

It may be seen that data can be represented in Equation 11.4 with the following parameters:

+   - r = 10 number of successes
+   - p = 0.6 probability of success
+   - k = n - 10 number of failures
+   - n = production batch size, 10, 11, ...

We can use the Excel function NEGBINOM.DIST to generate the NBD and plot the graph, as shown in Figure 11.2.