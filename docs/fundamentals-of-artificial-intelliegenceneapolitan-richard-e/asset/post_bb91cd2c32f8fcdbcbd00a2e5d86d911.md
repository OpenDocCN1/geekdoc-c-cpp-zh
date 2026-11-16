
## Section 10.2

**Exercise 10.3** Consider the parameter $p_0$ in Equality 10.1. Do larger values of $p_0$ place more importance on exploitation or exploration?

**Exercise 10.4** Implement the ant colony system (ACS) discussed in Section 10.1.2. Investigate ways to improve it.

**Exercise 10.5** Recall from Section 10.2 that the attraction for a school by an isolated fish is given by the following formula $c = kN^t$, where $c$ and $t$ are constant and $N$ is the number of fish in the school. Investigate the behavior of this function for $t < 1$ and for $t > 1$. When is the effect of adding another fish less pronounced as $N$ increases, and when is it more pronounced?

**Exercise 10.6** Consider Reynolds’ three rules for guiding the behavior of a boid, which appear in Section 10.2. For each rule, discuss the behavior of the boid if that rule was not present and the other two rules were present.

## Part IV

## Learning

## Chapter 11

## Learning Deterministic Models

![](img/67fa924962ee21b3590be9f3b10d9fe7_324_0.png)

In Part I (Logical Intelligence), we solved problems using models that represented deterministic relationships. For example, in Section 2.3.1, we introduced decision trees, and we showed how we could use a decision tree to determine the family of a plant from its properties. In Part II (Probabilistic Intelligence), we solved problems using models that represented probabilistic relationships. For example, in Section 6.7, we introduced Promedas, which produces a differential (probabilistic) diagnosis using a set of patient findings such as history data, physical findings, and laboratory data. In both parts, we constructed applications based on human knowledge that might be obtained from an expert in the application area.

In Part III we present methods for learning the models from data. The current chapter concerns learning deterministic models, while Chapters 12 and 13 address learning probabilistic models such as Bayesian networks. Chapter 14 introduces two related types of learning, namely unsupervised learning and reinforcement learning.

### 11.1 Supervised Learning

Artificial intelligence researchers have coined the type of learning discussed in this chapter as “supervised learning.” Supervised learning involves learning a function from a training set. The function maps a variable _x_ (which may be a vector) to a variable _y_, and the training set is a set of known values of (_x_, _y_) pairs. The variables in _x_ are called the predictors, and the variable _y_ is called the target. For example, American Express might be interested in learning the relationship between charges on an American Express card and the number of miles traveled by the card holder. The training set consists of pairs (_x_, _y_), where _x_ is the number of miles traveled by a given card holder in a given year and _y_ is the amount of money charged that year by the card holder. As another example, we may wish to learn a way to determine the family of a plant from a vector of properties of the plant. In this case, the training set consists of pairs (_x_, _y_) where _x_ is a vector of attributes of a given plant and _y_ is the known family of the plant. The function learned is called a model of the underlying system generating that data.

In the first example above, the variable _y_ is continuous; whereas in the second, it is discrete. Next we discuss techniques for handling each of these situations.

### 11.2 Regression

Regression is a standard statistical technique for performing supervised learning when all variables are continuous. It was not developed by the artificial intelligence community, but rather traces its roots to Francis Galton in the 19th century [Bulmer, 2003]. Next, we briefly review linear regression, which is the simplest type of regression. You should consult a statistics text such as [Freedman et al., 2007] for a thorough coverage of regression.

### 11.2.1 Simple Linear Regression

In simple linear regression, we assume we have an independent random variable _X_ and a dependent random variable _Y_ such that

```
y = \beta_0 + \beta_1 x + \epsilon_x, (11.1)
```

where \(\epsilon_x\) is a random variable, which depends on the value _x_ of _X_, with the following properties:

- For every value _x_ of _X_, \(\epsilon_x\) is normally distributed with 0 mean

# Table 11.1 Miles and Dollars for 25 American Express Card Holders

