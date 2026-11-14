
| Obs | temp | moisture | soil | k | half_life |
|---|---|---|---|---|---|
| 1 | 10 | L | C | -0.001202 | 576.845 |
| 2 | 10 | L | P | -0.002728 | 254.065 |
| 3 | 10 | H | C | -0.004828 | 143.572 |
| 4 | 10 | H | P | -0.005547 | 124.762 |
| 5 | 30 | L | C | -0.005053 | 137.415 |
| 6 | 30 | L | P | -0.010462 | 66.255 |
| 7 | 30 | H | C | -0.008767 | 79.066 |
| 8 | 30 | H | P | -0.012854 | 53.927 |
| 9 | 10 | L | C | -0.002603 | 266.325 |
| 10 | 10 | L | P | -0.004008 | 248.754 |
| 11 | 10 | H | C | -0.002566 | 270.115 |
| 12 | 10 | H | P | -0.004192 | 165.340 |
| 13 | 30 | L | C | -0.006293 | 110.151 |
| 14 | 30 | L | P | -0.009222 | 75.165 |
| 15 | 30 | H | C | -0.015358 | 51.202 |
| 16 | 30 | H | P | -0.015393 | 45.029 |

The approach to fitting a repeated measure over time and then analyzing coefficients from the fitted model is often called the growth curve approach, and it is used so often that it is incorporated as a feature in SAS proc glm. By adding the actual levels of the within subject (time) factor and the polynomial option to the repeated statement as shown in the commands below,

```
proc glm data=residue;
   class temp moisture soil;
   model lc1 lc2 lc3 lc4 lc5 = temp|moisture|soil;
   repeated time 5 (0 7 14 30 60) polynomial/
   print summary;
run;
```

proc glm automatically computes polynomial contrasts over the repeated measures and analyzes each one separately. For example, two of the tables resulting from this command are shown on the next page.

The table for time.1 shown on the next page is the analysis of the linear contrast in log concentration over days. The significance levels (P-values) are similar to those resulting from the analysis of the log half-life. Both temperature and moisture have significant effects on the linear contrast, and soil (P-value=0.0364) is also significant at the \(\alpha = 0.05\) level. In the analysis of log half-life described above the P-value for soil was 0.0526.

The table for time.2 shown on the next page is the analysis of the quadratic contrast in log concentration over days. Here it can be seen that none of the factors affect the quadratic trend. The polynomial option on the repeated statement in proc glm calculates up to \(l - 1\) polynomial contrasts for \(l\) repeated measures time points.

## The GLM Procedure

### Repeated Measures Analysis of Variance

### Analysis of Variance of Contrast Variables

time_N represents the nth degree polynomial contrast for time

### Contrast Variable: time_1

| Source | DF | Type III SS | Mean Square | F Value | Pr > F |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Mean | 1 | 1.63068592 | 1.63068592 | 297.79 | < .0001 |
| temp | 1 | 0.47804051 | 0.47804051 | 87.30 | < .0001 |
| moisture | 1 | 0.08498935 | 0.08498935 | 15.52 | 0.0043 |
| temp*moisture | 1 | 0.02381646 | 0.02381646 | 4.35 | 0.0705 |
| soil | 1 | 0.03448920 | 0.03448920 | 6.30 | 0.0364 |
| temp*soil | 1 | 0.01821844 | 0.01821844 | 3.33 | 0.1056 |
| moisture*soil | 1 | 0.00126468 | 0.00126468 | 0.23 | 0.6437 |
| temp*moisture*soil | 1 | 0.00000176 | 0.00000176 | 0.00 | 0.9861 |
| Error | 8 | 0.04380496 | 0.00547562 | | |

### Contrast Variable: time_2

