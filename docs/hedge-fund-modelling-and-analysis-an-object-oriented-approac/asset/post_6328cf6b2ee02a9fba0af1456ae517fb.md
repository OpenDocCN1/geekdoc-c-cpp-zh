
distribution of monthly P&L values and an indicator for the VaR at a 95% confidence level in the left-tail of the distribution at the 5th percentile. Note that there are losses in excess of the VaR value further to the left of the tail indicates that VaR does not tell us anything about the actual magnitude of the extreme losses in the tail.

# SOURCE 7.2: MONTHLY VaR AT 95% CONFIDENCE LEVEL USING HISTORICAL SIMULATION

```cpp
//
// ...n// RMetrics.h
// ...

DBL HistoricVaR(const V2DD& v, const int& p); // HistoricVaR()
// ...n// RMetrics.cpp
#include "RMetrics.h"

#include <algorithm> // For sorting sort(

DBL RMetrics::HistoricVaR(const V2DD& v, const int& p)
{
    UINT n = v.size();
    DBL tmp; // Define a temporary holding variable
    DBL aum = 100000000.0; // Initialise to $100,000,000 (AuM)

    V1DD pnl; // Define a 1D vector of doubles for the P&L

    // Calculate Historic P&L
    for(UINT j=1; j<v[0].size(); j++) {
        for(UINT i=0; i<n; i++) {
            tmp = aum * (v[i][j] / 100.0);
            pnl.push_back(tmp);
        }
    }

    // Sort P&L in descending order
    sort(pnl.begin(), pnl.end());

    // Calculate pth percentile of ordered P&L e.g., 95th
    DBL pp = *(pnl.begin() + int(pnl.size()) * (1 - p / 100.0));

    return pp;
}

// ...
// main.cpp
// ...

// Create class instances
Import ctai;
RMetrics rmetrics;

// Declare and call GetData()
V2DD data = ctai.GetData("./data/cta_index.dat");

// Declare and call HistoricVaR() member function
DBL hvar = rmetrics.HistoricVaR(data, 95);

// Output results
cout << "\n Historic VaR = $" << fixed << setprecision(0) << hvar << "\n";
// ...
```

![](img/2d1ac831a270b8b08f8b8ec2205913dc_264_0.png)

# 7.3.2 Parametric Method

The parametric method does not require all of the data that the historic simulation requires but may use the data to determine parameters of the hedge fund return distribution. If we generally assume the hedge fund returns are consistent with a normal distribution then we only need two parameters to characterise the distribution, namely the mean, $\mu$ and standard deviation, $\sigma$. That is, once we have determined two parameters we no longer require all of the historical data to calculate VaR. Recall from (7.2) that the VaR can be written formally as:

$VaR_{1-\alpha} = \mu + Z_{\alpha}\sigma$ (7.3)

Source 7.3 shows an implementation of this function to determine the monthly VaR at a 95% confidence level for the CTA Index with a current value of $100m AuM.

# SOURCE 7.3: MONTHLY VAR AT 95% CONFIDENCE LEVEL USING PARAMETRIC METHOD

```cpp
// ...
// RMetrics.h
// ...
DBL ParametricVaR(const V2DD&, const int&); // ParametricVaR()

protected:
private:
    // Member variable declarations
    static const DBL z295; // z-value for 95% confidence level
    static const DBL z299; // z-value for 95% confidence level
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
DBL RMetrics::ParametricVaR(const V2DD& v, const int& p)
{
    UINT n = v.size();
    DBL tmp; // Declare a temporary holding variable
    DBL aum = 100000000.0; // Initialise to $100,000,000 (AuM)

    V1DD pnl; // Define a 1D vector of doubles for the P&L

    // Calculate historic P&L
    for(UINT j=1; j<v[0].size(); j++)
    {
        for(UINT i=0; i<n; i++)
        {
            tmp = aum * (v[i][j] / 100.0);
            pnl.push_back(tmp);
        }
    }

    DBL mean = Mean(pnl, 1); // Inherit Mean from the Stats class
    DBL std = StdDev(pnl, 'p', i); // Inherit St. Dev. from the Stats Dev.
    DBL pvar;

    // Check for correct confidence level
    if(p != 95 && p != 99) {
        mutils.ErrorChk("p must be 95 (95%) or 99 (99%)");
    }

    if(p == 95)
    {
        pvar = mean + std * z95;
    }
    else
    {
        pvar = mean + std * z99;
    }

    return pvar;
}

// ...
// main.cpp
// ...

// Create class instances
Import ctai;
RMetrics rmetrics;

// Declare and call GetData()
V2DD data = ctai.GetData("./data/cta_index.dat");

// Declare and call ParametricVaR() member function
DBL pvar = rmetrics.ParametricVaR(data, 95);

// Output results
cout << "\n Parametric VaR = $" << fixed << setprecision(0) << pvar << "\n";
// ...
```

