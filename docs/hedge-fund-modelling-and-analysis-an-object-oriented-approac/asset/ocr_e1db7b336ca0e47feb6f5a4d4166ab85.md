![](bbox=[0.125, 0.115, 0.876, 0.386])

You will notice from Source 7.3 that we have used two slightly different member functions from the Stats class for the Mean() and StDev(). These are declared as type DBL and now take a V1DD input parameter as opposed to a V2DD. Source 7.4 shows how we have overloaded the member functions so we can use them to calculate a single value for the parametric VaR.

# SOURCE 7.4: Mean() AND StDev() OVERLOADED MEMBER FUNCTIONS OF THE STAT CLASS

```
// Stats.h
// ...

V1DD Mean(const V1DD& v, const int& f); // Mean()
DBL Mean(const V1DD& v, const int& f); // Mean()
V1DD StDev(const V1DD& v, const char& c, const int& f); // StDev()
DBL StDev(const V1DD& v, const char& c, const int& f); // StDev()
// ...
// ...
// Stats.cpp
// ...

// Mean()
DBL Stats::Mean(const V1DD& v, const int& f = 1)
{
  UINT n = v.size();
  double tmp; // Declare a temporary holding variable
```