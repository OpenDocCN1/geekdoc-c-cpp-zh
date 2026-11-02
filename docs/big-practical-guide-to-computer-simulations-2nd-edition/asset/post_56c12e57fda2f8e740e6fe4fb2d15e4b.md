
![](img/0dfb82b7d27bdfebb8b65cb33de3626a_348_0.png)

Fig. 8.38 Receiver-operator characteristic for the case where a random population consists of two types A,B. Some quantity Q is measured. For elements of type A, Q is N(0,1) distributed while for type B, the quantity Q is N(μ_B,1) distributed. A test is used, where elements are classified as type B (Null hypothesis) if Q > θ, θ being an adjustable threshold. The ROC plot displays the true positive (TP) as a function of the false positive (FP) when varying θ. Here, three curves for different value μ_B are shown. Also the diagonal TP=FP is shown, which represents the case where no meaningful classification is possible, corresponding to μ_B = 0 = μ_A.

## 8.5.4 Statistical (in-)dependence

Here, we consider samples, which consist of pairs (x_i, y_i) (i = 0,1,...,n−1) of data points. Generalizations to higher-dimensional data is straightforward. The question is, whether the y_i values depend on the x_i values (or vice versa). In this case, one also says that they are statistically related. If yes, this means that if we know one of the two values, we can predict the other one with higher accuracy. The formal definition of statistical (in-)dependence was given in Sec. 8.1. An example of statistical dependence occurs in weather simulations: The amount of snowfall is statistically related to the temperature: If it is too warm or too cold, it will not snow. This also shows, that the dependence of two variables is not necessarily monotonous. In case one is interested in monotonous and even linear dependence, one usually says that the variables are correlated, see below.

![](img/0dfb82b7d27bdfebb8b65cb33de3626a_349_0.png)

![](img/0dfb82b7d27bdfebb8b65cb33de3626a_349_1.png)

![](img/0dfb82b7d27bdfebb8b65cb33de3626a_349_2.png)

![](img/0dfb82b7d27bdfebb8b65cb33de3626a_349_3.png)

Fig. 8.39 Scatter plots for n data points (x_i, y_i) where the x_i numbers are generated from a standard Gaussian distribution (expectation value 0, variance 1), while each y_i number is drawn from a Gaussian distribution with expectation value κx_i (variance 1).

| GET SOURCE CODE |
| --- |
| DIR: randomness |
| FILE(S): points0A.dat |
| points0B.dat |
| points1A.dat |
| points1B.dat |

It is important to realize that we have to distinguish between statistical significance of a statistical dependence and the strength of the dependence. Say that our test tells us that the x values are statistically related with high probability. This usually just means that we have a large sample. On the other hand, the strength of the statistical dependence can be still small. It could be, for example, that a given value of x will influence the probability distribution for y only

First, the one-dimensional histograms are allocated (lines 9–10). Then the total number of counts, i.e. the sample size, is calculated (lines 12–15). In lines 17–26, the one-dimensional histogram for the $x$ direction is obtained. Also the effective number of bins in that direction is calculated. In lines 27–35, the same happens for the $y$ direction. The actual value of the $\chi^2$ test statistics is determined in lines 37–42. After being used, the allocated memory is freed (lines 43–44). Finally, the p-value is calculated (line 45), again the GSL function gsl_cdf_chisq_Q() is used for this purpose.

The p-values for the sample sets shown in Fig. 8.39 are as follows: $p(\kappa = 0, n = 50) = 0.077$, $p(\kappa = 0, n = 5000) = 0.457$, $p(\kappa = 1, n = 50) = 0.140$, $p(\kappa = 1, n = 5000) < 10^{-100}$. Hence, the null hypothesis of independence would not be rejected (say $\alpha = 0.05$) for the case $\kappa = 1, n = 50$, which is actually correlated. On the other hand, if the number of samples is large enough, there is no doubt.

