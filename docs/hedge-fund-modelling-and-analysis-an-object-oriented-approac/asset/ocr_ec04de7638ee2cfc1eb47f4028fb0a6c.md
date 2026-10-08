parameters we no longer require all of the historical data to calculate VaR. Recall from (7.2) that the VaR can be written formally as:

$VaR_{1-\alpha} = \mu + Z_{\alpha}\sigma$ (7.3)

Source 7.3 shows an implementation of this function to determine the monthly VaR at a 95% confidence level for the CTA Index with a current value of $100m AuM.

# SOURCE 7.3: MONTHLY VAR AT 95% CONFIDENCE LEVEL USING PARAMETRIC METHOD

```
// ...
// RMetrics.h
// ...
DBL ParametricVaR(const V2DD&, const int&); // ParametricVaR()

protected:
private:
    // Member variable declarations
    static const DBL 295; // z-value for 95% confidence level
    static const DBL 299; // z-value for 95% confidence level
    static const DBL e95; // z-value for 95% confidence level (ES)
    static const DBL e99; // z-value for 95% confidence level (ES)
// ...

// ...
// RMetrics.cpp

// Initialise members of the RMetrics class
const DBL RMetrics::z295 = -1.64485363;
const DBL RMetrics::z299 = -2.32634787;
const DBL RMetrics::e95 = -2.06271281;
const DBL RMetrics::e99 = -2.66521422;
// ...

// ParametricVaR()
DBL RMetrics::ParametricVaR(const V2DD&, const int& p)
{
    UINT n = v.size();
    DBL tmp; // Declare a temporary holding variable
    DBL aum = 100000000.0; // Initialise to $100,000,000 (AuM)

V1DD pnl; // Define a 1D vector of doubles for the P&L
```