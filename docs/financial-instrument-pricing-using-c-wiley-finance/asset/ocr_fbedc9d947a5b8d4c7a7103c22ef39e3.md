discuss *catastrophic cancellation* that occurs when we subtract two nearly equal numbers. In this case this operation increases relative accuracy substantially more than it increases absolute error. This phenomenon is also called *loss of significance*. In the case of approximating derivatives we have seen in Section 22.3.5 that there is a critical value of the step size below which the approximation will give disastrous results. We computed this critical value (approximately 0.003) for the exponential function using floating-point arithmetic.

We use the following generic divided difference formulae to approximate a function’s derivatives:

```
template <typename T>
    T firstDividedDifference(const FunctionType<T>& f, T xval, T h)
{ // 2nd order approximation h^2/6

    return (f(xval+h) - f(xval-h)) / (T(2) * h);
}
```

```
template <typename T>
    T RichardsonfirstDividedDifference(const FunctionType<T>& f,
                                    T xval, T h)
{ // 4th order approximation to df/dx using Richardson extrapolation

    T h2 = h * T(0.5);
    T f1 = 4*firstDividedDifference(f, xval, h2);
    T f2 = firstDividedDifference(f, xval, h);

    return (f1 - f2) / 3;
}
```

```
template <typename T>
    T firstDividedDifferenceOrder4(const FunctionType<T>& f, T xval, T h)
{ // 4th order approximation h^4/30

    return (f(xval -2*h) - 8*f(xval -h) + 8*f(xval + h)
        - f(xval + 2*h)) / (12 * h);
}
```

```
template <typename T>
    T secondDividedDifference(const FunctionType<T>& f, T xval, T h)
{ // 2nd order h^2/12

    return (f(xval+h) - (2 * f(xval)) + f(xval-h)) / (h * h);
}
```

```
template <typename T>
    T secondDividedDifferenceOrder4(const FunctionType<T>& f, T xval, T h)
{ // 4th order h^4/90

    return (-f(xval - 2*h) + 16*f(xval - h) - 30*f(xval)
        + 16*f(xval + h) - f(xval + 2*h)) / (12 * h * h);
}
```