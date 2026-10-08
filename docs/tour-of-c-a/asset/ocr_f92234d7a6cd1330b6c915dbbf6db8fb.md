```
constexpr int dmv = 17;
int var = 17;
const double sqv = sqrt(var);

double sum(const vector<double>&);

vector<double> v = {1.2, 3.4, 4.5};
const double s1 = sum(v);
constexpr double s2 = sum(v);
```

// dmv is a named constant
// var is not a constant
// sqv is a named constant, possibly computed at run time

// sum will not modify its argument (§1.7)

// v is not a constant
// OK: sum(v) is evaluated at run time
// error: sum(v) is not a constant expression