| Cardholder | Miles (X) | Dollars (Y) |
|---|---|---|
| 1 | 1211 | 1802 |
| 2 | 1345 | 2405 |
| 3 | 1422 | 2005 |
| 4 | 1687 | 2511 |
| 5 | 1849 | 2332 |
| 6 | 2026 | 2305 |
| 7 | 2133 | 3016 |
| 8 | 2253 | 3385 |
| 9 | 2400 | 3090 |
| 10 | 2468 | 3694 |
| 11 | 2699 | 3371 |
| 12 | 2806 | 3998 |
| 13 | 3082 | 3555 |
| 14 | 3209 | 4692 |
| 15 | 3466 | 4244 |
| 16 | 3643 | 5298 |
| 17 | 3852 | 4801 |
| 18 | 4033 | 5147 |
| 19 | 4267 | 5738 |
| 20 | 4498 | 6420 |
| 21 | 4533 | 6059 |
| 22 | 4804 | 6426 |
| 23 | 5090 | 6321 |
| 24 | 5233 | 7026 |
| 25 | 5439 | 6964 |

- For every value x of X, \(\epsilon_x\) has the same standard deviation \(\sigma\)

- The random variables \(\epsilon_x\) for all x are mutually independent

Note that these assumptions entail that the expected value of Y given a value x of X is given by

```
E(Y|X = x) = \beta_0 + \beta_1 x.
```

The idea is that the expected value of Y is a deterministic linear function of x. However, the actual value y of Y is not uniquely determined by the value of X because of a random error term \(\epsilon_x\).

Once we make these assumptions about two random variables, we use simple linear regression to try to discover the linear relationship shown in Equality 11.1 from a random sample of values of X and Y. To estimate the values of \(\beta_0\) and \(\beta_1\), we find the values of b_0 and b_1 that minimize the Mean Square Error (MSE), which is

```
\frac{\sum_{i=1}^n[y_i - (b_0 + b_1 x_i)]^2}{n},
```

where $n$ is the size of the sample, and $x_i$ and $y_i$ are the values of $X$ and $Y$ for the $i$th item in the sample. An example follows.

**Example 11.1** This example is taken from [Aczel and Sounderpandian, 2002]. American Express suspected that charges on American Express cards increased with the number of miles traveled by the card holder. To investigate this matter, a research firm randomly selected 25 card holders and obtained the data shown in Table 11.1. Figure 11.1 shows a scatterplot of the data. We see that it appears that a linear relationship holds between Dollars ($Y$) and Miles ($X$).

The values of $b_0$ and $b_1$ that minimize the MSE are our estimates of $\beta_0$ and $\beta_1$. We do not review how to find the minimizing values here. Any statistics package such as MINITAB, SAS, or SPSS has a linear regression module. If we use one such package to do a linear regression analysis based on the data in Table 11.1, we obtain that

$b_0 = 274.8 \qquad b_1 = 1.26.$

So the linear relationship is estimated to be

$y = b_0 + b_1 x = 274.8 + 1.26 x. \quad (11.2)$

Other information provided by a statistics package, when used to do the linear regression analysis in Example 11.1, includes the following:

| Predictor | Coefficient | SE Coefficient | T | P |
|---|---|---|---|---|
| Constant | $b_0 = 274.8$ | 170.3 | 1.61 | .12 |
| $x$ | $b_1 = 1.255$ | .0497 | 25.25 | 0 |

Briefly, we discuss what each of these quantities means.

- SE coefficient: This quantity, called the **standard error of the coefficient**, enables us to compute our confidence in how close our approximations are to the true values of $\beta_0$ and $\beta_1$ (assuming a linear relationship exists). Recall that for the normal density function, 95% of the mass falls in an interval whose endpoints are the mean $\pm$ 1.96 times the standard deviation. So if $\sigma_0$ is the SE coefficient for $b_0$, we can be 95% confident that

$\beta_0 \in (b_0 - 1.96\sigma_0, b_0 + 1.96\sigma_0).$

In Example 11.1, we can be 95% confident that

$\beta_0 \in (274.8 - 1.96 \times 170.3, 274.8 + 1.96 \times 170.3) = (-58.988, 608.588)$

$\beta_1 \in (1.255 - 1.96 \times .0497, 1.255 + 1.96 \times .0497) = (1.158, 1.352).$

Note that we can be much more confident in the estimate of $\beta_1$.
