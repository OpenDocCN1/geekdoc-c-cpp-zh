# Vector-Valued (Multivariate) Time Series

This procedure is very similar to the one described in Section 8.1 for testing $H_0: \rho(k)=0$ versus $H_1: \rho(k) \neq 0$. In that case, it should be noted that the significance level $\alpha=0.05$ applies separately for each $k_i$, and it would not be unusual for 5% of $\hat{ho}_{ij}(k)$ to exceed $2(1/\sqrt{n})$ when the null hypothesis is true.

# EXAMPLE 10.5: TESTING WHEN SUNSPOT ACTIVITY AND GLOBAL TEMPERATURE ARE INDEPENDENT

We let $X_i$ denote the annual sunspot numbers ($t_{swfile08.1850}$) and $X_j$ denote the global temperature data ($t_{swfile hadley}$), from 1850 to 2008 as displayed in Figure 10.7. In this example, we will consider these two times to be stationary (see Chapter 9 for alternative models). We showed the estimated cross-correlations, $\hat{ho}_{ij}(k)$ for $k=-20, -19, \dots, -1, 0, 1, \dots, 20$ between annual sunspot numbers and temperature occur at positive lags, with the largest cross-correlation being $\hat{ho}_{ij}(6)=0.271$ This makes intuitive sense, because if there is a relationship, we would expect earth's activity to influence temperature and would not expect that the earth's temperature would have any influence on current or future solar activity. However, the question remains whether an estimated sample correlation of this is significantly different from zero, since, in this case we do not know the asymptotic variance in Equation 10.45. Thus we use

![](bbox=[0.173, 0.546, 0.808, 0.853])

**Figure 10.9** (a) Estimated cross-correlations, $\hat{ho}_{12}(k)$, where $X_1$ is the sunspot data and $X_2$ is global temperature data from 1850 to 2009 and (b) estimated cross-correlations between the residuals from AR models fit to each series.