Running the following line produces five randomly generated Dunedin temperatures from the X ~ N(22,1.5) distribution:

```
R obs <- rnorm(5,mean=22,sd=1.5)
R obs
[1] 22.92233 23.09505 20.98653 20.10941 22.33888
```

Now, for the sake of example, these five values constitute all the data you have for this particular problem; in other words, you pretend to know that μ_X = 22 and σ_X =1.5. Your guesses of the true values of μ_X and σ_X, denoted x and s, respectively, are therefore as follows:

```
R obs.mean <- mean(obs)
R obs.mean
[1] 21.89044
R obs.sd <- sd(obs)
R obs.sd
[1] 1.294086
```

The estimated standard error can be calculated:

```
R obs.mean.se <- obs.sd/sqrt(5)
R obs.mean.se
[1] 0.5790545
```

Because n = 5 is relatively small, you must assume the values in obs realizations from a normal distribution, in line with the points made for situation 2. This allows you to handle the sampling distribution of X using the t-distribution with 4 degrees of freedom. Recall from Section 16.2.3, though, any t-distribution is typically placed on a standardized scale. For you to find the probability that the mean temperature (in a sample of five days) is not 21.5 based your calculated sample statistics, you must first standardize this value using the rules outlined in Section 16.2.2. Label the corresponding variable as T and the specific value as t_4, stored as the object t4 in R.

```
R t4 <- (21.5-obs.mean)/obs.mean.se
R t4
[1] -0.674206
```

This has placed the value of interest, 21.5, on the standardized scale, making it interpretable with respect to a standard normal distribution, or as is correct in this setting (because you are using the estimate s rather than the unknown σX in calculating the standard error), t4 follows the aforementioned t-distribution with 4 degrees of freedom. The estimated probability is