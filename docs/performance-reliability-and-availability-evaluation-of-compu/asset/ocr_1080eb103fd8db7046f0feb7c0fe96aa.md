# 538 Performance Reliability, and Availability Evaluation of Computational Systems

$t_i$, presents the time to failure of servers in ascending order. Columns $\hat{R}(t_i)$, $\hat{F}(t_i)$, $\hat{f}(t_i)$, and $\hat{\lambda}(t_i)$ depict the reliability, the cumulative time distribution, and the failure rate at $t_i$, respectively. In this specific study the Functions 25.2.10, 25.2.9, 25.2.11 and 25.2.12 were adopted. From this table, the reliability at $2022h$ is estimated as $\hat{R}(2022h) = 0.2917$. Likewise, $\hat{F}(t)$, $\hat{f}(t)$, and $\hat{\lambda}(t)$ are estimated. The estimated time to failure was MTTF = 134.85h. Adopting bootstrap, a confidence interval for the MTTF was estimated. The confidence interval obtained considering 95% of confidence is MTTF $\$(1016.57h, 1811.27h).

The reliability $\hat{R}(t)$ and the cumulative function $\hat{F}(t)$ are step functions that decreases and increases, respectively, each observed failure time. Consequently, some graph the reliability and cumulative function estimate as step functions. The density estimate $\hat{f}(t_i)$ is well represented by kernel density estimates or the empirical density function, closely related to histograms. Likewise, we plotted the hazard function estimate $\hat{\lambda}(t_i)$. Here, however, for each of these functions $\hat{R}(t_i)$, $\hat{F}(t_i)$, $\hat{f}(t_i)$, and $\hat{\lambda}(t_i)$, we each point and connect them with line segments. Figure 25.4 $\hat{R}(t_i)$, $\hat{F}(t_i)$, $\hat{f}(t_i)$, and $\hat{\lambda}(t_i)$.

![](bbox=[0.147, 0.433, 0.852, 0.743])

**Figure 25.4** $\hat{R}(t_i)$, $\hat{F}(t_i)$, $\hat{f}(t_i)$ and $\hat{\lambda}(t_i)$ - Ungrouped Complete Data.

Assume one is interested in estimating the reliability at $t_j$, where $t_j$ is not a failure time recorded and $t_i < t_j < t_{i+1}$. Consider $t_i$ and $t_{i+1}$ are failure time during the observation. One of the simplest approaches is adopting a linear interpolation between