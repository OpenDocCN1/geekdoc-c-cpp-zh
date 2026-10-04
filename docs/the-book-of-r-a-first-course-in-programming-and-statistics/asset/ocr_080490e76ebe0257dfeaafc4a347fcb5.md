# 19

# ANALYSIS OF VARIANCE

![](bbox=[0.15, 0.42, 0.31, 0.61])

Analysis of variance (ANOVA), in its simplest form, is used to compare multiple means in a test for equivalence. In that sense, it’s a straightforward extension of the hypothesis test comparing two means. There’s a continuous variable from which the means of interest are calculated, and there’s at least one categorical variable that tells you how to define the groups for those means. In this chapter, you’ll explore the ideas surrounding ANOVA and look at comparing means first split by one categorical variable (one-way ANOVA) and then split by multiple categorical variables (multiple-factor ANOVA).

# 19.1 One-Way ANOVA

The simplest version of ANOVA is referred to as one-way or one-factor analysis. Simply put, the one-way ANOVA is used to test two or more means for equality. Those means are split by a categorical group or factor variable. ANOVA is often used to analyze experimental data to assess the impact of an intervention. You might, for example, be interested in comparing the mean weights of the chicks in the built-in chickwts data set, split according to the different food types they were fed.