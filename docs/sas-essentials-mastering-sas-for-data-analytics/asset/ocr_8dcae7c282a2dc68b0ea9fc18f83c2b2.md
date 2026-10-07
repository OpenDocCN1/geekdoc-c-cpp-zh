# 312 CHAPTER 13: ANALYSIS OF VARIANCE

The “Going Deeper” section in this chapter describes how to perform posthoc comparisons for a one-way ANOVA.

# 13.1 COMPARING THREE OR MORE MEANS USING ONE-WAY ANALYSIS OF VARIANCE

A one-way ANOVA is an extension of the independent group t-test where there are more than two groups. Assumptions for this test are similar to those for the t-test: Data within groups are normally distributed with equal variances across groups. Another key assumption is that of independent samples. That is, not only the observations within a group represent a random sample, but also there is no matching or pairing of observations among groups. This is analogous to the requirement of independent samples in the two-sample t-test. With the t-test, the ANOVA is robust against moderate departures from the assumptions of normality and equal variance (especially for larger sample sizes). However, the assumption of independence is critical. The hypotheses for the comparison of independent groups are as follows (k is the number of groups):

$H_0: \mu_1 = \mu_2 = ... = \mu_k$: Means of all groups are equal.
HH_a: \mu_i \neq \mu_j$ for some $i \neq j$: At least two means are not equal.

The test used to test these hypotheses is an $F$ with $k-1$ and $N-k$ degrees of freedom, where $N$ is the number of subjects. A $p$-value for the F-test is evidence for rejecting the null hypothesis. In other words, there is evidence that at least one pair of means are not equal. These tests can be performed in SAS using PROC ANOVA. The syntax for the statement is as:

```
PROC ANOVA <options>;
CLASS variable;
MODEL dependentvar = independentvars;
MEANS independentvars / typecomparison <meansoptions>;
```

Table 13.1 lists common options and statements used with PROC ANOVA and PROC GLM. Some options for GLM are only listed (as GLM only). Not every option listed here is illustrated in the chapter’s examples.

The model statement is a key part of the PROC ANOVA procedures. It is similar to the MODEL statement described in the previous chapter for PROC REG. The form of the statement is

```
MODEL dependentvariable=independentvariable;
```

The dependent variable is the quantitative variable of interest (your outcome variable), and the independent variable (one independent variable in the one-way ANOVA case) is the grouping variable for the analysis (the variable listed in the CLASS statement). For example, if you have measured FEV (pulmonary forced expiratory volume) and want to determine if there is a weight difference by group, your model statement would be

```
MODEL FEV=GROUP;
```