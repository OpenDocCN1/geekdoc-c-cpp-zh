```
/* Calculates mean and standard deviations */
proc sort data=breed; by time;
proc means data=breed var height by time;
output out=means stdev=;
/* Creates weights */
data breed3; merge breed means; by time;
w=1/s;
proc glm data=breed3;
class time;
model height=time;
weight w;
run;
```

The GLM Procedure

Dependent Variable: height

Weight: w

| Source | DF | Sum of Squares | Mean Square | F Value | Pr > F |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Model | 2 | 18.20937757 | 9.10468879 | 6.23 | 0.0201 |
| Error | 9 | 13.16606021 | 1.46229560 | | |
| Corrected Total | 11 | 31.36998578 | | | |

With these results, it can be seen that F-test from the weighted least squares is more sensitive than the unweighted least squares, and the P-value is similar to what was obtained with the Box-Cox transformation shown in Section 2.5.1.

When the error distribution is not normal, an alternative to analyzing a transformation of the response is to use a generalized linear model (see McCullagh and Nelder, 1989). In fitting a generalized linear model, the user must specify the error distribution and a link function in addition to the model. The method of maximum likelihood is used to estimate the model parameters and the generalized likelihood ratio tests are used to test the hypotheses. When the link function is the identity and the distribution is normal, the generalized linear model analysis will result in the method of least squares and the ANOVA F-test. The SAS procedure genmod will fit the generalized linear model and compute appropriate likelihood ratio test statistics. This procedure allows the user to choose from the distributions Binomial, Poisson, Negative Binomial, Multinomial, Gamma, Inverse Gaussian, as well as Normal. For each distribution, genmod has a default link function.

To illustrate the use of proc genmod to analyze experimental data, consider the following example. A professor wanted to compare three different teaching methods to determine how the students would perceive the course. The treatment factor was the teaching method, the experimental unit was a class of students, and the response was the summary of student ratings for the