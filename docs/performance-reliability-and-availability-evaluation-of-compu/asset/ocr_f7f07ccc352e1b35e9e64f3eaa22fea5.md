# Workload Characterization

# 489

![](bbox=[0.138, 0.101, 0.463, 0.24])

![](bbox=[0.517, 0.101, 0.863, 0.24])

(a) tps

(b) kB_wrtn/s

![](bbox=[0.313, 0.282, 0.663, 0.421])

(c) kB_wrtn

**Figure 24.11** Correlations between %system and tps, kB_wrtn/s and kB_wrtn.

reject normal distribution with mean $\mu = 9.77\%$, and the standard deviation $\sigma = 1.94\%$ is a suitable distribution to represent %system. The Kolmogorov-Smirnov goodness of fit also failed to represent the triangular distributions $Tr(40.431 	imes 10^3 \text{ kB/s}, 103.67 	imes 10^3 \text{ kB/s}, 99.201 	imes 10^3 \text{ kB/s})$ and $Tr(20.160 	imes 10^3 \text{ kB/s}, 518.350 	imes 10^3 \text{ kB/s}, 103 	imes 10^3 \text{ kB/s}, 496.07 	imes 10^3 \text{ kB/s})$ for representing kB_wrtn/s and kB_wrtn, respectively. For all goodness of fit tests, we found no evidence to reject the distribution even considering a degree of confidence of 80%. Figure 24.12 shows the respective probability density function of each random variable.

**Example 24.3.3.** Suppose a web client access a web-server in a data center to execute a set of services. The web-server took to process each service required in each request is shown in Table 24.14. The statistical summary of the sample is shown in Table 24.15. The histogram of the sample, depicted in Figure 24.13, shows a multimodal data set. The Coefficient of Range (CoR) for (see Definition 3.3.2) is

```
$CoR = \frac{M - m}{M + m}$
$$CoR = \frac{415.24 - 38.75}{415.24 + 38.75} = 0.83,$$
```