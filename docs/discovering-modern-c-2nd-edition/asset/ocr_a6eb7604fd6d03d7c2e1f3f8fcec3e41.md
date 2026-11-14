```
template <typename T>
T square_root(const T& x)
{
    const T my_eps= T{2} * x * numeric_limits<T>::epsilon();
    T r = x;

    while (std::abs((r * r) - x) > my_eps)
    {
        r = (r + x/r) / T{2};
    }
    return r;
}
```