```
Stats() {}
virtual -Stats() {};
```

```
// Member function declarations
V1DD VAI(const V2DD& v); // VAI()
V1DD Mean(const V2DD& v); // Mean()
V1DD StdDev(const V2DD& v, const char& c); // StdDev
V1DD Skew(const V2DD& v); // Skew()
V1DD XKurt(const V2DD& v); // XKurt()
```

```
V1DD Cov(const V2DD& v); // Cov()
```

private:

```
// Member variable declarations
Utils m_utils;
```

```
}
```

```
// Stats.cpp
// ...
```

```
// Cov()
V1DD Stats::Cov(const V2DD& v)
```

```
{
if(v[0].size() < 3) m_utils.ErrorChk("More than one time series
required");n
```

```
UINT n = v.size();
double tmp; // Declare a temporary holding variable
```

```
V1DD mean = Mean(v); // Declare a 1D vector of doubles for the Mean
V1DD cov; // Declare a 1D vector of doubles for the Covar.
```

```
// Calculate Covar. using Eigen. (3.18)
for(UINT k=0; k<mean.size(); k++)
{
for(UINT j=1; j<v[0].size(); j++)
{}
```

```
tmp = 0.0;
for(UINT i=0; i<n; i++)
{
tmp += ((v[i][j] - mean[j-1]) * (v[i][k+1] - mean[k]));
}
tmp /= (n-1);
cov.push_back(tmp);
```