![](img/2d1ac831a270b8b08f8b8ec2205913dc_267_0.png)

You will notice from Source 7.3 that we have used two different member functions from Stats class for Mean() and StDev(). These are declared as DBL and now take V2DD input. Source 7.4 shows how we have overloaded the member functions so we can use them to calculate a single value for VaR.

# SOURCE 7.4: Mean() AND StDev() OVERLOADED MEMBER FUNCTIONS OF THE STAT CLASS

```cpp
// Stats.h
// ...

DBL Mean(const V1DD& v, const int& f); // Mean()
DBL Mean(const V2DD& v, const int& f); // Mean()
V1DD StDev(const V1DD& v, const char& c, const int& f); // StDev()
DBL StDev(const V2DD& v, const char& c, const int& f); // StDev()
// ...
// Stats.cpp
// ...

// Mean()
DBL Stats::Mean(const V1DD& v, const int& f = 1)
{
    UINT n = v.size();
    double tmp; // Declare a temporary holding variable
    DBL mean; // Declare a double for the Mean

    // Calculate mean using Eq. (3.10)
    tmp = 0.0;
    for(UINT i=0; i<n; i++) {
        tmp += v[i];
    }
    tmp /= n;
    tmp *= (double)f; // Cast frequency (f) to double
    mean = tmp;

    return mean;
}

// ...
// StDev() - Sample (s), Population (p)
DBL Stats::StDev(const V1DD& v, const char& c, const int& f = 1)
{
    if(c != 's' && c != 'p') {
        mutils.ErrorChk("Type must be 's' (sample) or 'p' (population)");
    }

    UINT n = v.size();
    double tmp; // Declare a temporary holding variable
    DBL mean = Mean(v); // Declare a double for the Mean
    DBL std; // Declare a double for the St. Dev.

    // Calculate St. Dev. using Eq. (3.12) or (3.13)
    tmp = 0.0;
    for(UINT i=0; i<n; i++) {
        tmp += pow(v[i] - mean, 2);
    }
    if (c == 's')
        tmp /= (n-1);
    else
        tmp /= n;
    std = sqrt(tmp) * (double)f; // Cast frequency (f) to double

    return std;
}
// ...
```

![](img/2d1ac831a270b8b08f8b8ec2205913dc_269_0.png)

FIGURE 7.4 Histogram showing monthly VaR with the parametric method

Source 7.5 shows that the monthly VaR for a CTA Index valued at $100m (AuM) for a 95% confidence level is i.e. there is only a 5% chance that the value of the CTA Index will fall by more than 5% over the next month. Figure 7.4 shows a histogram indicating the monthly VaR.

# SOURCE 7.5: Monthly VaR AT 95% CONFIDENCE LEVEL USING Modified METHOD

```cpp
// ...
// RMetrics.h
// ...

DBL ModifiedVaR(const V2DD& v, const int&); // ModifiedVaR()

// ...
// ...
// RMetrics.cpp

ModifiedVaR()
DBL RMetrics::ModifiedVaR(const V2DD& v, const int& p)
{
    UINT n = v.size();
    DBL tmp; // Declare a temporary holding variable
    DBL aum = 100000000.0; // Initialise to $100,000,000 (AuM)

    DBL z, zcf;
    DBL mvar;

    // Calculate historic P&L
    V1DD pnl;
    for(UINT j=1; j<v[0].size(); j++) {
        for(UINT i=0; i<n; i++) {
            tmp = aum * (v[i][j] / 100.0);
            pnl.push_back(tmp);
        }
    }

    DBL mean = Mean(pnl, 1); // Inherit Mean from the Stats class
    DBL std = StDev(pnl, 's', 1); // Inherit St. Dev. from the Stats class
    DBL skew = Skew(pnl, 1); // Inherit Skew from the Stats class
    DBL xskurt = Xskurt(pnl, 1); // Inherit Excess Kurtosis from the Stats class

    // Check for correct confidence level
    if(p != 95 && p != 99) {
        m_utils.ErrorChk("p must be 95 (95%) or 99 (99%)");
    }

    if(p == 95) {
        z = z95;
    }
    else {
        z = z99;
    }

    zcf = z+((pow(z, 2) - 1)*skew)/ 6 + ((pow(z, 3) - 3 * z) * xskurt) / 24
    - (((pow(z, 3)) - 5 * z) * pow(skew, 2) / 36)); // Cornish-Fisher variate

    mvar = mean + zcf * std;

    return mvar;
}

// ...
// main.cpp
// ...

// Create class instances
Import ctai;
RMetrics rmetrics;
```
