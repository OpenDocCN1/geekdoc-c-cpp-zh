# Figure 7.3 Final data set output from PROC UNIVARIATE

| | Number | ci2_5 | ci97_5 |
|---|---|---|---|
| 1 | 1 | 6.6683063611 | 8.2044066933 |
| 2 | 2 | 2.7496613966 | 3.8034761911 |
| 3 | 3 | 0.1571411282 | 0.3293202486 |
| 4 | 4 | 0.0781773482 | 0.1762668438 |
| 5 | 5 | 0.0491894662 | 0.12122238 |
| 6 | 6 | 0.0223418825 | 0.0825019539 |
| 7 | 7 | -0.002321409 | 0.049210235 |
| 8 | 8 | -0.026757273 | 0.0165793219 |
| 9 | 9 | -0.048553003 | -0.009261781 |
| 10 | 10 | -0.066158723 | -0.030617703 |
| 11 | 11 | -0.084416946 | -0.05018291 |
| 12 | 12 | -0.100432506 | -0.064214789 |
| 13 | 13 | -0.118548036 | -0.078569921 |
| 14 | 14 | -0.138006805 | -0.093207119 |

# An Aligning Procedure for Factor Loadings

An additional step is required when bootstrapping CI for factor loadings. As you might have noticed in your own analyses, the order in which factors are extracted can be arbitrary, and the direction of the loadings on a factor can change. This is a problematic phenomenon when considering estimation of bootstrapped CI around factor loadings because the results from one resample might be systematically different from another. For example, if we run the syntax presented in the previous section and examine the bootstrapped results from the engineering data, we might find some instances where interest was extracted as the first factor and others where the problem solving factor was extracted first. In addition, in one data set we might find an item that has a loading of 0.88 on the interest factor, and in another it might have a loading of -0.88. These two issues have been referred to as the “alignment problem” in the literature (Clarkson, 1979; Pennell, 1972). They must be addressed before the CIs are estimated.

An alignment procedure has been proposed to address these issues (Clarkson, 1979; Ichikawa & Konishi, 1995). This procedure essentially compares each possible factor order solution within a given resample to the original solution and calculates the sum of squared deviations to identify the solution with the best fit. For example, if three factors are being extracted then we would compare the factors in their initial order, 1-2-3, to the original solution that was derived from the entire sample. But then we would also reorder and compare the bootstrapped solution using the following order schemes: 1-3-2, 2-1-3, 2-3-1, 3-1-2, and 3-2-1. We must compare all possible orderings of the factors. Thus, there would be k! possible combinations that must be evaluated, where k is the number of factors. We would identify the order that has the smallest sum of squared deviations as having the best fit and being the order that best aligns with the original solution. We would then re-order the bootstrapped results to match the identified order. Finally, the direction of the loading would