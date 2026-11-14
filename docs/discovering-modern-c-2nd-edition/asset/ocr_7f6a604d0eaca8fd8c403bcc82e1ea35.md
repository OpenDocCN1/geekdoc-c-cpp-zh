?: to stop the recursion because both of its respective branches are eagerly evaluated and one of them still contains the infinite recursion. In C++17 we can however take constexpr-if. Traditionally, recursive template definitions are terminated a specialization like the following:

Click here to view code image

```
template <typename F, typename T>
class nth_derivative <1, F, T>
{
public:
    nth_derivative(const F& f, const T& h) : f(f), h(h) {}
    T operator()(const T& x) const
    {
        return ( f(x+h) - f(x) ) / h;
    }
private:
    const F& f;
    T h;
};
```

This specialization is identical to the class derivative that we now could throw away. Or we keep it and reuse its functionality by simply deriving from it (more about derivation in Chapter 6).

Click here to view code image

```
template <typename F, typename T>
class nth_derivative<1, F, T>
    : public derivative<F, T>
{
    using derivative<F, T>::derivative;
};
```

Now we can compute any derivative like the 22nd:

Click here to view code image

```
nth_derivative<22, psc_f, double> d22_psc_o{psc_f(1.0),
    0.00001};
```

The new object d22_psc_o is again a unary function object. Unfortunately, it approximates so badly that we are too ashamed to present the results here. From Taylor series, we know that the error of the f'' approximation is reduced from O(h) to O(h^2) when a backward difference is applied to the