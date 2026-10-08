
```
V1DD Skew(const V2DD& v, const int& f); // Skew()
DBL Skew(const V1DD& v, const int& f); // Skew()
V1DD XSkurt(const V2DD& v, const int& f); // XSkurt()
DBL XSkurt(const V1DD& v, const int& f); // XSkurt()
// / ...
// / ...
// Stats.cpp
// / ...

// Skew() - Sample Only
DBL Stats::Skew(const V1DD& v, const int& f = 1)
{
    UINT n = v.size();
    double tmp; // Declare a temporary holding variable

    DBL mean = Mean(v); // Declare a 1D vector of doubles for the Mean
    DBL std = StDevDev(v, 's'); // Declare a 1D vector of doubles for the St. Dev.

    DBL skew; // Declare a 1D vector of doubles for the Skew

    // Calculate Skew Eqn. (3.14)
    tmp = 0.0;
    for (UINT i=0; i<n; i++) {
        tmp += pow((v[i] - mean) / std, 3);
    }
    tmp *= (double)n/((n-1)*(n-2));
    tmp /= sqrt((double)f); // Cast frequency (f) to double
    skew = tmp;

    return skew;
}

// XSkurt() - Sample Only
DBL Stats::XSkurt(const V1DD& v, const int& f = 1)
{
    UINT n = v.size();
    double tmp; // Declare a temporary holding variable

    DBL mean = Mean(v);
    DBL std = StDevDev(v, 's');

    DBL xskurt;

    // Calculate X Skurt. using Eqn. (3.15)
    tmp = 0.0;
    for (UINT i=0; i<v.size(); i++) {
    
    tmp += pow((v[i] - mean / std, 4);
    }

    tmp *= (double)n* (n+1) / ((n-1) * (n-2) * (n-3));
    tmp = 3 * pow((double)(n-1), 2) / ((n-2) * (n-3));
    tmp /= (double)f; // Cast frequency (f) to portfolio
    xskurt = tmp;

    return xskurt;
}
//
```

Figure 7.5 shows a histogram indicating the monthly MVaR figure which is clearly higher when compared to the parametric VaR95 of $1,556,215 for the CTA Index.

## 7.5 EXPECTED SHORTFALL

Apart from the assumption that the P&L distribution is normal, VaR also fails to satisfy one of the concepts of a coherent risk measure. Artzner et al. (1999) have stated that a desirable measure of risk should satisfy four properties or axioms of risk, namely:

- 1. Must be monotonic i.e. if asset X ≥ 0, VaR(X) ≤ 0 i.e. positive returns should not increase risk.
- 2. Must be sub-additive i.e. for assets X1 and X2, VaR(X1 + X2) ≤ VaR(X1) + VaR(X2) i.e. the risk of a portfolio of two assets should not be larger than the risk of the sum of the individual assets. If this were the case, adding assets to a portfolio to reduce risk through diversification would not be possible.
- 3. Must possess positive homogeneity so for any positive number, a, VaR(aX) = aVaR(X) i.e. increasing the size of the portfolio by a times should increase the risk by a multiple of a assuming all assets in the portfolio remain the same in terms of weighting.
- 4. Must be translational invariant that for any real number, a, VaR(X+a) ≤ VaR(X)- a i.e. adding amount of cash (or risk-free asset) to the portfolio should result in a reduction of the risk by any amount a.

Unfortunately, VaR only satisfies three of the axioms of risk; i. it fails to satisfy the sub-additive rule. For this reason, an alternative (and often complementary) measure of VaR was developed known as expected shortfall (ES)¹ which is discussed in detail in Rockafellar and Uryasev (2000).

![](img/2d1ac831a270b8b08f8b8ec2205913dc_277_0.png)

## Figure 7.6 Comparison of ES and VaR at the 95% confidence level

ES does satisfy all the axioms of risk and is considered a coherent risk measure. ES is conditional expectation of loss given that the loss is beyond VaR i.e. the conditional on that exceeding VaR, that is:

$ES_{1-\alpha} = E[-X|-X \geq VaR_{1-\alpha}]$ (7.7)

where $ES_{1-\alpha}$ is the estimated ES at 100($1-\alpha$%) confidence level. $E[X]$ is the conditional expectation of the random variable $X$ given event B i.e. the average loss when VaR is exceeded. Yamai and Yoshida (2002) show that (7.7) can be derived:

```
$ES_{1-\alpha} = E[-X|-X \geq VaR_{1-\alpha}] = \frac{1}{\alpha} \int_{-VaR_{1-\alpha}}^{-\infty} x \frac{1}{\sigma_X\sqrt{2\pi}} e^{-\frac{x^2}{2\sigma_X^2}} dt$
```

