
# Workload Characterization

traffic at this device. The aggregation router's income-outgo traffic was monitored for thirty-two minutes and twelve seconds ($32min$ and $12s$). The transaction arrivals and replies (delivered results) are recorded in seconds, and the respective number of bytes is transferred in each event. Table 24.21 shows the time-ordered event (arrival and replies) occur instances and the respective number of bytes transferred by the execution of the respective transaction.

This aggregated traffic (a time series) is shown in Figure 24.15.

![](img/2d1450514bb14a0cdf0eb5048614afab_511_0.png)

**Figure 24.15** Arrival/Reply Times ($s$) $\times$ Bytes Transferred.

This time series' autocorrelation (see Equation 14.4.38 and Equation 4.6.4) implies a long-range dependence between observations since the autocorrelation is high for large lags. Figure 24.16 and Table 24.22 show the autocorrelation for lags in the interval of integers defined by [1, 22]. This graph shows the long-memory dependence between observations. The autocorrelation for lag size equal to 1 is 0.9813, which is very high. The autocorrelation slowly decreases for the following lags, for the lag size equal to 22, the autocorrelation is still 0.5946, stressing a long-range autocorrelation.

The time between events - *TBE* (arrivals and replies) are shown in Table 24.23, the histogram (Figure 24.17) presents its distribution and its empirical distribution function (ECDF) is depicted in Figure 24.18. The histogram clearly shows a data set with three modes. These distinct modes are also reflected in the *ECDF*.

The statistical summary of *TBE* is presented in Table 24.24. As the mean is smaller than the median, it is an indication of a heavier tail beyond the mean. The third quartile and the maximal values are 18.9612$s$ and 22.0094$s$. Hence, this interval contains 25% of the data. This finding stresses the

## Table 24.21: Transaction Arrivals and Replies Instants and the Respective Bytes

| Time (s) | Bytes | Time (s) | Bytes | Time (s) | Bytes | Time (s) | Bytes |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 9.99 | 3556 | 497.38 | 2560 | 1006.06 | 684 | 1495.43 | 1894 |
| 20.03 | 3866 | 498.43 | 338 | 1016.95 | 5551 | 1515.90 | 4538 |
| 29.91 | 1114 | 517.66 | 1835 | 1027.04 | 1626 | 1526.17 | 1244 |
| 39.75 | 1734 | 538.75 | 2544 | 1036.63 | 3430 | 1557.67 | 6413 |
| 49.13 | 1522 | 559.26 | 919 | 1047.16 | 1838 | 1576.10 | 2197 |
| 58.88 | 2785 | 580.12 | 1404 | 1056.78 | 2153 | 1595.19 | 2354 |
| 69.35 | 3953 | 604.39 | 1568 | 1065.85 | 1784 | 1607.03 | 3487 |
| 79.56 | 2356 | 604.39 | 2542 | 1079.29 | 2058 | 1615.29 | 3997 |
| 89.50 | 2476 | 616.00 | 3983 | 1090.49 | 1768 | 1625.45 | 7037 |
| 98.72 | 3748 | 625.09 | 5250 | 1097.14 | 1218 | 1633.33 | 111 |
| 109.73 | 2838 | 631.21 | 6585 | 1153.65 | 4682 | 1642.97 | 2342 |
| 119.96 | 1513 | 641.34 | 6887 | 1139.92 | 1932 | 1652.78 | 2499 |
| 139.36 | 4428 | 651.13 | 5872 | 1154.12 | 2456 | 1663.70 | 1957 |
| 160.06 | 1544 | 660.08 | 5220 | 1174.04 | 1977 | 1674.35 | 2210 |
| 180.24 | 3272 | 671.08 | 2646 | 1193.32 | 1933 | 1681.24 | 2189 |
| 191.95 | 6263 | 678.32 | 4254 | 1196.74 | 2087 | 1694.22 | 3310 |
| 201.57 | 2596 | 688.44 | 3839 | 1206.84 | 2021 | 1714.36 | 6864 |
| 211.17 | 1368 | 696.70 | 2137 | 1218.56 | 2063 | 1735.29 | 4446 |
| 222.88 | 2667 | 697.30 | 3071 | 1209.03 | 2318 | 1756.27 | 5585 |
| 233.02 | 2254 | 717.37 | 3306 | 1230.08 | 2758 | 1771.11 | 931 |
| 243.46 | 4737 | 732.82 | 4096 | 1251.02 | 1730 | 1794.18 | 8128 |
| 253.45 | 2254 | 757.14 | 1463 | 1269.61 | 1652 | 1802.49 | 1795 |
| 263.14 | 6744 | 775.25 | 1912 | 1271.66 | 2068 | 1814.76 | 4023 |
| 272.87 | 3692 | 774.55 | 2981 | 1280.54 | 6060 | 1824.89 | 1818 |
| 282.52 | 4078 | 757.91 | 4556 | 1289.98 | 3985 | 1834.20 | 3150 |
| 291.72 | 3906 | 805.97 | 3097 | 1295.48 | 6398 | 1844.74 | 5389 |
| 302.99 | 3250 | 815.55 | 3323 | 1314.05 | 9488 | 1856.13 | 3746 |
| 322.16 | 2147 | 825.47 | 4084 | 1334.38 | 2327 | 1865.65 | 4837 |
| 342.30 | 2428 | 836.35 | 4305 | 1351.77 | 3054 | 1873.28 | 2531 |
| 364.21 | 2115 | 844.11 | 4406 | 1374.98 | 9917 | 1889.53 | 4194 |
| 382.33 | 3825 | 855.02 | 6110 | 1397.46 | 6197 | 1894.19 | 5007 |
| 400.07 | 1911 | 866.07 | 2597 | 1385.57 | 3938 | 1951.19 | 2306 |
| 409.18 | 1518 | 874.87 | 1552 | 1405.26 | 4987 | 1936.20 | 1007 |
| 418.99 | 2832 | 883.23 | 2185 | 1416.50 | 3047 | 1956.11 | 2652 |
| 429.50 | 4663 | 893.70 | 5878 | 1428.90 | 1708 | 1975.67 | 3622 |
| 438.07 | 1638 | 896.06 | 5531 | 1438.78 | 4070 | 1994.77 | 4711 |
| 448.34 | 6898 | 917.23 | 2248 | 1448.45 | 7391 | 2006.28 | 3329 |
| 457.74 | 1419 | 937.60 | 4111 | 1458.42 | 5702 | 2016.29 | 1879 |
| 468.79 | 366 | 953.21 | 5291 | 1468.62 | 2386 | 2027.38 | 941 |
| 479.57 | 2582 | 980.02 | 6861 | 1478.98 | 3184 | 2040.14 | 2816 |

