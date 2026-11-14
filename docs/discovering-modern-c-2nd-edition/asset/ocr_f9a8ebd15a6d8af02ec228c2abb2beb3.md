```
struct helper
{
    double maxm(double x, double y) const { return x >= y ? x : y; }
    static double max(double x, double y) { return x >= y ? x : y; }
};
```