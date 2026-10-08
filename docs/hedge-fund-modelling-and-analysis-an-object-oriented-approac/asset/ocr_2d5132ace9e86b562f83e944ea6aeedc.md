# Performance Measurement

As can be seen, the SR produces a ranked list which captures very well in one metric of the risk-adjusted return (or return per unit). This metric is already a vast improvement over just using the annualised returns for performance since the hedge fund manager can use leverage (as opposed to traditional fund managers who cannot use leverage), so they need to be relative to their ‘peers’ in a risk-adjusted manner. As mentioned earlier, a poorer manager can simply use leverage to gain superior results when measured against the SR performance, their results would not seem superior. It is for this reason that the SR is a very commonly used metric in the world of hedge funds – enabling a manager or investor to get a quick picture of whether a strategy or fund is worth pursuing. In general, the SR is the first port of call for any hedge fund analysis, and if SR is high, further analysis is required to assess other characteristics of the fund.

The disadvantage of the SR is that it is absolute in the sense that it does not measure the manager meaningfully against a market benchmark (i.e. the risk-free rate). However, other measures will be described in the following sections which are relative versus a market benchmark for ranking purposes. Other disadvantages are that the SR is based exclusively on mean-variance, so higher moments are neglected and assumed to be zero. The SR assumes that the returns are Gaussian which is not always the case for hedge funds, especially the more exotic relative strategies as highlighted by Lhabitant (2007).



In this section, we will consider performance metrics based around the Market Model (MM). The MM differs from the Capital Asset Pricing Model (CAPM) in that it is based around a regression of excess returns of individual assets over some reference market benchmark (or aggregate index). MM can be written as:

```
$R_i = \alpha_i + R_F + \beta_i(R_M - R_F) + \epsilon_i \quad (5.5)$
```

in terms of risk preferences:

```
$R_i - R_F = \alpha_i + R_F + \beta_i(R_M - R_F) + \epsilon_i \quad (5.6)$
```

According to the CAPM all priced assets with respect to publicly known information should fall on the Security Market Line (SML) as shown in Figure 5.10.
In 5.10 Hedge Fund B exhibits greater than expected performance (i.e. –ve alpha) where Fund A exhibits less than expected performance (i.e. –ve alpha), both with respect to the market benchmark. From the CAPM we can estimate this measure of a hedge fund’s added value:

```
$\alpha_p = R_p - E^{CAPM}(R_M) \quad (5.7)$
```

```
$.:\alpha_p = (R_p - R_F) - \beta_p(R_M - R_F) \quad (5.8)$
```