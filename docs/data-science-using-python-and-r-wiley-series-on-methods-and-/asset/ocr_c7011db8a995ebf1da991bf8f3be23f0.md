# 8.1 INTRODUCTION TO NAÏVE BAYES

Of course, classification modeling is not restricted to decision trees. Many other classification methods are available, including Naïve Bayes classification. Naïve Bayes classification methods are based on Bayes Theorem, developed by the Reverend Thomas Bayes¹. Bayes Theorem updates our knowledge about the data parameters by combining our previous knowledge (called the prior distribution) with new information obtained from observed data, resulting in updated parameter knowledge (called the posterior distribution).

# 8.2 BAYES THEOREM

Consider a data set made up of two predictors X = X1, X2 and a response variable Y, where the response variable takes one of three possible class values: y1, y2, and y3. Our objective is to identify which of y1, y2, and y3 is the most likely for a particular combination of predictor variable values. Let us call this most likely combination X' = {X1 = x1, X2 = x2}.

We can use Bayes Theorem to identify which class is the most likely for a particular combination of predictor variable values by:

+   1. calculating the posterior probability for each of y1, y2, and y3, for the combination of predictors x1 and x2, and
+   2. selecting the value of y with the highest posterior probability.

Let y' be one of the three potential values of Y. Bayes Theorem tells us:

```
p(Y=y'|X') = \frac{p(X'|Y=y')p(Y=y')}{p(X')} (8.1)
```

> ¹Thomas Bayes, Essay Toward Solving a Problem in the Doctrine of Changes, Philosophical Transactions of the Royal Society of London, 1793.