# Display 3.24 (continued)

Statistics for Table of conc by cbrood3
Statistic	DF	Value	Prob
Chi-Square	4	44.7552	<.0001
Likelihood Ratio Chi-Square	4	46.1891	<.0001
Mantel-Haenszel Chi-Square	1	24.5782	<.0001
Phi Coefficient		0.9461
Contingency Coefficient		0.6873
Cramer's V		0.9461
WARNING: 50% of the cells have expected counts less than 5. Chi-Square may not be a valid test.
Fisher's Exact Test
Table Probability (P)	2.677E-10
Pr <= P	5.354E-09
Cochran-Armitage Trend Test
Statistic (Z)	5.0080
One-sided Pr > Z	<.0001
Two-sided Pr > |Z|	<.0001
Sample Size = 50

The probability of producing young in the third brood appears to decrease in the highest nitrophen concentration. For more details about the statistical tests in this example, see standard categorical data references (e.g., Agresti 2002). Categorical data analysis methods in SAS are nicely summarized by Stokes et al. (2009).

# 3.10 Summarizing Numeric Variables

If you were stuck on a desert island with access to only one SAS procedure, PROC UNIVARIATE might be your choice (assuming you have an interest in characterizing a numeric variable while stranded on a desert island). This procedure can generate descriptive statistics of location (means, medians, percentiles) and spread (standard deviation, variance, range, interquartile range). It can identify extreme values in the data set. In addition, it can produce simple graphics including histograms, normal quantile plots, stemplots, box plots, etc. The following programming statements produce a