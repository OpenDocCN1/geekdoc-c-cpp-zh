
# Lifetime Data Analysis

![](img/2d1450514bb14a0cdf0eb5048614afab_571_0.png)

**Figure 25.14 Kaplan-Meier Applied to Ungrouped Complete Data - $\hat{R}(t) \times t$ and $\hat{F}(t) \times t$.** 

# Ungrouped and Censored Data

Now, the Kaplan-Meier method is applied to an ungrouped and censored lifetime data set. Such a data set has censored event times. The events may be of two types: failure or censoring. Hence, as the events are exact, they are not grouped, in each time interval $\Delta t_i$ either $r_i=1$ or $c_i = 1$, such that

$n_{i+1} = n_i - 1$.

Thus, in time intervals $\Delta t_i$ in which occurs a censoring, the term $1 - r_i/n_i = 1 - 0/n_i = 1$. Therefore,

> $$\hat{R}(t_i) = \prod_{j=1}^{i} (1 - \frac{r_j}{n_j}), \quad (25.2.36)$$

From the above, we have $\hat{R}(t_i) = \hat{R}(t_{i-1}) \times (1 - \frac{r_i}{n_i})$.

**Example 25.2.8.** Assume that forty ($n=48$ servers) were observed in operation. The server may fail (Column $r_i=1$) or be censored (Column $c_i=1$). The exact time of each event (failure or censoring) of each server was recorded. Table 25.9 summarizes the recorded data and reliability analysis. Column $t_i$ shows the time to failure. $n_{i+1}$ depicts the number of surviving devices at $t_{i+1}$. The reliability estimate at $t_i$, the cumulative time to failure distribution estimate at $t_i$, the estimate of the time to failure density function at $t_i$, and the estimate of the failure rate at $t_i$ are presented in the respective columns. Column $1/n_i$ shows the impact on the reliability due to the type of event, in the interval $\Delta t_i = t_{i+1} - t_i$. It is worth observing that if the event $i$ is censoring, $1/n_i = 1$.

# Table 25.9 Kaplan-Meier - Ungrouped and Censored Data

| $i$ | $t_i$ | $d_i$ | $n_i$ | $1-d_i/n_i$ | $\hat{R}(t_i)$ | $\hat{f}(t_i)$ | $\lambda(t_i)$ |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 1157.5 | 1 | 42 | 0.97617 | 0.97617 | 0.02083 | 0.00002 |
| 2 | 1582.5 | 1 | 46 | 0.97826 | 0.95832 | 0.01467 | 0.00005 |
| 3 | 1745.6 | 1 | 45 | 0.97826 | 0.93750 | 0.06250 | 0.00134 |
| 4 | 2187.7 | 1 | 45 | 1.00000 | 0.93333 | 0.08333 | 0.00000 |
| 5 | 2533.4 | 1 | 43 | 0.97674 | 0.91667 | 0.08333 | 0.00006 |
| 6 | 2671.6 | 1 | 43 | 0.97722 | 0.89583 | 0.01417 | 0.00015 |
| 7 | 2735.5 | 1 | 42 | 1.00000 | 0.89583 | 0.01417 | 0.00009 |
| 8 | 2773.3 | 1 | 42 | 0.97619 | 0.87433 | 0.01417 | 0.00010 |
| 9 | 2952.1 | 1 | 42 | 0.97684 | 0.87500 | 0.01250 | 0.00012 |
| 10 | 3288.7 | 1 | 41 | 0.97619 | 0.85147 | 0.14458 | 0.00067 |
| 11 | 3501.4 | 1 | 40 | 0.97500 | 0.83333 | 0.16667 | 0.00012 |
| 12 | 3820.8 | 1 | 40 | 1.00000 | 0.83333 | 0.16667 | 0.00000 |
| 13 | 3988.7 | 1 | 40 | 1.00000 | 0.83333 | 0.16667 | 0.00000 |
| 14 | 4196.6 | 1 | 40 | 0.97500 | 0.81333 | 0.16667 | 0.00000 |
| 15 | 4335.3 | 1 | 39 | 0.97500 | 0.79250 | 0.18750 | 0.00009 |
| 16 | 4657.8 | 1 | 38 | 0.97368 | 0.79167 | 0.20833 | 0.00006 |
| 17 | 4870.3 | 1 | 37 | 0.97368 | 0.77297 | 0.22017 | 0.00013 |
| 18 | 4968.3 | 1 | 37 | 0.97297 | 0.75200 | 0.25000 | 0.00028 |
| 19 | 4968.3 | 1 | 35 | 0.97222 | 0.72917 | 0.27083 | 0.09524 |
| 20 | 5219.6 | 1 | 34 | 0.97059 | 0.70643 | 0.26444 | 0.00512 |
| 21 | 5219.9 | 1 | 32 | 0.96070 | 0.66667 | 0.33333 | 0.00217 |
| 22 | 5323.1 | 1 | 32 | 1.00000 | 0.66667 | 0.33333 | 0.00037 |
| 23 | 5440.7 | 1 | 31 | 0.96875 | 0.65483 | 0.35417 | 0.00015 |
| 24 | 5445.8 | 1 | 30 | 0.96754 | 0.65250 | 0.37500 | 0.00464 |
| 25 | 5662.6 | 1 | 29 | 0.96569 | 0.64017 | 0.39583 | 0.00016 |
| 26 | 5772.9 | 1 | 29 | 0.96551 | 0.63433 | 0.43933 | 0.00009 |
| 27 | 6126.4 | 1 | 28 | 0.96552 | 0.61333 | 0.41667 | 0.00009 |
| 28 | 6270.5 | 1 | 27 | 0.96429 | 0.56250 | 0.43750 | 0.00014 |
| 29 | 6307.3 | 1 | 26 | 0.96519 | 0.54517 | 0.45833 | 0.00105 |
| 30 | 6332.9 | 1 | 26 | 1.00000 | 0.54517 | 0.45833 | 0.00000 |
| 31 | 6396.2 | 1 | 25 | 0.96154 | 0.52083 | 0.47917 | 0.00063 |
| 32 | 6447.7 | 1 | 24 | 0.95917 | 0.50000 | 0.50000 | 0.00026 |
| 33 | 6617.3 | 1 | 24 | 0.95900 | 0.49167 | 0.50917 | 0.00008 |
| 34 | 6711.5 | 1 | 23 | 0.95652 | 0.48523 | 0.50833 | 0.00000 |
| 35 | 7497.2 | 1 | 22 | 0.95562 | 0.45817 | 0.54617 | 0.00003 |
| 36 | 8005.1 | 1 | 21 | 0.95435 | 0.45769 | 0.56250 | 0.00009 |
| 37 | 8239.7 | 1 | 20 | 0.95238 | 0.44167 | 0.55833 | 0.00029 |
| 38 | 8380.4 | 1 | 19 | 0.95000 | 0.39583 | 0.60417 | 0.00037 |
| 39 | 8456.7 | 1 | 18 | 0.94500 | 0.37500 | 0.62500 | 0.00027 |
| 40 | 9071.2 | 1 | 18 | 1.00000 | 0.37500 | 0.62500 | 0.00000 |
| 41 | 10272.1 | 1 | 18 | 1.00000 | 0.36250 | 0.62500 | 0.00000 |
| 42 | 10559.1 | 1 | 17 | 0.94414 | 0.35417 | 0.64583 | 0.00020 |
| 43 | 10894.1 | 1 | 16 | 0.94118 | 0.33333 | 0.66667 | 0.00019 |
| 44 | 12015.9 | 1 | 15 | 0.93500 | 0.31250 | 0.68750 | 0.00006 |
| 45 | 12008.4 | 1 | 14 | 0.93333 | 0.29167 | 0.70833 | 0.00105 |
| 46 | 12549.9 | 1 | 13 | 0.93154 | 0.27167 | 0.72917 | 0.00195 |
| 47 | 15183.3 | 1 | 12 | 0.92308 | 0.25000 | 0.75000 | 0.00003 |