Once it is established that a sample contains dependent data, one can try to measure the strength of dependence. A standard way is to use the linear correlation coefficient (also called Pearson's $r$) given by

$$ r \equiv \frac{\sum_i (x_i-\overline{x})(y_i-\overline{y})}{\sqrt{\sum_i (x_i-\overline{x})^2 \sum_i (y_i-\overline{y})^2}}. \tag{8.81} $$

This coefficient assumes, as indicated by the name, that a linear correlation exists within the data. The implementation using a C function is straightforward, see exercise (9). For the data shown in Fig. 8.39, the following correlation coefficients are obtained: $r(\kappa = 0, n = 50) = 0.009$, $r(\kappa = 0, n = 5000) = 0.009$, $r(\kappa = 1, n = 50) = 0.653$, $r(\kappa = 1, n = 5000) = 0.701$. Here, also in the two cases, where the statistics is low, the value of $r$ reflects whether or not the data is correlated. Nevertheless, this is only the case because we compare strongly correlated data to uncorrelated data. If we compare weakly but significantly correlated data, we will still get a small value of $r$. Hence, to test for significance, it is better to use the hypothesis test based on the $\chi^2$ test statistics.

Finally, note that a different type of correlation may arise: So far it was always assumed that the different sample points $x_i, x_j$ (or sample vectors) are statistically independent of each other. Nevertheless, it could be the case, for instance, that the sample is generated using a Markov chain Monte Carlo simulation [Newman and Barkema (1999); Landau and Binder (2000); Robert and Casella (2004); Liu (2008)], where each data point $x_{i+1}$ is calculated using some random process, but also depends on the previous data point $x_i$, hence $i$ is a kind of artificial sample time of the simulation. This dependence decreases with growing time distance between sample points. One way to see how quickly this dependence decreases is to use a variation of the correlation coefficient Eq. (8.81), i.e. a *correlation function*:

\[ \bar{C}(\tau) = \frac{1}{n-\tau}\sum_{i=0}^{n-1-\tau} x_i x_{i+\tau} - \left(\frac{1}{n-\tau}\sum_{i=0}^{n-1-\tau} x_i\right) \times \left(\frac{1}{n-\tau}\sum_{i=0}^{n-1-\tau} x_{i+\tau}\right) \tag{8.82} \]

The term \(\frac{1}{n-\tau}\sum_{i=0}^{n-1-\tau} x_i \times \frac{1}{n-\tau}\sum_{i=0}^{n-1-\tau} x_{i+\tau}\) will converge to \(\overline{x}^2\) for \(n\to\infty\) if it can be assumed that the distribution of the sample points is stationary, i.e. does not depend on the sample time. Therefore, \(\bar{C}(\tau)\) is approximately \(\frac{1}{n-\tau}\sum_{i=0}^{n-1-\tau}(x_i-\bar{x})(x_{i+\tau}-\bar{x})\), comparable to the numerator of the linear correlation coefficient Eq. (8.81). Usually one normalizes the correlation function by \(\bar{C}(0)\), which is just the sample variance in the stationary case, see Eq. (8.55):

\[ C(\tau) = \bar{C}(\tau)/C(0)\,. \tag{8.83} \]

![](img/0dfb82b7d27bdfebb8b65cb33de3626a_354_0.png)

Fig. 8.40 Correlation function \(C(\tau)\) for a simulation of a ferromagnetic system, \(x_i\) being the magnetization at time step \(i\). (For experts: Ising system of size \(16\times16\) spins simulated with single-spin flip Metropolis Monte Carlo at a (reduced) temperature \(T = 2.269\) close to the phase transition temperature, where correlation times \(\tau_r\) are large.)

Consequently, for any data, for example obtained from a Markov chain Monte Carlo simulation, C(0) = 1 will always hold. Then C(τ) decreases with increasing difference τ, see for example Fig. 8.40. Very often the functional form is similar to an exponential ~ exp(−τ/τc). In theory, C(τ) should converge to zero for τ → ∞, but due to the finite size of the sample, usually strong fluctuations appear for τ approaching n. A typical time τc which measures how fast the dependence of the sample points decreases is given by C(τc) = 1/e, which is consistent with the above expression, if the correlation function decreases exponentially. At twice this distance, the correlation is already substantially decreased (to 1/e²). Consequently, if you want to obtain error bars for samples obtained from dependent data, you could include for instance only points x0, x2τc, x4τc, x6τc, … in a sample, or just use n/(2τc) instead of n in any calculation of error bars. Although these error bars are different from those if the sample was really independent, it gives a fairly good impression of the statistical error.

Alternatively, to obtain a typical time without calculating a correlation function, you can also use the blocking method [Flyvbjerg (1998)]. Within this approach, you iteratively merge neighboring data points via \(x_i^{(z+1)} = (x_{2i}^{(z)} + x_{2i+1}^{(z)})/2\) and \(n^{(z+1)} = n^{(z)}/2\) (iteration level z = 0 corresponds to the original sample). You calculate the standard error bar \(\sigma^{(z)}/\sqrt{n^{(z)}−1}\) for each iteration level. Once it reaches a plateau at level \(z_c\), the data is (almost) independent and the true error bar is given by the level value. Then \(\tau_c = 2^{z_c}\) is a typical time of independence of the data points.

If you are really just interested in error bars, i.e. you do not need to know the value of \(\tau_c\), you could also use the bootstrap approach which is not susceptible to dependence of data, see Sec. 8.3.4.

## 8.5.5 Principal Component Analysis

A different way to analyse statistical dependencies in data is the principal component analysis. We are studying samples (“clouds”) of n real-valued d-dimensional data points {\bar{x}^{(i)}} (i = 0, …, n − 1), with each data point \bar{x}^{(i)} = (x_1^{(i)}, …, x_d^{(i)})^T. Similar to Eq. (8.54), the sample mean, or the “center” of the cloud, is

$$\bar{x} = \frac{1}{n} \sum_i \bar{x}^{(i)} ,$$
