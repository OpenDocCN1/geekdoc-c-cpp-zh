distribution of monthly P&L values and an indicator for the VaR at a 95% confidence level in the left-tail of the distribution at the 5th percentile. Note that there are losses in excess of the VaR value further to the left of the tail indicates that VaR does not tell us anything about the actual magnitude of the extreme losses in the tail.

# SOURCE 7.2: MONTHLY VaR AT 95% CONFIDENCE LEVEL USING HISTORICAL SIMULATION

```
//
// ...n// RMetrics.h
// ...

DBL HistoricVaR(const V2DD& v, const int& p); // HistoricVaR()
// ...n// RMetrics.cpp
#include "RMetrics.h"

#include <algorithm> // For sorting sort(

DBL RMetrics::HistoricVaR(const V2DD& v, const int& p)

UINT n = v.size();
DBL tmp; // Define a temporary holding variable
DBL aum = 100000000.0; // Initialise to $100,000,000 (AuM)

VIDD pnl; // Define a 1D vector of doubles for the P&L

// Calculate Historic P&L
for(UINT j=1; j<v[0].size(); j++) {
{
for(UINT i=0; i<n; i++) {
tmp = aum * (v[i][j] / 100.0);
npnl.push_back(tmp);
}
}

// Sort P&L in descending order
sort(pnl.begin(), pnl.end());

// Calculate pth percentile of ordered P&L e.g., 95th
DBL pp = *(pnl.begin() + int(pnl.size()) * (1 - p / 100.0));
```