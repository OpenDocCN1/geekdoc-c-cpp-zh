# TABLE 7.3 ES critical values for 95% and 99% confidence intervals

| c | α = (1 - c) | Critical value (z_α) |
|---|---|--|
| 95% | 5% | -2.06271281 |
| 99% | 1% | -2.66521422 |

Table 7.3 shows the most common confidence levels at 95% and 99% and their associated values z_α for the ES. Note that both zES5 and zES1 have been negated in both to be consistent with the critical values for VaR and to indicate a loss in the left-tail of the P&L distribution.

Using the standard formula for VaR_{1-α} from (7.2), we have similarly:

$ES_{1-α} = \mu + z_{ES}\sigma$ (7.9)

where $ES_{α}$ is the critical value from a normal distribution at the required significance level, $\alpha$. This gives the estimate of the ES in the left-tail of the P&L distribution but course it could be further along the distribution. Since ES is by definition more than VaR, ES is a more conservative estimate of VaR and thus it is often used as a complement to traditional VaR measures. Source 7.7 shows that monthly $ES_{ag}$ is 2 189 835.

# SOURCE 7.7: MONTHLY VaR AT 95% CONFIDENCE LEVEL USING ES

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
(
  UINT n = v.size();
DBL tmp; // Declare a temporary holding variable
DBL aum = 1000000000.0; // Initialise to $100,000,000 (AuM)
```