# Modern C++: Lambda Improvements (C++20)

# Template Parameters In Lambdas

C++20 permits lambdas to have template parameters:

```
auto sumTem = []typename T>(T x, T y) { return x + y };
```

All of the template parameters must have the same type.

# Allow lambda-capture [=, this]

Until C++20 this was always captured by reference in lambdas, even with the introducer []. To remove this confusion, C++20 deprecates such behaviour and allows the more explicit [=, this]:

```
[=]();          // captures this by reference, deprecated since C++20
[*this]();    // OK since C++17, captures this by value
[this]();     // OK since C++20, captures this by reference
```