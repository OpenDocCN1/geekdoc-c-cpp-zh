> The log-normal curve represents an engineering truth missed by the bell curve.

The normal curve is a misfit; it has an odd negative tail that is not practical and also it tenders a misleading peak. The log-normal curve does not go negative and has the right skewed tail and a perfect peak.

> Software design is not a Gaussian process; it is a log-normal process.

# Building a Log-Normal PDF for Software Design Complexity

As the saying goes, if we substitute natural logarithms for x in a Gaussian PDF equation (Equation 17.1), we obtain a log-normal PDF equation, as follows:

```
F(x, μ, σ) = 1 / √(2πσ) e^(-(x-μ)² / (2σ²)) (17.1)
```

Accordingly, natural logarithms of data must be taken first, and then in Equation 17.1, x must be replaced by Ln(x), μ must be replaced by the average of Ln(x), and σ must be replaced by the standard deviation of Ln(x). However, the equation will be in the logarithmic scale. Taking exponential of the results will convert them to real-life units.

It may be noted that the Excel function LOGNORM.DIST takes inputs in the logarithmic scale but gives results in real domain. We do not have to take exponentials and go through a separate conversion process, and this is a great practical convenience.

Users have built their own versions of the log-normal PDF. The first choice we need to make is the central value.

> The log-normal PDF is built around the median, like the Gaussian is built around the mean.

Some versions of log-normal use the geometric mean. In a typical log-normal process, the median and the geometric mean are nearly equal. Using the geometric mean is highly justified by the fact that log-normal numbers are multiplicative and tend to form a geometric series. In creating a log-normal PDF, the NIST Engineering Statistics Handbook [3] proposes the following structure:

```
f(x) = 1 / (σ x √(2π)) e^(-(ln x - β)² / (2σ²)) (17.2)
```

where β is the scale factor and σ is the shape factor.