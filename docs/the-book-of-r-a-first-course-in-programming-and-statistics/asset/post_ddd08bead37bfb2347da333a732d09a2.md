
+   - The function should contain a check for the rule of thumb to ensure the validity of the normal distribution in both one- and two-sample settings. If this is violated, the function should still complete but should issue an appropriate warning message (see Section 12.1.1).
- All that need be returned is a list containing the members Z (test statistic), P (appropriate p-value—this can be determined by alternative; for a two-sided test, determining whether Z is positive or not can help), and CI (two-sided CI with conf.level).

+   g. Replicate the two examples in the test of Sections 18.3.1 and 18.3.2 using Z.test; ensure you reach identical results.

+   h. Call Z.test(p1=0.11,n1=10,p0=0.1) to try your warning message in the one-sample setting.

## 18.4 Testing Categorical Variables

The normal-based Z-test is particular to data that are binary in nature. To statistically test claims regarding more general categorical variables, with more than two distinct levels, you use the ubiquitous *chi-squared test*. Pronounced khai, "chi" refers to the Greek symbol $\chi$ and is sometimes noted in shorthand as the $\chi^2$ test.

There are two common variants of the chi-squared test. The first—a chi squared test of distribution, also called *goodness of fit* (GOF) test—is used when assessing the frequencies in the levels of a single categorical variable. The second—a chi-squared test of *independence*—is employed when you're investigating the relationship between frequencies in the levels of two variables.

### 18.4.1 Single Categorical Variable

Like the Z-test, the one-dimensional chi-squared test is also concerned with comparing proportions in a setting where there are more than two proportions. A chi-squared test is used when you have $k$ levels (or categories) of a categorical variable and want to hypothesize about their observed frequencies to find out how many of $n$ observations fall into each defined category. In the following examples, it must be assumed that the categories are *mutually exclusive* (in other words, an observation cannot take more than one of the possible categories) and *exhaustive* (in other words, the $k$ categories cover all possible outcomes).

I'll illustrate how hypotheses are constructed and introduce the relevant ideas and methods with the following example. Suppose a researcher in sociology is interested in the dispersion of rates of facial hair in his local city and whether they are uniformly represented in the male population. It defines a categorical variable with three levels: clean shave (1), beard only or moustache only (2), and beard and moustache (3). He collects data on 53 randomly selected men and finds the following outcomes:

```
R> hairy <- c(2,3,2,3,2,1,3,2,3,2,2,2,3,3,3,2,3,2,1,3,2,2,1,2,3,
2,2,2,2,1,2,1,1,1,2,2,3,1,2,1,2,1,1,3)
```

Now, the research question asks whether the proportions in each category are equally represented. Let $\pi_1$, $\pi_2$, and $\pi_3$ represent the true proportion of men in the city who fall into groups 1, 2, and 3, respectively. Therefore we seek to test these hypotheses:

$H_0 : \pi_1 = \pi_2 = \pi_3 = \frac{1}{3}$
$H_1 : H_0$ is incorrect

For this test, use a standard significance level of 0.05.
The appearance of the alternative hypothesis is a little different from the interpretation of what you've seen so far but is an accurate reflection of a chi-squared goodness of fit. In these types of problems, $H_0$ is always that the proportions in each group are equal to the values, and $H_A$ is that the data, as a whole, do not match the proportions defined in the null. The test conducts assuming the null hypothesis is true, and evidence against the no-change, baseline setting will be represented as a small p-value.

# Calculation Chi-Squared Test of Distribution

The quantities of interest are the proportion of $n$ observations in each categories, $\pi_1, \dots, \pi_k$, for a single mutually exclusive and exhaustive variable. The null hypothesis defines these null values for each proportion; label these respectively as $\pi_{0(i)}, \dots, \pi_{0(k)}$. The test statistic $\chi^2$ is given as

```
$\chi^2 = \sum_{i=1}^{k} \frac{(O_i - E_i)^2}{E_i} (18.11)$
```

