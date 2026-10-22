
## Table 10.1 Death Sentence by Race of Defendant

|  | Blacks | Nonblacks | Total |
|---|---:|---:|---:|
| Death | 28 | 22 | 50 |
| Life | 45 | 52 | 97 |
| **Total** | **73** | **74** | **147** |

Let’s consider the table in more general form as

| $m_{11}$ | $m_{12}$ |
|---|---|
| $m_{21}$ | $m_{22}$ |

where $m_{ij}$ is the *expected number* of cases falling into row $i$ and column $j$. What I mean by this is that if $n$ is the sample size and $p_{ij}$ is the probability of falling into cell $(i,j)$, then

$$m_{ij}=np_{ij}.$$

There are a couple of different but equivalent ways of writing a loglinear model for these four frequency counts. The way I’m going to do it is consistent with how PROC GENMOD estimates the model. Let $R_i$ be a dummy variable for the rows, having a value of 1 if $i=1$ and 0 if $i=2$. Similarly, let $C_j$ be a dummy variable for the columns with a value of 1 if $j=1$ and 0 if $j=2$. We can then write the “saturated” loglinear model for this $2\times2$ table of frequency counts as

$$\log m_{ij}=\beta_0+\beta_1R_i+\beta_2C_j+\beta_3R_iC_j \qquad i,j=1,2. \tag{10.1}$$

Note that $R_iC_j$ is the product (interaction) of $R_i$ and $C_j$. Equation (10.1) actually represents four different equations:

$$\begin{aligned}
\log m_{11}&=\beta_0+\beta_1+\beta_2+\beta_3\\
\log m_{12}&=\beta_0+\beta_1\\
\log m_{21}&=\beta_0+\beta_2\\
\log m_{22}&=\beta_0.
\end{aligned} \tag{10.2}$$

In a moment, we’ll see how to estimate the four $\beta$ parameters using PROC GENMOD. But before doing that, let’s talk about why we might be interested in these parameters at all. All we’ve done in equation (10.2) is transform the four expected frequencies into four different quantities. The reason for doing this is that the $\beta$’s show us things about the table that aren’t so easily seen by looking at the frequency counts.

We are particularly interested in β₃, which is the coefficient for the interaction term.

If we solve equations (10.2) for β₃, we get:

β₃ = log( (m₁₁ m₂₂) / (m₁₂ m₂₁) )  (10.3)

The quantity in parenthesis is the cross-product ratio. In Chapter 2, we saw that the cross-product ratio is equal to the odds ratio. In this case, it’s the ratio of the odds of a death sentence for blacks to the odds of a death sentence for nonblacks. Recall that an odds ratio of 1.0 corresponds to independence between the two variables. Because the logarithm of 1 is 0, independence of the row and column variables is equivalent to β₃=0. So, we can test whether the two variables are independent by testing whether β₃=0.

All this has been expressed in terms of expected frequency counts, the mᵢⱼ. What about the observed frequency counts, which I’ll denote by nᵢⱼ? For the model we’ve just been considering, the maximum likelihood estimator of β₃ has the same form as equation (10.3) except that expected frequencies are replaced by observed frequencies:

β̂₃ = log( (n₁₁ n₂₂) / (n₁₂ n₂₁) )  (10.4)

For the data in Table 10.1, β̂₃ = log[(28×52)/(45×22)] = .3857. Similar expressions can readily be obtained for the other β parameters in the model, but we’re usually not very interested in them.

Although it’s simple enough in this case to get all the maximum likelihood estimates by hand calculations, we can also do it with PROC GENMOD. Here is the SAS code:

```
DATA penalty;
    INPUT n death black;
    DATALINES;
28 1 1
22 1 0
45 0 1
52 0 0
;
PROC GENMOD DATA=penalty;
    MODEL n = death black death*black / DIST=POISSON;
RUN;
```

Each cell in the table is a separate record in the data set. DEATH is a dummy variable for a death sentence, and BLACK is a dummy variable for race. The MODEL statement includes the main effects of row and column, as well as their interaction. The DIST option in the MODEL statement says that each frequency count has a Poisson distribution whose expected value m_ij is given by equation (10.2). For frequency counts in contingency tables, the Poisson distribution is appropriate for a variety of different sampling designs. As we saw in Chapter 9, the default in GENMOD for a Poisson distribution is LINK=LOG. That means that the logarithm of the expected value of the dependent variable is assumed to be a linear function of the explanatory variables, which is exactly what equation (10.1) says.

## Output 10.1 PROC GENMOD Output for Loglinear Model for a 2 × 2 Table

| Criteria For Assessing Goodness Of Fit |
| Criterion | DF | Value | Value/DF |
| Deviance | 0 | 0.0000 | . |
| Scaled Deviance | 0 | 0.0000 | . |
| Pearson Chi-Square | . | 0.0000 | . |
| Scaled Pearson X2 | . | 0.0000 | . |
| Log Likelihood |  | 391.0691 |  |
| Full Log Likelihood |  | -10.7765 |  |
| AIC (smaller is better) |  | 29.5531 |  |
| AICC (smaller is better) |  | . |  |
| BIC (smaller is better) |  | 27.0983 |  |

