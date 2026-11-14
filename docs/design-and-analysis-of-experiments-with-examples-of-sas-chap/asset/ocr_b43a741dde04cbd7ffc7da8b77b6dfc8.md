# 5.5.3 Determining Sample Sizes for Two-Factor Sampling Experiments

In a two-factor sampling experiment, there are three sample sizes to be considered. First the number of levels of factor A, a, second the number of levels of factor B, b, and finally the number of replicates within each cell, r. The degrees of freedom for the replicate mean square is ab(r - 1), by replacing t(r - 1) by ab(r - 1) in formula (5.8), it can be used to determine the value of ab(r - 1) that will result in the desired width of the confidence interval for σ². Next using a rule of thumb like that expressed in Section 5.4.4 the levels of factor A and Factor B can be determined.

# 5.5.4 Two-Factor Studies with Unequal Replication

When there are unequal numbers of replicates in each subclass, the method of moments or analysis of variance estimators of the variance components for the two-factor sampling experiment are not unique. Their values will depend on whether the type I or type III sums of squares are used to get the estimates. On the other hand, the maximum likelihood estimators and REML estimators are unique and may be preferred in this situation.

Table 5.6 Calcium in Blood Serum Solutions with Unknown Concentrations Standard Solution

| Laboratory | 1 | 2 | 3 | 4 |
| :--- | :--- | :--- | :--- | :--- |
| A | 87 | 92 | 179 | 177 |
| | 84 | 83 | 173 | |
| | 80 | 76 | 166 | |
| B | 80 | 69 | 138 | 151 |
| | 70 | 46 | 138 | |
| | | | 132 | |
| C | 70 | 67 | 173 | 176 |
| | 60 | 63 | 166 | |
| | 44 | 48 | | |

To illustrate the calculations, consider the data in Table 5.6 taken from a sampling study to estimate the sources of variability in an inter-laboratory assay of calcium in blood serum that was shown by Rao and Rao (1997). The commands to read the data and compute the variance components using proc varcomp are similar to those shown in the last section for balanced data. Using the method of moments-analysis of variance estimators proc varcomp only gives the option to use the type I sums of squares. The results of this analysis are shown on the next page.