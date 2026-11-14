```
template <typename T>
typename abs_functor<T>::result_type
abs(const T& x)
{
    return abs_functor<T>{}(x);
}
```