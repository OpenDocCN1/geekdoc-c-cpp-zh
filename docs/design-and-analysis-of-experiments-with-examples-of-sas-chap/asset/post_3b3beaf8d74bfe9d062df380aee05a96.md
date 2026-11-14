
Where

```
y = \begin{pmatrix} y_{11} \\ y_{12} \\ y_{13} \\ y_{14} \\ y_{21} \\ y_{22} \\ y_{23} \\ y_{24} \\ y_{31} \\ y_{32} \\ y_{33} \\ y_{34} \end{pmatrix}, X = \begin{pmatrix} 1 & 1 & 0 & 0 \\ 1 & 1 & 0 & 0 \\ 1 & 1 & 0 & 0 \\ 1 & 1 & 0 & 0 \\ 1 & 0 & 1 & 0 \\ 1 & 0 & 1 & 0 \\ 1 & 0 & 1 & 0 \\ 1 & 0 & 1 & 0 \\ 1 & 0 & 0 & 1 \\ 1 & 0 & 0 & 1 \\ 1 & 0 & 0 & 1 \\ 1 & 0 & 0 & 1 \end{pmatrix}, \beta = \begin{pmatrix} \mu \\ \tau_1 \\ \tau_2 \\ \tau_3 \end{pmatrix}, \epsilon = \begin{pmatrix} \epsilon_{11} \\ \epsilon_{12} \\ \epsilon_{13} \\ \epsilon_{14} \\ \epsilon_{21} \\ \epsilon_{22} \\ \epsilon_{23} \\ \epsilon_{24} \\ \epsilon_{31} \\ \epsilon_{32} \\ \epsilon_{33} \\ \epsilon_{34} \end{pmatrix},
```

and \(\epsilon \sim MVN(0, \sigma^2 I)\).

