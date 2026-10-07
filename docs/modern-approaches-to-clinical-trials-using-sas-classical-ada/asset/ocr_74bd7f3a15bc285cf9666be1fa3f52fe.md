The method of Lehacher and Wassmer can be viewed as a special case of combination function (3.1) with equal weights $w_1$ and $w_2$, based on the sum of standardized Wald statistics obtained at the end of the trial [30]. The method of Cui, Hung, and Wang (discussed in detail in the next section) is also a special case where the second half of the trial is down-weighted in situations where the sample size is increased [22].

The above p-value combination tests do not rely on any particular rule for sample size adaptation, as long as sample size increase is the only change. Bauer and Köhne [25] recommended Stage 2 sample size adjustment for Fisher's combination test using a conditional power argument

$Pr\sigma(\text{reject } H_0 \text{ at the end } i \text{ interim data}) = Pr\sigma(p_2 < (c_\alpha / p_1) \text{ interim data})$

where the Stage 2 p-value $p_2$ is calculated using the Stage 2 data only (i.e. from $2(M-n)$ subjects based on adjusted final sample size $2M$). The final sample size is selected by equating the conditional power to some reasonable number (e.g. 80%) and solving for $M$.

# 3.3.3.2 CHW Procedure as a Special Case of the Combination Test

The method of Cui, Hung, and Wang (CHW) was originally presented in [22]; we reproduce a simplified description of it here. Suppose an interim analysis with a decision to possibly increase the sample size is conducted after $2n$ patients and the originally planned sample size is $N$ per group. Let $Z_n$ be the normalized test statistic comparing the means of the two treatment groups based on the interim data. Under the null hypothesis $\zeta=0$, the statistic $Z_n$ follows a standard normal distribution. If the sample size does not increase, the test statistic in the final analysis, denoted by $Z_N$, can be written as the weighted sum of the test statistics from the two stages $Z_n$ and $Z_{N-n}$:

$Z_N = \sqrt{\frac{n}{N}}Z_n + \sqrt{\frac{N-n}{N}}Z_{N-n}$.

If after the interim analysis, the sample size is increased to $M(M>N)$ per group, the same statistic becomes