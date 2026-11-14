```
template <typename T>
auto abs(const T& x) -> decltype(abs_functor<T>{}(x))
{
    return abs_functor<T>{}(x);
}
```