| Analysis Of Maximum Likelihood Parameter Estimates |
| Parameter | DF | Estimate | Standard Error | Wald 95% Confidence Limits | Wald Chi-Square | Pr > ChiSq |
| Intercept | 1 | 3.9512 | 0.1387 | 3.6794 4.2230 | 811.84 | <.0001 |
| death | 1 | -0.8602 | 0.2543 | -1.3587 -0.3617 | 11.44 | 0.0007 |
| black | 1 | -0.1446 | 0.2036 | -0.5436 0.2545 | 0.50 | 0.4776 |
| death*black | 1 | 0.3857 | 0.3502 | -0.3006 1.0721 | 1.21 | 0.2706 |
| Scale | 0 | 1.0000 | 0.0000 | 1.0000 1.0000 |  |  |

Examining Output 10.1, we see that the deviance for this model is 0. That’s because it’s a saturated model; there are four estimated parameters for the four cells in the table, so the model perfectly reproduces the frequency counts. The estimate for the interaction is .3857, which is the same value obtained from hand calculation of equation (10.4). This

estimate has an associated Wald chi-square of 1.214, which is nearly identical to the traditional Pearson chi-square (1.218) for testing whether the two variables are independent (obtained with PROC FREQ). That’s not surprising because both statistics are testing the same null hypothesis.

Instead of a loglinear model, we could estimate a logit model for this table, taking death sentence as the dependent variable:

```
PROC GENMOD DATA=penalty DESC;
FREQ n;
MODEL death=black / D=BINOMIAL LINK=LOGIT AGGREGATE;
RUN;
```

This produces Output 10.2.

## Output 10.2 PROC GENMOD Output for Logit Model for a 2 ×2 Table

| Analysis Of Maximum Likelihood Parameter Estimates |
| Parameter | DF | Estimate | Standard Error | Wald 95% Confidence Limits | Wald Chi-Square | Pr > ChiSq |
| Intercept | 1 | -0.8602 | 0.2543 | -1.3587 -0.3617 | 11.44 | 0.0007 |
| black | 1 | 0.3857 | 0.3502 | -0.3006 1.0721 | 1.21 | 0.2706 |
| Scale | 0 | 1.0000 | 0.0000 | 1.0000 1.0000 |  |  |

Remarkably, the estimates in Output 10.2 are identical to some of the estimates in Output 10.1. The coefficient for BLACK in the logit model is the same as the BLACK*DEATH coefficient in the loglinear model, along with identical standard errors and chi-squares. Similarly, the intercept (and associated statistics) in the logit model is the same as the DEATH coefficient in the loglinear model. This is a general phenomenon. As I’ve said before, every logit model for a contingency table has a corresponding loglinear model. But the main effects in the logit model become 2-way interactions (with the dependent variable) in the loglinear model. The intercept in the logit model becomes a main effect of the dependent variable in the loglinear model.

Now let’s do something peculiar just to emphasize the point. We’ll estimate another logit model, but we’ll switch the variables around and make BLACK the dependent variable and DEATH the independent variable:

```
PROC GENMOD DATA=penalty DESC;
    FREQ n;
    MODEL black=death / D=BINOMIAL LINK=LOGIT AGGREGATE;
RUN;
```

## Output 10.3 PROC GENMOD Output for Logit Model for a 2 × 2 Table with Variables Reversed

| Analysis Of Maximum Likelihood Parameter Estimates |
| Parameter | DF | Estimate | Standard Error | Wald 95% Confidence Limits | Wald Chi-Square | Pr > ChiSq |
| Intercept | 1 | -0.1446 | 0.2036 | -0.5436 0.2545 | 0.50 | 0.4776 |
| death | 1 | 0.3857 | 0.3502 | -0.3006 1.0721 | 1.21 | 0.2706 |
| Scale | 0 | 1.0000 | 0.0000 | 1.0000 1.0000 |  |  |

In Output 10.3, we see again that the slope coefficient (along with its standard error and chi-square) is identical to the two-way interaction in the loglinear model. Unlike bivariate linear regression, where the regression line changes when you reverse the dependent and independent variables, the bivariate logit model is symmetrical with respect to the two variables. We also see that the intercept term corresponds to the main effect of BLACK in the loglinear model.

Why do the logit models share parameters with the loglinear model? The algebra that demonstrates this is really quite simple. The dependent variable in the logit model is the logarithm of the odds. As explained in chapter 2, the odds can be defined as the expected number of events divided by the expected number of non-events. For example, the log-odds of a death sentence for racial group j is log(m1j/m2j). Substituting from the loglinear model in equation (10.1), we get:

log(m1j/m2j) = log(m1j) − log(m2j)
= (β0 + β1R1 + β2Cj + β3R1Cj) − (β0 + β1R2 + β2Cj + β3R2Cj).

But because R1=1 and R2=0, this reduces to:

log(m1j/m2j) = β1 + β3Cj.
