
As the size of the aggregate model. The intermediate demand after aggregation, $\bar{T}$, is an $m \times m$ square matrix. Each block on the diagonal, $\bar{T}^{rr}$, is an $n(r) \times n(r)$ square matrix. Off-diagonal matrices are basically rectangular, depending on the size of the supply region $r$ and the size of the demand region $s$ after aggregation. For example, the size of $\bar{T}^{rs}$ is $n(r) \times n(s)$.

We define the aggregation matrix as follows:

$$Z = \begin{bmatrix} z(1) & 0 & 0 & 0 \\ 0 & z(2) & 0 & 0 \\ 0 & 0 & \ddots & 0 \\ 0 & 0 & 0 & z(k) \end{bmatrix}$$

Each $z(r)$ on the diagonal is an $n(r) \times n$ block aggregation matrix. Each column of $z(r)$ must have one and only one “1,” with other entries being “0”; and each row must have at least one “1” (can be more than one “1”), with other entries being “0.” The placement of “1”s in a row indicate which sectors in the unaggregated model will be combined into a new sector in the aggregate model. If a matrix is pre-multiplied by $z(r)$, then the rows—but not the columns—of the original matrix are grouped into $n(r)$ sectors. A prime represents the transpose of a matrix or vector. Post-multiplying a matrix by $z(r)'$ will therefore aggregate the columns into $n(r)$ sectors.

The relationships for intermediate demand, final demand, total output, and carbon intensity before and after aggregation are presented as follows:

$$ZTZ' = \bar{T} \qquad (3.4)$$

$$Zx = \bar{x} \qquad (3.5)$$

$$ZF = \bar{F} \qquad (3.6)$$

$$[Z(c \otimes x)] \otimes (Zx)^{-1} = \bar{c} \qquad (3.7)$$

$\otimes$ is the multiplication of corresponding elements. $c$ is a diagonal matrix of carbon intensity for the detailed model with $c^1$, $c^2$, … and $c^k$ on the diagonal. $\bar{c}$ is the corresponding diagonal matrix of carbon intensity after aggregation.

Based on Equation (3.3), we have the following relations for the unaggregated model:

$x=(I-A)^{-1}F=Lf$ (3.8)

The calculation of CFs using MRIO is as follows:

$C\otimes x=C\otimes Lf$ (3.9)

For a particular region $s$, the carbon footprints, $w=\{w_j^s\}$, are calculated as follows:

$w_j^s=\sum_q\left[\left(\sum_i\sum_l c_{lj}^{i}r_{ij}^{q}\right)f_j^{qs}\right]$ (3.10)

For the aggregate model, there are two alternative ways for the calculation of CFs:

### Procedure 1:

$\bar{w}=Zw$ (3.11)

where $w$ is the CFs calculated from the unaggregated model. Because all the information of the unaggregated system is known and Procedure 1 is only a summation of relevant sectoral CFs in the original model, there is no aggregation bias. We define $\bar{w}$ as the “true” value.

### Procedure 2:

In another procedure, we first aggregate the MRIO model based on Equations (3.4) through (3.7). From the aggregated model, we then calculate the CFs:

$\bar{x}=(I-\bar{A})^{-1}\bar{f}=\bar{L}\bar{f}$ (3.12)

$\bar{C}\otimes\bar{x}=\bar{C}\otimes\bar{L}\bar{f}$ (3.13)

$\hat{w}_j^s=\sum_q\left[\left(\sum_i\sum_l\bar{c}_{lj}^{i}\bar{r}_{ij}^{q}\right)\bar{f}_j^{qs}\right]$ (3.14)

where $\hat{w}$ is the CFs calculated from the aggregate model. Procedure 2 is the question at issue in which aggregation bias will occur in the calculations of CFs. We define the discrepancy between $\hat{w}$ and $\bar{w}$ as aggregation error. At region-sectoral level, this is $(\hat{w}_j^s - \bar{w}_j^s)$. In addition, we use error rate, $(\hat{w}_j^s - \bar{w}_j^s)/\hat{w}_j^s$, to assess the relative, rather than the absolute, effects of aggregation. Error rate is used because the magnitude of aggregation errors can be extremely large due to the different economic scales of sectors in a national economy. The aggregation errors of some small sectors, although important to the sectors themselves, can be overlooked when compared with the aggregation errors of large-scale sectors.

## 3.3 RESULTS

To examine aggregation bias, we set aggregation schemes, determined by Z, randomly using Monte Carlo simulation. The procedure includes the following:

- 1. Randomly determine the number of regions in which aggregation will be conducted.
- 2. Randomly determine which regions are selected for conducting aggregation.
- 3. Randomly determine the number of sectors for each selected region.
- 4. Randomly determine which sectors are selected for aggregation in each selected region.

We repeated this procedure 100,000 times and obtained 100,000 randomly determined aggregation matrices $Z_s$. For each $Z_i$, we calculated $\hat{w}^{Z_i} = ((\hat{w})^s Z_i)^T$, $\bar{w}^{Z_i} = ((\bar{w})^s Z_i)^T$, $(\hat{w})^s Z_i - (\bar{w})^s Z_i$, and $[(\hat{w})^s Z_i - (\bar{w})^s Z_i]/(\hat{w})^s Z_i$. Because aggregation is conducted randomly many times, aggregation errors and error rates can be considered random variables.

