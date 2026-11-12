Now, $p(Y = y')$ represents the knowledge we have about how likely the class value y' is, before we even begin. Since that information is known prior to our analysis, we call $p(Y = y')$ the **prior probability**. This prior information is combined with $p(X' | Y = y')$, which represents how the data behave, when the response equals y'. The denominator, $p(X')$, is how the data behave without reference to the response class values, otherwise known as the **marginal probability** of the data.

The result of the formula, $p(Y = y' | X')$, represents the information or idea we have about how likely our class value y' is if we observe the particular predictor variable values X'. Since the information is updated from $P(Y = y')$ after examining the data, we call $p(Y = y' | X')$ the **posterior probability**.

What if we have no prior knowledge about the parameters? In this case, you can use a **noninformative prior**, which says that every class value is equally likely. By using a noninformative prior, your posterior probabilities are based solely on the data.

# 8.3 MAXIMUM A POSTERIORI HYPOTHESIS

How can we use the Bayes Theorem probabilities to classify a record? In our example above, we have three different possible values of y'. For a fixed value of X', we calculate a Bayes Theorem probability for each of the three possible values of Y:

```
p(Y = y_1|X') = \frac{p(X'|Y = y_1) p(Y = y_1)}{p(X')}

p(Y = y_2|X') = \frac{p(X'|Y = y_2) p(Y = y_2)}{p(X')}

p(Y = y_3|X') = \frac{p(X'|Y = y_3) p(Y = y_3)}{p(X')}
```

The **maximum a posteriori hypothesis** tells us to classify the record X' as the value of Y which has the highest posterior probability. In other words, choose the class value of Y that corresponds with the largest of the three posterior probabilities we calculated.

# 8.4 CLASS CONDITIONAL INDEPENDENCE

If we have more than one predictor variable, then the class conditional independence assumption allows us to write $p(X' | Y = y')$ as the product of independent events. For example, say we have two predictor variables $X' = (X_1 = x_1, X_2 = x_2)$. To write $p(X' | Y = y')$, we would write $p(X_1 = x_1 | Y = y') \times p(X_2 = x_2 | Y = y')$. We will see a demonstration of this in the Section 8.5.