```
$= \frac{1}{\alpha} \sigma_X \frac{\phi(-VaR_{1-\alpha}/\sigma_X)}{\sqrt{2\pi}} - \frac{\sigma_X^2}{2\alpha} \frac{\phi(-VaR_{1-\alpha}/\sigma_X)}{\sqrt{2\pi}} = \frac{\sigma_X^2 q_a^2}{2\alpha}$ (7.8)
```

where $I_A$ is the indicator function whose value is 1 when A is true and 0 when A is false, and $q_a$ is the $100^{th}$ percentile of the normal distribution. VaR, the P&L distribution does not have the problems pointed out by Artzner et al. (1999) and such VaR does not have the issue of left-tail risk. That is, ES and VaR are simply scalar multiples of each other because they are scalar multiples of the standard deviation, $\sigma$. For example, VaR at 95% confidence level is $-1.645\sigma$, while ES at the confidence level is $-2.063\sigma$ as shown in Figure 7.6.

## TABLE 7.3 ES critical values for 95% and 99% confidence

| c | α = (1 - c) | Critical value (zα) |
| :--- | :--- | :--- |
| 95% | 5% | -2.0627128 |
| 99% | 1% | -2.6652142 |

Table 7.3 shows the most common confidence levels at 95% and 99% and their associated values $z_\alpha$ for the ES. Note that both $z_{ES5}$ and $z_{ES1}$ have been negated to be consistent with the critical values for VaR and to indicate a loss in the left-tail of the P&L distribution. Using the standard formula for $VaR_{1-\alpha}$ from (7.2), we have similarly:

$ES_{1-\alpha} = \mu + z_{ES}\sigma$ (7.9)

where $ES_{\alpha}$ is the critical value from a normal distribution at the required significance level, $\alpha$. This gives the estimate of the ES in the left-tail of the P&L distribution but could be further along the distribution. Since ES is by definition more than VaR, ES is a more conservative estimate of VaR and thus it is often used as complement to traditional VaR measures. Source 7.7 shows that monthly $ES_{\alpha}$ is 2.1835.

## SOURCE 7.7: MONTHLY VaR AT 95% CONFIDENCE LEVEL USING ES

```
// ...
// RMetrics.h
// ...

DBL ExShortfall(const V2DD& v, const int& p); // ExShortfall()

// ...
// ...

// RMetrics.cpp

// ExShortfall()
DBL RMetrics::ExShortfall(const V2DD& v, const int& p)
{
  UINT n = v.size();
  DBL tmp; // Declare a temporary holding variable
  DBL aum = 100000000.0; // Initialise to $100,000,000 (AuM)
}
```

## Market Risk Management

DBL es;

```
// Calculate historic P&L
VDDD pnl;
for (UINT j=1; j<v[0].size(); j++)
{
    for(UINT i=0; i<n; i++)
    {
        tmp = aum * (v[i][j]) / 100.0;
        pnl.push_back(tmp);
    }
}
```

DBL mean = Mean(pnl, 1); // Inherit Mean from the Stats class
DBL std = StdDev(pnl, 's', 1); // Inherit St. Dev. from the Stats class
DBL skew = Skew(pnl, 1); // Inherit Skew from the Stats class
DBL xskurt = XKurt(pnl, 1); // Inherit Excess Kurtosis
from the Stats class

// Check for correct confidence level

```
if((p == 95) || (p == 99)) m_utils.ErrorChk("p must be 95 (95%) or 99 (99%)");

if (p == 95)
{
    es = mean + e95 * std;
}
else
{
    es = mean + e99 * std;
}
return es;
```

```
// ...
// main.cpp
// ...
```

```
// Create class instances
Import ctai;
RMetrics rmetrics;
```

```
// Declare and call GetData()
V2DDD data = ctai.GetData("*./data/cta_index.dat");
```

```
// Declare and call ExShortfall() member function
DBL es = rmetrics.ExShortfall(data, 95);
```

```cpp
// Output results
cout << "\nExpected Shortfall = " << fixed << setprecision(0) << es << '\n';
//
```

![](img/2d1ac831a270b8b08f8b8ec2205913dc_280_0)

Figure 7.5 shows a histogram indicating the monthly MVaR figure which is clearly higher when compared to the parametric VaR95 of $1,556,215 for the CTA Index.

![](img/2d1ac831a270b8b08f8b8ec2205913dc_280_1)

## Figure 7.6 Comparison of ES and VaR at the 95% confidence level

## Figure 7.8 The 'child' and 'parent' distributions
