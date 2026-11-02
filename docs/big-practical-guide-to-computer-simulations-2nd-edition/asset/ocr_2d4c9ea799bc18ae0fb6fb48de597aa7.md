# ### 8.5.2 Kolmogorov-Smirnov test

Next, we consider the case where the statistical properties of a sample $\{x_0,x_1,\ldots,x_{n-1}\}$, obtained from a repeated experiment using a continuous random variable, is to be compared to a given distribution function $F_X$. One could, in principle, compare a histogram and a correspondingly binned probability distribution using the chi-squared test explained in the previous section. Unfortunately, the binning is artificial and has an influence on the results (imagine few very large bins). Consequently, the method presented in this section is usually preferred, since it requires no binning. Note that if the distribution function is parameterized and if the parameter is determined by the sample (e.g. by the mean of the data) such that the $F_X$ fits the data best, the methods from Sec. 8.6.2 have to be applied.

The basic idea of the Kolmogorov-Smirnov test is to compare the distribution function to the empirical sample distribution function $F_{\hat X}$ defined in Eq. (8.69). Note that $F_{\hat X}(x)$ is piecewise constant with jumps of size $1/n$ at the positions $x_i$ (assuming that each data point is contained uniquely in the sample).

Here again, one has several choices for the test statistics. For instance, one could calculate the area between $F_X$ and $F_{\hat X}$. Instead, usually just the maximum difference between the two functions is used:

$$d_{\max} \equiv \max_x \left|F_X(x)-F_{\hat X}(x)\right| \tag{8.74}$$

Since the sample distribution function changes only at the sample points, one has to perform the comparison just before and just after the jumps. Thus, Eq. (8.74) is equivalent to

$$d_{\max} \equiv \max_i \left\{ \left|F_X(x_i)-1/n-F_{\hat X}(x_i)\right|, \left|F_X(x_i)-F_{\hat X}(x_i)\right| \right\}$$

This sample statistics is visualized in Fig. 8.36.

The p-value, i.e. the probability of a value of $d_{\max}$ as measured ($d_{\max}^{\text{measured}}$) or worse, given the null hypothesis that the sample is drawn from $F_X$, is approximately given by (see [Press et al. (1995)] and references therein):

$$P(d_{\max} \ge d_{\max}^{\text{measured}}) = Q_{\mathrm{KS}}\left(\left(\sqrt{n}+0.12+0.11/\sqrt{n}\right)d_{\max}^{\text{measured}}\right) \tag{8.75}$$

This approximation is already quite good for $n \ge 8$. Here, the following