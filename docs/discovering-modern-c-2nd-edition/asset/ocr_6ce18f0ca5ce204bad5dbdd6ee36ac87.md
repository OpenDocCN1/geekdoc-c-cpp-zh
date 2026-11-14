```
template <typename T>
inline T sum(T t) { return t; }
```

```
template <typename T, typename ...P>
inline sum_type_t<T, P...> sum(T t, P ...p)
{
    return t + sum(p...);
}
```