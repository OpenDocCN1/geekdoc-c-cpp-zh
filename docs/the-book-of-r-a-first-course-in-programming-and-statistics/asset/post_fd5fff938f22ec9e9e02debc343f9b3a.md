
The test statistic, as per (18.11), is given as the sum of the $(O_i - E_i)^2/E_i$ contributions in the fourth column of hairy.matrix.

```
R X2 <- sum(hairy.matrix[,4])
R X2
[1] 0.0932075
```

The corresponding p-value is the appropriate upper-tail area of the chi-squared distribution with $
u = 3-1 = 2$ degrees of freedom.

```
R 1-pchisq(X2,df=2)
[1] 0.00942681
```

This small p-value provides evidence to suggest that the true frequencies in the defined categories of male facial hair are not uniformly distributed in a 1/3,1/3,1/3 fashion. Remember that the test result doesn't give you the true properties but only suggests that they do not follow those in $H_0$.

## R Function: chisq.test

Like t and prop.test, R provides a quick-use function for performing a chi-squared GOF test. The chisq test function takes the vector of observed frequencies as its first argument x. For the facial hair example, this simple line therefore provides the results as found previously:

```
R chisq.test(x=hairy.tab)
```

Chi-squared test for given probabilities

```
data: hairy.tab
X-squared = 9.3208, df = 2, p-value = 0.009463
```

By default, the function performs a test for uniformity, taking the number of categories as the length of the vector supplied to x. However, suppose that the researcher collecting the facial hair data realizes he was doing so in November, during which many men grow mustaches in support of "Mo-ovember" to raise awareness of men's health. This changes thoughts on the true rates in their clean-shaven (1), beard-only or moustache (2), and beard and moustache (3) categories. He wants to test the following:

> $H_0 : \pi_{(1)} = 0.25; \pi_{(2)} = 0.5; \pi_{(3)} = 0.25
H_A : H0 is incorrect.

If a GOF test of uniformity is not desired, when the "true" rates across the categories are not all the same, the chisq.test function requires you to supply the proportions as a vector of the same length as x to the p argument. Naturally, each entry in p must correspond to the categories labeled in x.

```
> chisq.test(x=hairy.tab,p=c(0.25,0.5,0.25))
```

Chi-squared test for given probabilities

data: hairy.tab
X-squared = 0.5094, df = 2, p-value = 0.7751

With a very high p-value, there is no evidence to reject H₀ in this scenario. In other words, there is no evidence to suggest that the proportions hypothesized for H₀ are incorrect.

## 18.4. Two Categorical Variables

The chi-squared test can also apply to the situation in which you have two mutually exclusive and exhaustive categorical variables at hand—call them variable A and variable B. It is used to detect whether there might be influential relationship (in other words, dependence) between A and B by looking at the way in which the distribution of frequencies change with respect to their categories. If there is no relationship, the distribution of frequencies in variable A will have nothing to do with the distribution of frequencies in variable B. As such, this particular variant of the chi-squared test is called a test of independence and is always performed with the following hypotheses:

> H₀ : Variables A and B are independent.
(or, There is no relationship between A and B.)
H_₁ : Variables A and B are not independent.
(or, There is a relationship between A and B.)

Carry out the test, therefore compare the observed data to the counts you'd expect to see if the distributions were completely unrelated (satisfying the assumption that H₀ is true). An overall departure from the expected frequencies will result in a small p-value and provide evidence against the null.

So, how are such data presented? For two categorical variables, a two-dimensional structure is appropriate; in R, this is a standard matrix. For example, suppose some dermatologists at a certain clinical practice are interested in their successes in treating a common skin affinity. Their records show N=355 patients have been treated at their clinic using one of four possible treatments—a course of tablets, a series of injections, a laser treatment, and an herbal-based remedy. The level of success in curing the affliction is also recorded—partial success, and full success. The data are given in the constructed matrix skin.

```
> skin <- matrix(c(20,32,8,52,9,72,38,32,64,30,120),4,3,
dimnames=list(c("Injection","Tablet","Laser","Herbal"),
c("None","Partial","Full"))
```

R> skin None Partial Full
Injection 20 9 16
Tablet 32 72 64
Laser 8 8 30
Herbal 52 32 12

