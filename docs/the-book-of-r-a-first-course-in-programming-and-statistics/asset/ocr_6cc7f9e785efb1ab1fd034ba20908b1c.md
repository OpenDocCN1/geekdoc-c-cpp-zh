+   - The function should contain a check for the rule of thumb to ensure the validity of the normal distribution in both one- and two-sample settings. If this is violated, the function should still complete but should issue an appropriate warning message (see Section 12.1.1).
- All that need be returned is a list containing the members Z (test statistic), P (appropriate p-value—this can be determined by alternative; for a two-sided test, determining whether Z is positive or not can help), and CI (two-sided CI with conf.level).

+   g. Replicate the two examples in the test of Sections 18.3.1 and 18.3.2 using Z.test; ensure you reach identical results.

+   h. Call Z.test(p1=0.11,n1=10,p0=0.1) to try your warning message in the one-sample setting.

# # 18.4 Testing Categorical Variables

The normal-based Z-test is particular to data that are binary in nature. To statistically test claims regarding more general categorical variables, with more than two distinct levels, you the ubiquitous *chi-squared test*. Pronounced khai, "chi" refers to the Greek symbol $\chi$ and is sometimes noted in shorthand as the $\chi^2$ test.

There are two common variants of the chi-squared test. The first—a chi squared test of distribution, also called *goodness of fit* (GOF) test—is used when assessing the frequencies in the levels of a single categorical variable. The second—a chi-squared test of *independence*—is employed when you're investigating the relationship between frequencies in the levels of two variables.

# ## 18.4.1 Single Categorical Variable

Like the Z-test, the one-dimensional chi-squared test is also concerned with comparing proportions in a setting where there are more than two proportions. A chi-squared test is used when you have $k$ levels (or categories) of a categorical variable and want to hypothesize about their frequent frequencies to find out what of $n$ observations fall into each defined category. In the following examples, it must be assumed that the categories are *mutually exclusive* (in other words, an observation cannot take more than one of the possible categories) and *exhaustive* (in other words, the $k$ categories cover all possible outcomes).

I'll illustrate how hypotheses are constructed and introduce the relevant ideas and methods with the following example. Suppose a researcher in sociology is interested in the dispersion of rates of facial hair in his local city and whether they are uniformly represented in the male population. It defines a categorical variable with three levels: clean shave (1), beard only