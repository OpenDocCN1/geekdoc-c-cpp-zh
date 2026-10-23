```
return [-1](T x)
{
    return std::exp(f(x));
};
}
```

```
template <typename T>
    FType<T> log(const FType<T>& f)
{ // log

    return [-1](T x)
    {
        return std::log(f(x));
    };
}
```

```
template <typename T>
    FType<T> pow(const FType<T>& f, int n)
{ // powers of a function f(x)*...*f(x) (n times)

    return [-1](T x)
    {
        return std::pow(f(x), n);
    };
}
```

This list is by no means exhaustive (nor is it meant to be) but it is easy to define your own functions and variations including algebra for vector functions, vector-valued functions and specialisations of the underlying data types such as complex numbers, for example.

We now give more examples of using this new functionality. The code compiles in all cases and is easy to understand. The first example computes the fourth power of a function:

```
FType<double> f = [](double x) { return x*x; };
int n = 4;
auto prodFun = pow(f, n);

double x = 2.0;
std::cout << "Power: " << prodFun(x) << "\n";
```

Strictly speaking, we should place these functions in a namespace to avoid confusing them with standard C++ functions such as std::pow, for example (we leave this as an exercise). The second example is a kind of *sanity check* to see how the code with unary minus and unary plus gives the expected result (the code compiles with flying colours):

```
{ // unary minus and plus

    auto f = assign(5.0);
    auto f1 = exp(f);
    auto f2 = +exp(f);
```