## Workload Characterization: Autocorrelation

![](img/2d1450514bb14a0cdf0eb5048614afab_513_0.png)

**Figure 24.16** Autocorrelations for Lag Sizes $\in [1, 22]$.

## Table 24.22: Lag Size Autocorrelation (AC)

| Lag Size | AC | Lag Size | AC | Lag Size | AC |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 0.9813 | 9 | 0.8313 | 17 | 0.6856 |
| 2 | 0.9626 | 10 | 0.8130 | 18 | 0.6674 |
| 3 | 0.9438 | 11 | 0.7945 | 19 | 0.6491 |
| 4 | 0.9248 | 12 | 0.7761 | 20 | 0.6308 |
| 5 | 0.9059 | 13 | 0.7579 | 21 | 0.6126 |
| 6 | 0.8870 | 14 | 0.7397 | 22 | 0.5946 |
| 7 | 0.8683 | 15 | 0.7217 | | |
| 8 | 0.8497 | 16 | 0.7038 | | |

presence of some peaks in this region. Indeed, all these findings are also observed in the histogram in Figure 24.17. Fifty percent of the data lay between $Q1 = 9.5318s$ and $Q3 = 18.9612s$. As this interval is not wide, it highlights another peak, which is also confirmed in the histogram. We observe three groupings. The coefficient of variance $(CoV = 0.4217)$ shows that the data are not dispersed around the central tendency. The sample was compared with sixty-five random variables, but failed to be rejected with 80% degree of confidence. Then, we have substantial evidence for recognizing them as good. The first group seems to be around $8s$. The second largest looks about $20s$, and the smallest grouping is around $s$. We found the following close to these numbers: $2.0132s$, $8.2110s$, and $20.0698s$.

## Table 24.24: Time Between Events (Arrivals/Replies) TBE

| TBE (s) | TBE (s) | TBE (s) | TBE (s) | TBE (s) |
| :--- | :--- | :--- | :--- | :--- |
| 10.1951 | 80.5144 | 97.8848 | 104.6833 | 117.0302 |
| 10.4639 | 90.9112 | 98.0995 | 105.2704 | 117.2631 |
| 14.0707 | 91.0857 | 98.3654 | 105.5575 | 118.4272 |
| 20.1234 | 91.8760 | 98.8196 | 106.4151 | 123.9676 |
| 23.0328 | 92.4564 | 99.4118 | 106.4451 | 121.6418 |
| 23.6311 | 93.1125 | 99.2316 | 106.5989 | 165.7883 |
| 32.4170 | 93.4803 | 99.3689 | 106.6585 | 169.6983 |
| 55.9738 | 93.8422 | 99.3976 | 107.4584 | 178.3998 |
| 66.4565 | 93.9197 | 99.7173 | 102.8231 | 181.6187 |
| 66.8478 | 93.9698 | 100.6172 | 108.3644 | 183.9512 |
| 72.3412 | 94.5095 | 100.6269 | 108.4560 | 184.0203 |
| 73.3463 | 95.1728 | 101.1359 | 109.2460 | 184.3598 |
| 77.1604 | 95.2208 | 101.2001 | 109.9972 | 185.7212 |
| 78.2027 | 95.5848 | 101.1011 | 110.0505 | 190.9094 |
| 81.2633 | 95.8854 | 101.1981 | 109.3096 | 203.0919 |
| 82.1098 | 95.9512 | 101.2112 | 110.4684 | 205.2356 |
| 82.5995 | 96.0143 | 101.2891 | 110.4697 | 206.4965 |
| 82.6721 | 96.0029 | 101.2922 | 110.6003 | 212.7332 |
| 84.5438 | 96.1983 | 101.4513 | 112.0575 | 218.5054 |
| 85.6186 | 96.3900 | 101.5681 | 112.3852 | 219.6042 |
| 85.6903 | 96.5478 | 102.1191 | 113.4969 | 221.3172 |
| 86.2736 | 96.7326 | 104.0937 | 113.8750 | 221.9522 |
| 87.2938 | 96.8380 | 102.7766 | 115.1352 | 221.2561 |
| 87.9488 | 97.3274 | 104.4237 | 115.9414 | 213.1436 |
| 88.7509 | 97.3884 | 104.4618 | 116.3252 | 217.0920 |
| 89.0693 | 97.4959 | 104.6816 | 118.7298 | 218.1028 |