The unaggregated MRIO model we used for this experiment is the AIO 2000. Because the inputs and outputs of Malaysian “unclassified sector” are all “0”s, which can cause a problem in the calculation of the Leontief inverse, we combined the “unclassified sector” with the “public administration” sector and named it the “unclassified” sector in the new MRIO system. For the calculation of carbon intensity, we used the GTAP-E Database Version 6 (Dimaranan, 2006). The GTAP Database Version 6 is the global database representing the world economy for 87 regions and 57 commodities for the year 2001. GTAP-E Database Version 6 provides the emissions data for corresponding regions and sectors in 2001.

![](img/644775a10ad87164013616d709050cee_83_0.png)

![](img/644775a10ad87164013616d709050cee_83_1.png)

![](img/644775a10ad87164013616d709050cee_83_2.png)

FIGURE 3.1 (continued) Probability distribution of error rates in ten economies.

For aggregated sectors, the error rates of samples showed a wide range, from −479 (aggregation of three sectors in China, i.e., “crude petroleum and natural gas,” “iron and steel,” and “finance and insurance”) to 166 (aggregation of two sectors, “paddy” and “synthetic resins and fiber” in Thailand) (Table 3.2). The mean of error rates ranged from 0.029 (for Korea) to 0.167 (for China). This indicates that, in general, aggregation of the AIO 2000 will have moderate effects on CF accounting; however, the aggregation of some sectors can cause considerable bias.

![](img/644775a10ad87164013616d709050cee_84_0.png)

FIGURE 3.1 (continued) Probability distribution of error rates in ten economies.

For unaggregated sectors, the range of error rates were from −0.876 (for Singapore) to more than 16 (for Indonesia) (Table 3.3), with mean levels between −2% and −5%. The confidence interval showed that, for example, for Indonesia, 95% of the error rates fell in the interval of −0.055 and 0.465 for aggregated sectors.

![](img/644775a10ad87164013616d709050cee_85_0.png)

FIGURE 3.1 (continued) Probability distribution of error rates in ten economies.

### TABLE 3.2 Summary of Error Rates for Aggregated Sectors

| Region | Minimum | Mean | Maximum | Standard Deviation | Confidence Interval Lower 2.5% | Confidence Interval Upper 2.5% |
|---|---:|---:|---:|---:|---:|---:|
| Indonesia | −0.734 | 0.107 | 2.677 | 0.140 | −0.055 | 0.465 |
| Malaysia | −12.176 | 0.037 | 11.471 | 0.162 | −0.126 | 0.377 |
| Philippines | −8.139 | 0.057 | 29.343 | 0.271 | −0.092 | 0.380 |
| Singapore | −0.438 | 0.066 | 1.885 | 0.162 | −0.102 | 0.536 |
| Thailand | −2.941 | 0.044 | 165.589 | 0.713 | −0.099 | 0.326 |
| Mainland China | −478.753 | 0.167 | 119.134 | 2.149 | −0.013 | 0.746 |
| Taiwan | −1.384 | 0.072 | 8.798 | 0.119 | −0.080 | 0.311 |
| Korea | −0.527 | 0.029 | 6.869 | 0.100 | −0.096 | 0.235 |
| Japan | −7.846 | 0.065 | 4.558 | 0.100 | −0.043 | 0.289 |
| USA | −0.355 | 0.092 | 1.574 | 0.088 | −0.007 | 0.310 |

### TABLE 3.3 Summary of Error Rates for Unaggregated Sectors

| Region | Minimum | Mean | Maximum | Standard Deviation | Confidence Interval Lower 2.5% | Confidence Interval Upper 2.5% |
|---|---:|---:|---:|---:|---:|---:|
| Indonesia | −0.733 | −0.023 | 16.585 | 0.162 | −0.398 | 0.113 |
| Malaysia | −0.758 | −0.040 | 5.779 | 0.118 | −0.399 | 0.105 |
| Philippines | −0.669 | −0.042 | 5.309 | 0.100 | −0.318 | 0.108 |
| Singapore | −0.876 | −0.049 | 3.349 | 0.127 | −0.506 | 0.074 |
| Thailand | −0.772 | −0.030 | 6.237 | 0.107 | −0.335 | 0.085 |
| Mainland China | −0.806 | −0.036 | 3.548 | 0.115 | −0.383 | 0.073 |
| Taiwan | −0.595 | −0.031 | 5.072 | 0.094 | −0.234 | 0.140 |
| Korea | −0.681 | −0.025 | 4.338 | 0.066 | −0.175 | 0.075 |
| Japan | −0.694 | −0.038 | 2.906 | 0.074 | −0.247 | 0.034 |
| USA | −0.826 | −0.043 | 3.596 | 0.106 | −0.353 | 0.017 |

The range of confidence intervals were between −0.102 and 0.746 for aggregated sectors, and between −0.506 and 0.14 for unaggregated sectors.

Comparing results for the two groups, and except for a few cases, the range of error rates was larger and the mean levels were higher for the aggregated sectors than for the unaggregated sectors. This indicates that aggregation has more impact on aggregated sectors than on unaggregated sectors. In addition, positive mean values for aggregated sectors indicate that, on average, aggregation of the AIO 2000 led to overestimation of CFs for aggregated sectors. Negative mean values indicate that there is a tendency of underestimation of the CFs for the nonaggregated sectors when other sectors are aggregated.

For individual economies, aggregation of sectors, on average, may influence CF accounting of China, Indonesia, and the USA more than other economies. From the range of error rates and the standard deviation of aggregated sectors, we can find that the aggregation of some sectors in China, Thailand, and the Philippines will have considerable impacts. For Indonesia, the aggregation of sectors within the country will have large effects on some specific unaggregated sectors (Table 3.3).

### 3.3.2 Factors Influencing the Aggregation Effect

As inferred by the ranges and standard deviations of error rates, the aggregation of some specific sectors may have significant impacts on the
