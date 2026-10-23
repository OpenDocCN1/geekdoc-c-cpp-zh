```
```cpp
FType<double> f22 = [&] (double x) { return std::cos(c*x); };
FType<double> f2 = -exp(f22);
FType<double> f3 = assign(a + std::exp(1.0));
FType<double> Ackley = f1 + f2 + f3;

return Ackley(x);
}
```
```

We can test if these functions give the same output by running a simple test program:

```
```cpp
double x = -1.0;
while (x < 1.0)
{
    std::cout << AckleyGlobalFunction(x) - AckleyGlobalFunctionII(x);
    x += 0.1;
}
```
```

The output should be (almost) zero in all cases.
As a final example we take the function:

$x^2 + x^4 + x^8, \quad -10 \leq x \leq 10.$  (A2.11)

A possible implementation is:

```
```cpp
double TestFunction(double x)
{ // To show how function algebra works

    // Bit unwieldy; used to show function vector spaces.
    FType<double> f1 = [] (double x) {return x*x; };
    FType<double> f2 = [&] (double x) {return f1(x)*f1(x); };
    FType<double> f3 = [&] (double x) {return f2(x)*f2(x); };

    FType<double> sumFunc = f1 + f2 + f3;

    return sumFunc(x);
}
```
```

We can check this code with a straightforward implementation using the power function
as follows:

```
```cpp
double x = 2.710;
std::cout << "Test vs exact: " << TestFunction(x) << ", "
          << std::pow(x, 2.0) + std::pow(x, 4.0) + std::pow(x, 8.0);
```
```

The output is:

```
```text
Test vs exact: 2970.35, 2970.35
```
```