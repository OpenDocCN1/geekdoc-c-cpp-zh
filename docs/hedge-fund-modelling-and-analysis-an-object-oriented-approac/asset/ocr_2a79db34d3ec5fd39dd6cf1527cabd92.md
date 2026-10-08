```
{
UINT n = v.size();
DBL tmp; // Declare a temporary holding variable

V1DD mlm2; // Declare a 1D vector of doubles for the Skew
V1DD mean = Mean(v, c); // Inherit Mean from the Stats class
V1DD std = StdDev(v, c, f); // Inherit St. Dev. from the Stats class

// Calculate M1M2
for (UINT j=1; j<v[0].size(); j++) {
    tmp = 0.0;
    for (UINT i=0; i<n; i++) {
        tmp = mean[j-1] / std[j-1];
    }
    mlm2.push_back(tmp);
}

return mlm2;
}

// ...
// main.cpp
// ...

V1DS s;
s.push_back("MgrA");
s.push_back("MgrB");

// Call Mean() and StdDev() member functions of the Stats class
mean = stats.Mean(data, 12);
std = stats.StdDev(data, 'p', 12); // Population (p)

// Call M1M2() member function of the PMetrics class
lmm2 = pmetrics.M1M2(data, 'p', 12);

// Output results
// Call SortPrint() member function of the PMetrics class
cout << "\nMean:\n";
pmetrics.SortPrint(mean, s);
cout << "\nSt. Dev.:\n";
pmetrics.SortPrint(std, s);
cout << "\nM1/M2:\n";

```