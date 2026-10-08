```
constexpr complex<double> operator"""i(long double arg) // imaginary literal
{
    return {0,arg};
}
```