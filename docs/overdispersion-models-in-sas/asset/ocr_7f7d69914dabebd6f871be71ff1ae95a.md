# Chapter 3 Quasi-likelihood Functions 71

Step 2: Compare the value of X$^2$ with that of a Chi-square distribution with (n–k) degrees of freedom. If the statistic X$^2$ is unacceptably large, conclude that the intra-cluster correlation is greater than zero, (\theta > 0$) and obtain $\hat{	heta}$ as

```
$$\hat{\theta} = \frac{X^2 - (n-k)}{\sum(m_j-1)(1-v_j^2)}$
```

Step 3: Using the new weights $w_j = [1+(m_j-1)\hat{	heta}^2]^{-1}$, estimate $\hat{eta}$ using the iterative procedure in (3.10). Recalculate the Pearson’s Chi-square statistic X^2$ using equation (3.11).

Step 4: If the X$^2$ is close to (n – k), then conclude that $\hat{	heta}$ is satisfactory and stop the procedure, re-estimate $\hat{	heta}$ using equation (3.12), and go back to Step 3.

As in Williams (1982), we revisit Crowder’s (1978) example to illustrate this methodology. Crowder’s example consisted of a 2x2 factorial experiment with two types of seeds (O. aegyptiaca 75 and 73) and two types of root extracts (bean and cucumber). The outcome is “t”, the number of Seeds that germinated out of “m” seeds. The data are reported in Table 3.7.

# Table 3.7: Seed Germination for Two Types of Seeds (O. aegyptiaca 75 and 73) and Two Types of Root Extracts (Bean and Cucumber)

| Type of Seed | Root Extract | $t_j$ | $m_j$ |
|---|---|---||
| O. aegyptiaca 75 | Bean | 10 | 39 |
| | | 23 | 62 |
| | | 23 | 81 |
| | | 26 | 51 |
| | | 17 | 39 |
| | Cucumber | 5 | 6 |
| | | 53 | 74 |
| | | 55 | 72 |
| | | 32 | 51 |
| | | 46 | 79 |
| | | 10 | 13 |
| O. aegyptiaca 73 | Bean | 8 | 16 |
| | | 10 | 30 |
| | | 8 | 28 |
| | | 23 | 45 |
| | | 0 | 4 |

Morel, Jorge, and Nagaraj Neerajal. Overdispersion Models in SAS®. Copyright 2011, SAS Institute Inc., Cary, North Carolina, USA: ALL RIGHTS RESERVED. For additional SAS resources, visit support.sas.com/publishing.