The least squares estimators for \(\beta\) are the solution to the normal equations \(X'X\hat{\beta} = X'y\). The problem with the normal equations is that \(X'X\) is singular and cannot be inverted. The solution to this problem using the SAS proc glm is to partition the \(X\) matrix as:

```
X = \begin{pmatrix} 1 & 1 & 0 & 0 \\ 1 & 1 & 0 & 0 \\ 1 & 1 & 0 & 0 \\ 1 & 0 & 1 & 0 \\ 1 & 0 & 1 & 0 \\ 1 & 0 & 1 & 0 \\ 1 & 0 & 1 & 0 \\ 1 & 0 & 0 & 1 \\ 1 & 0 & 0 & 1 \\ 1 & 0 & 0 & 1 \\ 1 & 0 & 0 & 1 \\ 1 & 0 & 0 & 1 \end{pmatrix} = [X_1 \ X_2]
```

Then \(X'X\) can be written in partitioned form as:

```
X'X = \begin{bmatrix} X_1'X_1 & X_1'X_2 \\ X_2'X_1 & X_2'X_2 \end{bmatrix}, \text{ and } X_1'X_1 \text{ is non-singular. Therefore } X'X^- = \begin{bmatrix} X_1'X_1^{-1} & 0 \\ 0 & 0 \end{bmatrix}
```

is a generalized inverse for \(X'X\), and \(\hat{\beta} = (X'X)^- X'y\) is a solution that is equivalent to the estimates that would be obtained with the restriction that \(\beta_1 = 0\) (see Freund and Littell, 1981). For the example with \(t = 3\) factor levels and \(r_i = 4\) replicates for \(i = 1, ..., t\),

```
\beta = \begin{pmatrix} \mu \\ \tau_1 \\ \tau_2 \\ \tau_3 \end{pmatrix}, \hat{\beta} = \begin{pmatrix} \hat{\mu} + \hat{\tau}_3 \\ \hat{\tau}_1 - \hat{\tau}_3 \\ \hat{\tau}_2 - \hat{\tau}_3 \\ 0 \end{pmatrix}
```

### 2.4.2 L.S. Calculations with SAS proc glm

Table 2.1 shows the data from a CRD design for the bread rise experiment described earlier in this chapter.

| Rise Time | Loaf Heights |
| :--- | :--- |
| 35 minutes | 4.5, 5.0, 5.5, 6.75 |
| 40 minutes | 6.5, 6.5, 10.5, 9.5 |
| 45 minutes | 9.75, 8.75, 6.5, 8.25 |

Using these data we have

\( X'X = \begin{pmatrix} 12 & 4 & 4 & 4 \\ 4 & 4 & 0 & 0 \\ 4 & 0 & 4 & 0 \\ 4 & 0 & 0 & 4 \end{pmatrix}, \quad X'y = \begin{pmatrix} 88.0 \\ 21.75 \\ 33.0 \\ 33.25 \end{pmatrix} \)

and

\( X'X^{-1} = \begin{pmatrix} 0.25 & -0.25 & -0.25 & 0 \\ -0.25 & 0.50 & 0.25 & 0 \\ -0.25 & 0.25 & 0.50 & 0 \\ 0 & 0 & 0 & 0 \end{pmatrix}, \quad \hat{\beta} = (X'X)^{-1}X'y = \begin{pmatrix} 8.3125 \\ -2.8750 \\ -0.0625 \\ 0.0000 \end{pmatrix} \)

The SAS commands to read in this data and compute these estimates are:

```
/* Reads the data from compact list */
/* data bread; */
input time h1-h4;
height=h1; output;
height=h2; output;
height=h3; output;
height=h4; output;
data keep time height;
35 4.5 5.0 5.5 6.75
40 6.5 6.5 10.5 9.5
45 9.75 8.75 6.5 8.25
run;
/* Fits model with proc glm */
proc glm;
class time;
model height=time/solution;
run;
```

These commands read the data in a compact format, like Table 2.1, then use the output statement to create four lines in the file, bread, for each line in the input records. The result of the model /solution; option is:

| Parameter | Estimate |
| :--- | :--- |
| Intercept | 8.312500000 B |
| time 35 | -2.875000000 B |
| time 40 | -0.062500000 B |
| time 45 | 0.000000000 B |

We can see the estimates are the same as those shown above. These parameter estimates are not unique because they depend on the ordering of the class variable time. proc glm recognizes this and designates the estimates as biased by following each value with a B.

### 2.4.3 Estimation of \(\sigma^2\) and distribution of quadratic forms

The estimate of the variance of the experimental error, \(\sigma^2\), is \(ssE/(n-t)\). It is only possible to estimate this variance when there are replicate experiments at each level of the treatment factor. When measurements on sub-samples or duplicate measurements on the same experimental unit are treated as replicates, this estimate can be seriously biased.

In matrix form, \(ssE\) can be written as

\(ssE = y'y - \hat{\beta}'X'y = y'(I - X(X'X)^-X')y,\)

and from the theory of linear models it can be shown that the ratio of \(ssE\) to the variance of the experimental error, \(\sigma^2\), follows a chi-square distribution with \(n-t\) degrees of freedom, i.e., \(ssE/\sigma^2 \sim \chi^2_{n-t}\).

### 2.4.4 Estimable Functions

A linear combination of the cell means is called an estimable function if it can be expressed as the expected value of a linear combination of the responses, i.e.,

\(\sum_{i=1}^t b_i(\mu + \tau_i) = E\left[\sum_{i=1}^t \sum_{j=1}^{r_i} a_{ij} Y_{ij}\right] \quad (2.7)\)

From this definition it can be seen that effects, \(\tau_i\), are not estimable, but a cell mean, \(\mu + \tau_i\), or a contrast of effects, \(\sum c_i \tau_i\), where \(\sum c_i = 0\), is estimable.

In matrix notation \(L\beta\) is a set of estimable functions if each row of \(L\) is a linear combination of the rows of \(X\), and \(L\hat{\beta}\) is its unbiased estimator. \(L\beta\) follows the multivariate normal distribution with covariance matrix \(\sigma^2 L'(X'X)^- L\), and the estimator of the covariance matrix is \(\hat{\sigma}^2 L'(X'X)^- L\). For example using the data from the bread rise experiment above,

\(L = \begin{pmatrix} 0 & 1 & -1 & 0 \\ 0 & 1 & 0 & -1 \end{pmatrix} . \quad (2.8)\)

\(L\beta = \begin{pmatrix} \tau_1 - \tau_2 \\ \tau_1 - \tau_3 \end{pmatrix}, \text{and } L\hat{\beta} = \begin{pmatrix} \hat{\tau}_1 - \hat{\tau}_2 \\ \hat{\tau}_1 - \hat{\tau}_3 \end{pmatrix} = \begin{pmatrix} -2.8025 \\ -2.8750 \end{pmatrix} \text{is a vector}

of contrasts of the effects. The number of degrees of freedom, or number of linearly independent contrasts of effects in a CRD, is always the number of levels of the treatment factor minus one, i.e., t - 1. Whenever there is a set of t - 1 linearly independent contrasts of the effects, they are called a saturated set of estimable contrasts.

It can be shown that \((L\hat{\beta})'(L(X'X)^{-}L')^{-1}(L\hat{\beta})\) follows the noncentral chi-square distribution, \(\chi^2_p(\lambda)\), where the noncentrality parameter

\(\lambda = (\sigma^2)^{-1}(L\beta)'(L(X'X)^{-}L')^{-1}(L\beta),\)

and **L** is the coefficient matrix for an estimable contrast like (2.8), and the degrees of freedom p is equal to the rank of **L**.

Estimable contrasts can be obtained from SAS proc glm using the estimate command. For example to estimate the average difference in the cell means for the first and second levels of the treatment factor, \((\mu + \tau_1) - (\mu + \tau_2) = \tau_1 - \tau_2\), use the command:

```
estimate '1 - 2' time 1 -1;
```

where the string in quotes is the label to be used in the output, time is the name of the treatment factor, and the numbers 1 -1 are the contrast coefficients, c_i. The command:

```
estimate '1 -2 -3' time 1 -1 -1;
```

would produce no output and in the log file the message "1 -2 -3 is not estimable" would be printed, since \(\sum c_i \neq 0\).

### 2.4.5 Hypothesis Test of No Treatment Effects

In the model for the CRD, the statistical hypothesis of interest is \(H_0 : \mu_1 = \mu_2 = ... \mu_t\) or \(\tau_1 = \tau_2 = ... = \tau_t\) versus the alternative \(H_a :\) at least two of the \(\tau\)s differ. If the null hypothesis is true, the model \(y_{ij} = \mu_i + \epsilon_{ij} = \mu + \tau_i + \epsilon_{ij}\) simplifies to \(y_{ij} = \mu + \epsilon_{ij}\) which can be represented as a single normal distribution with mean \(\mu\) and variance \(\sigma^2\) rather than multiple normal distributions like those shown in Figure 2.1.

The sums of squares about the mean is \(ssTotal = \sum_{i=1}^t \sum_{j=1}^{n_i} (y_{ij} - \bar{y}_{\cdot\cdot})^2 = y'y - (1'y)^2/(1'1)\), where \(\bar{y}_{\cdot\cdot}\) is the grand mean and 1 is a column vector of 1s. This sum of squares can be partitioned as:

ssTotal = ssT + ssE (2.9)

where \(ssT = \hat{\beta}'X'y - (1'y)^2/(1'1) = (L\hat{\beta})'(L(X'X)^{-}L')^{-1}(L\hat{\beta})\), and **L** is the coefficient matrix for a saturated set of estimable contrasts. This quantity is called the treatment sums of squares. Under the null hypothesis \(H_0 : \mu_1 = \mu_2 = ... \mu_t\), both ssT and ssE follow the chi-squared distribution. These sums of squares and their corresponding mean squares, which are formed by dividing each sum of squares by its degrees of freedom, are usually presented
