The first step of the algorithm is to correct for GC-content biases. Given a bin $i$, its GC-content is defined as the number of G or C base pairs in the bin divided by the bin length, multiplied by 100, and rounded to the nearest integer. For each GC-content $gc \in \{0, \dots, 100\}$, the average read depth $RD_{gc}$ is calculated over bins with the same GC, and then for each bin $i$ the corrected read depth is

```
$$RD^{\text{corrected}} = \frac{RD^{\text{global}}}{RD_{gc}} RD^{\text{raw}}$
```

The next step for each bin is to identify if its RD is close to its left neighbors or its right neighbors. To accomplish this, each bin is represented as the ordered pair $x_i=(i, r_i)$ where $r_i$ is the GC-corrected read depth of the bin $i$. To represent the signal change over the two-dimensional space, a Gaussian kernel is used with the following density function:

```
$$F(x_i) = C \sum_{j\neq i} e^{-\frac{(j-i)^2}{2H_b^2}} e^{-\frac{(r_j-r_i)^2}{2H_r^2}}$
```

where $H_b$ is the number of bins to look at on each side of $i$ (band width for the genomic location), $H_r$ is the band width for the read depth, and $C$ is a constant normalization factor. The mean-shift rectify is the two-dimensional vector of partial derivatives over genome and read depth, respectively. Because only the genome needs partitioned for CNV discovery, only the partial derivative over genome needs to be considered:

```
$$\frac{\delta F}{\delta i}(x_i) = C' \sum_{j\neq i} (j-i) \exp\left(-\frac{(j-i)^2}{2H_b^2}\right) \exp\left(-\frac{(r_j-r_i)^2}{2H_r^2}\right)$
```

where $C'$ is a normalization that does not need to be calculated in this case because it is always positive and only the sign of the derivative is required. Boundaries of neighbor segments with different count numbers are calculated finding neighbor bins shifting directions to left. Smoothed RD signal is calculated for each segment as the average read depth of the bins within the segment.

To complete this partitioning, the bandwidths $H_b$ and $H_r$ need to be chosen. The bandwidth $r_i$ is calculated as follows:

```
$$H_r^i = \begin{cases} \frac{\bar{r}}{R}H^0 & : r_i > \frac{\bar{r}}{4} \ \frac{H^0}{2} & : r_i \le \frac{\bar{r}}{4} \end{cases}$
```

where $H^0$ is estimated as the average of best of a Gaussian function to distribution read depth across the genome and $\bar{r}$ is the average read depth across the genome. The second case is to prevent $H_r^i$ becoming zero. Choosing the band-width $H_b$ is challenging because large values of $H_b$ reduce sensitivity to call small CNVs and small values of $H_b$ cause partitioning of large CNVs. To overcome this