Where $O_i$ is the *observed* count and $E_i$ is the *expected* count in the $i$th category; $i = 1, \dots, k$. The $O_i$ are obtained from the raw data, and the expected counts, $E_i = n\pi_{0(i)}$, are merely the product of the overall sample size with the respective null proportion for each category. The result of $\chi^2$ follows a chi-squared distribution (explained further momentarily) with $u = k-1$ degrees of freedom. You usually consider the test to be valid based on an informal rule of thumb that at least 80 percent of the expected counts $E_i$ should be at least 5.

In this type of chi-squared test, it is important to note the following:

+   - The term *goodness of fit* refers to the proximity of the observed data to the distribution hypothesized in $H_0$.

+   Positive extremity of the result of (18.11) provides evidence against H₀. As such, the corresponding p-value is always computed as an upper-tail area.

+   As in the current example, a test for uniformity simplifies the null hypothesis slightly by having equivalent proportions π₀ = π₀(1) = ... = π₀(k).

+   A rejected H₀ doesn't tell you about the true values of πᵢ. It merely suggests that they do not follow H₀ specifically.

The chi-squared distribution relies on specification of a degree of freedom, unlike the t-distribution. Unlike a χ-curve, however, a chi-squared curve is unidirectional in nature, being defined for non-negative values and with a positive (right-hand) horizontal asymptote (tail going to zero).

It's this unidirectional distribution leads to p-values defined as upper-tail areas only; decisions like one- or two-tailed areas have no relevance in these types of chi-squared tests. To get an idea of the density functions actually look like, Figure 18-1 shows three particular curves with ν=1, ν=5, and ν=10 degrees of freedom.

![](img/b2cfc85cbb129f60fe595a2bae074fe4_445_0.png)

Figure 18-1: Three instances of the chi-squared density function using differing degrees of freedom values. Note the positive domain of the function and the "flattening" and "right-extending" behavior as v is increased.

This image was produced using the relevant d-function, dchisq, with v passed to the argument df.

```
R x <-seq(0,20,length=100)
R plot(x,dchisq(x,df=1),type="1",xlim=c(0,15),ylim=c(0,0.5),ylab="density")
R lines(x,dchisq(x,df=5),lty=2)
R lines(x,dchisq(x,df=10),lty=3)
R abline(h=0,col="gray")
```

412 Chapter 18

```
abline(v=0,col="gray")nRlegend("topright",legend=c("df=1","df=5","df=10"),lty=1:3)
```

The current facial hair example is a test for the uniformity of the distributions in the three categories. You can obtain the observed counts and corresponding proportions with table.

```
R n <- length(hairy)
R n
[1] 53
Rairy.tab <- table(hairy)
Rairy.tab
hairy
      1 2 3
11 28 14
Rairy.tab/n
hairy
0.207542 0.5283019 0.2641509
```

For computation of the test statistic $\chi^2$, you have the observed counts $O_i$ in hairy.tab. The expected count $E_i$ is a straightforward arithmetic calculation of the total number of observations multiplied by the null proportion 1/3 (the result as expected), giving you the value for each category.

These, as well as the contribution of each category to the test statistic, are nicely presented in a matrix constructed with cbind (Section 3.1.2).

```
R expected <- 1/3*n
R expected
[1] 17.66667
Rairy.matrix <- cbind(1:3,hairy.expected,
hairy.expected)^2/expected)
R dimnames(hairy.matrix) <- list(c("clean","beard OR mous.",
"beard AND mous."),
c("i","Oi","Ei"),(OI-Ei)^2/Ei))
```

```
R hairy.matrix
clean      i Oi (Ei-Oi)^2/Ei
           1 17.66667 2.515233
beard OR mous. 2 28 17.66667 6.0440252
beard AND mous. 3 14 17.66667 0.7610063
```

Note that all the expected counts are comfortably greater than 5, which satisfies the informal rule of thumb mentioned earlier. In terms of R coding, also note that the single number is implicitly recycled to match the length of the other vectors supplied to cbind and you've used the dimens attribute (refer to Section 6.2.1) to annotate the rows and columns.