| Source | DF | Type III SS | Mean Square | F Value | Pr > F |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Mean | 1 | 0.00004201 | 0.00004201 | 1.91 | 0.2045 |
| temp | 1 | 0.00000785 | 0.00000785 | 0.36 | 0.5669 |
| moisture | 1 | 0.00004169 | 0.00004169 | 1.89 | 0.2061 |
| temp*moisture | 1 | 0.00000005 | 0.00000005 | 0.00 | 0.9644 |
| soil | 1 | 0.00000268 | 0.00000268 | 0.12 | 0.7361 |
| temp*soil | 1 | 0.00000068 | 0.00000068 | 0.03 | 0.8647 |
| moisture*soil | 1 | 0.00001497 | 0.00001497 | 0.68 | 0.4335 |
| temp*moisture*soil | 1 | 0.00000002 | 0.00000002 | 1.55 | 0.2490 |
| Error | 8 | 0.00017615 | 0.00002202 | | |

## 9.7 Review of Important Concepts

The crossover and repeated measures designs presented in this chapter are special cases of the randomized complete block (RCB), Latin square design (LSD), and split-plot (CRSP, RBSP) designs presented in Chapters 4 and 8 and highlighted in Figure 9.4. These designs are used in situations where the blocking factor is a human subject or large animal, and the subplot experimental units are successive periods of time.

Crossover designs are most useful when a more precise test of the treatment effects is desired and each subject can be assigned each treatment in successive periods. Crossover experiments should not be used in cases where the experimental subjects are permanently changed by the initial treatment. Otherwise, the result of applying following treatments will not be the same as it would be if they had been applied first. Except for the simple two-period AB, BA case, the levels of the whole-plot factor in crossover experiments are just random groupings of subjects and can usually be ignored in the analysis. Therefore, the model for the analysis of crossover experiments, except for the

## Figure 9.4 Design Selection Roadmap

![](img/878b651cdbe9da3d6d22e64d64b8a54f_389_0.png)

simple case, is the same as it is for Latin square designs. For the simple two-period AB, BA case, the model is the same as a split-plot model, where the whole-plot treatment factor is the carryover effect.

Repeated measures designs are useful when the objective is to compare the trend in the response across repeated measures over time between levels or combinations of levels of treatment factors. The model is the same as a split-plot experiment, where treatment factors are the whole-plot factors and repeated measures over time are the subplot factors. When the covariance matrix of the repeated measures satisfies the Huynh-Feldt condition, the same ANOVA or REML analysis used for split-plot experiments is appropriate.

When the Huynh-Feldt condition does not hold, there are two alternative univariate methods of analysis that can be used. The first method is a correction to the usual ANOVA F-tests based on degree of freedom adjustments proposed by Greenhouse and Geisser or Huynh and Feldt. The second univariate analysis method that can be used is the conservative growth curve approach. In this approach a curve is fit to each set of repeated observations over time, and summary statistics from the curve fits, which are independent from one combination of whole-plot factor levels to another, are analyzed as separate responses.

## 9.8 Exercises

- 1. Consider the data from a study reported by Varma and Chilton (1974), that was later re-analyzed by Jones (1980).

| Subject | Group 1 Period 1 Placebo | Group 1 Period 2 Test | Group 2 Period 1 Test | Group 2 Period 2 Placebo |
|---|---|---|---|---|
| 1 | 0.83 | 1.83 | 1.67 | 0.33 |
| 2 | 1.00 | 2.17 | 2.50 | 0.50 |
| 3 | 0.67 | 1.67 | 1.00 | -0.17 |
| 4 | 0.50 | 1.50 | 1.67 | 0.50 |
| 5 | 0.50 | 2.33 | 1.83 | 0.50 |
| 6 | 0.83 | 1.83 | 0.50 | 0.33 |
| 7 | 1.00 | 0.50 | 1.33 | 0.67 |
| 8 | 0.67 | 0.33 | 1.33 | 0.00 |
| 9 | 0.67 | 0.50 | 0.50 | 0.17 |
| 10 | 0.33 | 0.67 | 2.17 | 0.83 |
| 11 | 0.00 | 0.83 | 1.67 | 0.33 |
| 12 | 1.17 | 1.33 | 1.50 | 0.00 |
| 13 | 0.00 | 0.67 | 1.33 | 0.50 |
| 14 | 0.50 | 1.83 | 1.50 | 0.50 |
| 15 | 0.33 | 1.50 | 1.33 | 0.00 |
| 16 | 0.33 | 1.50 | 0.67 | -0.17 |
| 17 | 0.50 | 1.17 | 1.67 | 0.50 |
| 18 | 1.00 | 1.67 | 2.50 | 0.67 |
| 19 | 0.00 | 1.33 | 1.83 | 0.00 |
| 20 | 0.50 | 1.50 | 0.83 | 0.67 |
| 21 | -0.50 | 2.83 | 2.33 | 0.17 |
| 22 | 0.17 | 2.33 | 1.17 | 0.50 |
| 23 | 1.00 | 1.33 | 1.33 | 0.00 |
| 24 | 1.00 | 1.67 | 1.33 | 0.83 |
| 25 | 1.33 | 0.67 | 0.33 | 1.33 |
| 26 | 0.33 | 0.83 | 2.17 | 1.17 |
| 27 | 2.00 | 1.00 | 1.00 | 0.33 |
| 28 | 4.00 | 0.17 | 0.33 | 1.00 |
| 29 | 0.83 | 1.67 | 1.17 | 0.17 |
| 30 | 0.50 | 1.33 | 0.50 | 0.50 |
| 31 | 0.50 | 1.50 | | |
| 32 | 0.50 | 1.67 | | |
| 33 | 2.17 | 1.33 | | |
| 34 | 0.67 | 1.17 | | |

