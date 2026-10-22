# Output 5.7  Effect of x on the Probability of Being in Each of the Three Categories

![](bbox=[0.196, 0.166, 0.845, 0.532])

What’s going on here? The diagram in Figure 5.1 helps explain this situation. The structure of the model is such that increases in x tend to move individuals from category 2 to category 3. But increases in x also tend to move individuals from category 1 to category 2. When x is very low, most of the cases are in category 1, so most of the movement is from 1 to 2 and the proportion of cases in 2 goes up. Eventually, however, there are few cases left in 1 so most of the movement is from 2 to 3, and the proportion remaining in 2 declines.

# Figure 5.1  Movement of Individuals as x Increases

![](bbox=[0.257, 0.724, 0.548, 0.799])

The upshot of this phenomenon is that multinomial logit coefficients must always be interpreted as effects on contrasts between pairs of categories, never on the probability of being in a particular category.