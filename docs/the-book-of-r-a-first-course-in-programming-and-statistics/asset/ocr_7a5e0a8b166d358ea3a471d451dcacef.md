Revisit the ubiquitous mtcars data frame from the MASS package.
j. In Section 22.2.4, you used stepwise AIC selection to model mean MPG. The selected model included a main effect for qsec. Rerun the same AIC selection process, but this time, do it in terms of GPM=1/MPG. Does this change the complexity of the final model?

# 22.2.5 Other Selection Algorithms

Any model selection algorithm will always aim to quantitatively define parsimony and suggest a model that optimizes that definition in light of the available data. There are alternatives to AIC, such as the corrected AIC (AICc) or the Bayesian Information Criterion (BIC), both of which impose heavier penalties on complexity than the default AIC in (22.3).

Sometimes it’s tempting to simply monitor R², the coefficient of determination, for a series of models. However, as mentioned in Section 22.2.1, this on its own is inadequate for choosing between models since it doesn’t penalize complexity and will generally always increase as you continue to add predictors, whether they have a statistically significant impact or not. The adjusted R² statistic, denoted R̃² and reported as Adjusted R-squared in summary, is a simple transformation of the original R² that does incorporate a penalty for complexity relative to the sample size n; calculated as

```
R̃² = 1 - (1 - R²)(n - 1) / (n - p - 1)
```

where p is the number of predictor terms (excluding the intercept). The algorithms based on tests and criteria are always preferable (since interpretation of R² can be difficult), but monitoring R̃² can be useful as a quick check between nested models—a higher value points to a preferred model.

For further reading, Chapter 8 of Faraway (2005) provides some excellent commentary on the guideline-only nature of both test- and criterion-based model selection procedures. Regardless of which approach you employ, always remember that any final model reached by using these algorithms should still be subject to scrutiny.

# 22.3 Residual Diagnostics

In previous chapters, you examined the practical aspects of multiple linear regression models, such as fitting and interpreting, dummy coding, transforming, and so on, but you haven’t yet looked at methods that are essential for determining the validity of your model. The final part of this chapter will introduce you to model diagnostics, the primary goal of which is to ensure that your regression model is valid and accurately represents the relationships in your data. For this, I’ll return focus to the theoretical assumptions underpinning the multiple linear regression model that were noted early in Section 21.2.1.