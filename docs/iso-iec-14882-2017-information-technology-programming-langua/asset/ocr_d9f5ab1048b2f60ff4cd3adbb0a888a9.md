# ISO/IEC 14882:2017(E)

```
// 29.9.4. classification / comparison functions
int fpclassify(float x);
int fpclassify(double x);
int fpclassify(long double x);
```

```
int infinite(float x);
int infinite(double x);
int infinite(long double x);
```

```
int isinf(float x);
int isinf(double x);
int isinf(long double x);
```

```
int isnan(float x);
int isnan(double x);
int isnan(long double x);
```

```
int isnormal(float x);
int isnormal(double x);
int isnormal(long double x);
```

```
int signbit(float x);
int signbit(double x);
int signbit(long double x);
```

```
int isgreater(float x, float y);
int isgreater(double x, double y);
int isgreater(long double x, long double y);
```

```
int iserequal(float x, float y);
int isequal(double x, double y);
int isequal(long double x, long double y);
```

```
int isless(float x, float y);
int isless(double x, double y);
int isless(long double x, long double y);
```

```
int islequal(float x, float y);
int isequal(double x, double y);
int isequal(long double x, long double y);
```

```
int isgreater(float x, float y);
int isgreater(double x, double y);
int isgreater(long double x, long double y);
```

```
int unordered(float x, float y);
int unordered(double x, double y);
int unordered(long double x, long double y);
```

```
// 29.9.5. mathematical special functions
```

```
// 29.9.5.1. associated Laguerre polynomials
```

```
double assoc_laguerre(unsigned n, unsigned m, double x);
float assoc_laguerref(unsigned n, unsigned m, float x);
long double assoc_laguerrel(unsigned n, unsigned m, long double x);
```