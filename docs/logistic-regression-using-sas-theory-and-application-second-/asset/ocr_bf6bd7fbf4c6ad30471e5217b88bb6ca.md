the model we’ve been examining. Four measures of association are shown in the right-hand column. The left-hand column gives the intermediate calculations on which those four statistics are based.

# Output 3.16  Ordinal Measures of Association from PROC LOGISTIC

| Association of Predicted Probabilities and Observed Responses |  |  |  |
|---|---:|---|---:|
| Percent Concordant | 88.3 | Somers' D | 0.800 |
| Percent Discordant | 8.4 | Gamma | 0.827 |
| Percent Tied | 3.3 | Tau-a | 0.361 |
| Pairs | 4850 | c | 0.900 |

Here’s how the measures are calculated. For the 147 observations in the sample, there are 147(146)/2 = 10731 different ways to pair them up (without pairing an observation with itself). Of these, 5881 pairs have either both 1’s on the dependent variable or both 0’s. We ignore these, leaving 4850 pairs in which one case has a 1 and the other case has a 0. For each pair, we ask the question, “Does the case with a 1 have a higher predicted value (based on the model) than the case with a 0?” If the answer is yes, we call that pair concordant. If no, the pair is discordant. If the two cases have the same predicted value, we call it a tie. Let C be the number of concordant pairs, D the number of discordant pairs, T the number of ties, and N the total number of pairs (before eliminating any). The four measures of association are then defined as follows:

$$\mathrm{Tau\text{-}a}=\frac{C-D}{N}$$

$$\mathrm{Gamma}=\frac{C-D}{C+D}$$

$$\mathrm{Somer's\ D}=\frac{C-D}{C+D+T}$$

$$c=.5\,(1+\mathrm{Somer's\ D})$$

All four measures vary between 0 and 1, with large values corresponding to stronger associations between the predicted and observed values. Of the four statistics, Tau-a tends to be closest to the generalized $R^2$. On the other hand, the $c$ statistic has become very popular