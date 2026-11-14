```
// Forward declaration
template <typename ...P> struct sum_type;
```

```
template <typename T>
struct sum_type<T>
{
    using type= T;
};
```

```
template <typename T, typename ...P>
struct sum_type<T, P...>
{
    using type= decltype(T() + typename sum_type<P...>::type());
};
```

```
template <typename ...P>
using sum_type_t= typename sum_type<P...>::type;
```