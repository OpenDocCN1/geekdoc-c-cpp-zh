```
double maxError = 0.0;
double minError = std::numeric_limits<double>::max();
const int NTrial = 100;
int coun = 0;
for (long long n = 1; n <= NTrial; ++n)
{
    if ((n / 100000) * 100000 == n)
    {
        std::cout << n << ",";
    }
    double b1 = uniformX(eng);
    double b2 = uniformY(eng2);
    double b3 = uniformY(eng3);
    double rho21 = uniformRho21(eng4);
    double rho31 = uniformRho31(eng5);
    double rho32 = uniformRho21(eng6);
    double val1 = trivarcumnorm(b1, b2, b3, rho21, rho31, rho32);
    double val2 = M(b1, b2, b3, rho21, rho31, rho32, NX, NY, NZ);
    std::cout << "Values, error: " << std::setprecision(6)
              << ++coun << " / " << val1 << "," << val2 << ","
              << std::abs(val1 - val2) << '\n';
    if (!std::isnan(val2))
    {
        maxError = std::max(maxError, std::abs(val1 - val2));
        minError = std::min(minError, std::abs(val1 - val2));
    }
}
std::cout << "Max, Min error: " << std::setprecision(16)
          << maxError << ", " << minError << '\n';
```

Output is displayed on the console. A snippet is:

```
Values, error: 1/ 3.36056e-25,8.60479e-26,2.50008e-25
Values, error: 2/ 5.55148e-15,5.55106e-15,4.2039e-19
Values, error: 3/ 0.998061,0.998062,1.55523e-06
Values, error: 4/ 0.667054,0.667056,2.38335e-06
Values, error: 5/ 3.57559e-08,3.57549e-08,9.60296e-13

// ...

Values, error: 96/ 7.25962e-15,7.21828e-15,4.13414e-17
Values, error: 97/ 0.0118934,0.0118931,2.91526e-07
Values, error: 98/ 6.82096e-17,6.19754e-17,6.23427e-18
Values, error: 99/ 9.44464e-07,9.44434e-07,2.96727e-11
Values, error: 100/ -4.16418e-25,1.23604e-73,4.16418e-25

Max, Min error: 6.003088278805357e-06, 1.36752501534285e-45
```