This was a simple crossover dental study comparing a test compound to a placebo with regard to their effect on dental hygiene as measured by the change in a dental hygiene index. There were thirty-four patients randomized to the first group and thirty patients randomized to the second group.

- (a) Use proc glm to analyze the data from this experiment.

- (b) Is there a difference of the test compound and placebo with respect to their effect on dental hygiene? If so, which produces the larger change in the index?

- (c) Is there any evidence of carryover effect of the test compound?

- 2. Lucas (1957) presented data from an extra-period crossover study on dairy cows. Three diet treatments were being compared and the response was the average daily production of FCM. The data is shown in the table below.

### Table 9.11 Dairy Cow Experiment - Response Is Average Daily FCM Production in Pounds, the Treatment Indicator Is In Parentheses

| Group | Cow | 1 | 2 | 3 | 4 |
|---|---|---|---|---|---|
| 1 | 1 | (1) 38.66 | (2) 37.43 | (3) 34.39 | (3) 31.30 |
| 1 | 2 | (1) 25.72 | (2) 26.13 | (3) 23.35 | (3) 18.69 |
| 2 | 3 | (2) 48.85 | (3) 46.88 | (1) 41.99 | (1) 39.61 |
| 2 | 4 | (2) 30.80 | (3) 29.29 | (1) 26.41 | (1) 23.16 |
| 3 | 5 | (3) 34.64 | (1) 32.27 | (2) 28.50 | (2) 27.13 |
| 3 | 6 | (3) 25.35 | (1) 26.00 | (2) 23.86 | (2) 19.92 |
| 4 | 7 | (1) 35.19 | (3) 33.50 | (2) 28.41 | (2) 25.12 |
| 4 | 8 | (1) 21.80 | (3) 23.91 | (2) 21.69 | (2) 17.55 |
| 5 | 9 | (2) 32.90 | (1) 33.12 | (3) 27.52 | (3) 25.10 |
| 5 | 10 | (2) 21.37 | (1) 21.97 | (3) 19.38 | (3) 16.57 |
| 6 | 11 | (3) 30.40 | (2) 29.50 | (1) 26.70 | (1) 23.09 |
| 6 | 12 | (3) 22.84 | (2) 20.97 | (1) 18.59 | (1) 16.10 |

- (a) Does every treatment follow every other treatment, including itself?

- (b) Analyze the data using proc glm. Are the treatment and carryover effects orthogonal? Check by comparing their type I and type III sums of squares.

- (c) Use the lsmeans statement to get least squares adjusted means for treatments. Why is this possible when it was not possible for the example in Section 9.4.1 ?

- 3. Consider planning an experiment to compare the taste of chocolate brownie recipes. The treatments will consist of three brands of boxed brownie mixes and one from-scratch home recipe. A panel of tasters will be used to evaluate the brownies. Each taster will taste each brownie and give it a rating from 1 to 10 (10 being the best possible).