# Lifetime Data Analysis

From Table 25.9, we have, the reliability estimate at $t_i$, that $\hat{R}(t_i) = 0.8333$. Interpolation may be adopted for estimating statistics at $t_j$, for $t_{i-1} < t_j < t_i$, $i \in \{1, ..., n\}$. As the data set is censored, the formulas for computing MTTF and standard deviation are not valid since the respective values would be pessimistic. Figure 25.1 depicts the graphs $\hat{R}(t) \times t$ and $\hat{F}(t) \times t$.

![](img/2d1450514bb14a0cdf0eb5048614afab_573_0.png)

There are other nonparametric methods for reliability analysis as the interested readers are referred to [88, 15].

# 25.3 PARAMETRIC METHODS

The last section introduced nonparametric strategies for lifetime data analysis. Now, theoretical distributions are adopted for evaluating reliability and other metrics based on collected lifetime. Therefore, estimating the distribution parameters is a decisive activity for accomplishing such a task. This section introduces three main strategies for estimating probability parameters:

- Graphical methods (Section 25.3.1),
- Methods based on moments (Section 25.3.2), and
- Maximum likelihood methods (Section 25.3.3).

The general process for estimating distribution parameters for reliability analysis consists of the following:

# Performance, Reliability, and Availability Evaluation of Systems

1. Carry out an exploratory data analysis (see Chapter 3) and rule out distributions that clearly do not hold the attributes of the data set. For instance, check the data statistics of centrality, variability, skewness, flatness, moments, failure rate (see Section 6.2 and 25.2) as well as construct graphs as histograms, dot-plots, box-plots, and cumulative empirical distributions and compare with the respective measures and graphs of the candidate distributions. Distributions that are not rejected in this preliminary analysis are considered for the next two steps.

2. Estimate the theoretical distribution parameters using one of those strategies depicted above, and

3. Perform goodness of fit, aiming at evidence to reject the theoretical distribution as a good fit to the empirical data (see Section 6.6).

# 25.3.1 GRAPHICAL METHODS

This section introduces a set of specific graphical methods adopted to estimate parameters of probability distributions. These methods are mainly presented for specific probability distributions. Nevertheless, such a strategy may also be applied to other probability distributions not covered in this section.

# Exponential Distribution

Let us adopt the graphical method for estimating the parameter ($\lambda$) of an exponential distribution. Consider $T$ a random variable exponentially distributed with parameter $\lambda$ representing the failure of a specific class of devices. Assume a failure sample of size $n$ was collected from a population that follows an exponential distribution with parameter $\lambda$; and sort the sample in ascending order such that $S = \{t_1, t_2, ..., t_i, ..., t_n\}$, where $t_1 < t_2 < ... < t_i < ... < t_n$.

The cumulative distribution function of $T$ is

$F(t) = 1 - e^{-\lambda t}$

where $t \ge 0$, and $\lambda \in \mathbb{R}$. From above equation we obtain

$e^{-\lambda t} = 1 - F(t)$.

Applying the natural logarithm to both sides of the above expression we get

$-\lambda t \ln(e) = \ln(1 - F(t))$

$\lambda \ln(e) = -\ln(1 - F(t))$

Since $\ln(e) = 1$ and $\ln(a/b) = \ln(a) - \ln(b)$, and if $a=1$, then $\ln(a) - \ln(b) = -\ln(b) = \ln(1/b)$, then

$\lambda \ln(t) = \ln\left( \frac{1}{1 - F(t)} \right). \quad (25.3.1)$