### A two-dimensional table presenting frequencies in this fashion is called a contingency table.

### Calculation: Chi-Squared Test of Independence

To compute the test statistic, presume data are presented as a $k_r \times k_c$ contingency table, in other words, a matrix of counts, based on two categorical variables (both mutually exclusive and exhaustive). The focus of the test is the way in which the $N$ observations between the $k_r$ levels of the "row" variable and the $k_c$ levels of the "column" variable are jointly distributed. The test statistic $\chi^2$ is given with

```
$$\chi^2 = \sum_{i=1}^{k_r} \sum_{j=1}^{k_c} \frac{(O_{[i,j]} - E_{[i,j]})^2}{E_{[i,j]}}$$ (18.12)
```

where $O_{[i,j]}$ is the observed count and $E_{[i,j]}$ is the expected count at position i and column position j. Each $E_{[i,j]}$ is found as the sum total of row i multiplied by the sum total of column j, all divided by N.

```
$E_{[i,j]} = \frac{(\sum_{u=1}^{k_r} O_{[u,j]}) \times (\sum_{v=1}^{k_c} O_{[i,v]})}{N}$$ (18.13)
```

The result, $\chi^2$, follows a chi-squared distribution with $
u = (k_r - 1) \times (k_c - 1)$ degrees of freedom. The p-value is always an upper-tailed area, and you can consider the test with satisfaction of the condition that at least 80 percent of the $E_{[i,j]}$ are at least 5. For calculation, it's important to note the following:

- It's not necessary to assume that $k_r = k_c$.
- The functionality of Equation (18.12) is the same as that of (18.11)—an overall sum involving the squared differences between the observed and expected values of each cell.
- The double-sum in (18.12) just represents the total sum over all the cells, in the sense that you can compute the total sample size $N$ with $\sum_{i=1}^{k_r} \sum_{j=1}^{k_c} O_{[i,j]}$.
- A rejected $H_0$ doesn't tell you about the nature of *how* the frequencies depend on one another, just that there is evidence to suggest that some kind of dependency between the two categorical variables exists.

Continuing the example, the dermatologists want to determine whether their records suggest there is statistical evidence to indicate some relationship between the type of treatment and the level of success in curing the skin affliction. For convenience, store the total number of categories $k_r$ and $k_c$ for the row and column variables, respectively.

```
R kr <- nrow(skin)
R kc <- ncol(skin)
```

You have $O_{\{i,j\}}$ in skin, so you now must compute the $E_{\{i,j\}}$ in light of Equation (18.13), which deals with row and column sums, you can evaluate these using the built-in rowSums and colSums functions.

```
R rowSums(skin) Tablet
Injection Laser Herbal
    45 168 46 96
R colSums(skin)
None Partial Full
    112 121 122
```

These results indicate the totals in each group, regardless of the other variable. To get the expected counts for all cells of the matrix, Equation (18.13) requires each row to be multiplied by each column sum once. You could write a for loop, but this would be inefficient and rather inelegant. It is better to use `rep` with the optional argument (refer to Section 2.3.2). By repeating each element of the column totals to multiply that repeated vector by the shorter vector produced by rowSums, You can then call sum(skin) to divide this by $N$ and arrange it into a matrix. The following lines show how this works-by-step:

```
R rep(colSums(skin),each=kr)
None None None Partial Partial Partial Full
    112 112 112 121 121 121 121 122
Full Full Full
    122 122 122
```

```
R rep(colSums(skin),each=kr)*rowSums(skin)
None None None Partial Partial Partial Full
    5040 18816 5152 10752 5445 20328 5566 11616 5490
Full Full Full
    20496 5612 17172
```

```
R rep(colSums(skin),each=kr)*rowSums(skin)/sum(skin)
None None None Partial Partial Partial Full
    14.9179 53.0282 15.4268 30.28732 15.33803 57.26197 16.57887 32.7211
Full Full Full
    45.6479 73.75321 15.80845 32.91955
```

```
R skin.expected <- matrix(rep(colSums(skin),each=kr)*rowSums(skin)/sum(skin),
nrow=kr,ncol=kc,dimnames=dimnames(skin))
```
