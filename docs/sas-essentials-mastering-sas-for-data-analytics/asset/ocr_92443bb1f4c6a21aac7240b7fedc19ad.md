# # 11

# ## COMPARING MEANS USING T-TESTS

# LEARNING OBJECTIVES

+   - To understand the use of the one-sample $t$-test using PROC UNIVARIATE and PROC TTEST
- To understand the use of the two-sample $t$-test using PROC TTEST
- To understand the use of the paired $t$-test using PROC MEANS AND PROC TTEST

Experiments where outcome measures are quantitative variables are often analyzed by comparing means. The Student's $t$-test is the most commonly used statistical test for comparing two means or for comparing an observed mean with a known value. If more than two groups are observed, an analysis of variance (ANOVA) is used to compare means across groups (discussed in Chapter 13).

#  11.1 PERFORMING ONE-SAMPLE T-TEST

A one-sample $t$-test is often used to compare an observed mean with a known or "gold standard" value. For example, in a quality control setting, you may be interested in comparing a sample of data to an expected outcome, such as the observed calories of liquid in baby formula against the claim on the label. The purpose of the one-sample $t$-test, in this case, is to determine if there is enough evidence to dispute the claim. In general, for a one-sample $t$-test you obtain a random sample from some population and compare the