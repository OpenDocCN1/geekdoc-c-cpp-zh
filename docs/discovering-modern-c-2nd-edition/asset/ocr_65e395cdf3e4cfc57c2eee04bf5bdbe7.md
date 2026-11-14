In Section 3.11, we implemented a variadic sum that accepted an arbitrary number of arguments of mixed types. The problem with this implementation was that we did not know an appropriate return type and used that of the first argument. And failed miserably. In the meantime, we have seen more features and want to re-attack the problem. Our first approach is to use decltype to determine the result type:

Click here to view code image

```
template <typename T>
inline T sum(T t) { return t; }

template <typename T, typename ...P>
auto sum(T t, P ...p) -> decltype( t + sum(p...) ) // Error
{
    return t + sum(p...);
}
```

Unfortunately, this implementation does not compile for more than two arguments. To determine the return type for n arguments, the return type for the last n − 1 arguments is needed which is only available after the function is completely defined but not yet for the trailing return type.

# C++11 5.2.7.1 Variadic Class Template

Thus, we have to determine the result type first. This can be done recursively by a variadic type trait:

Click here to view code image

```
// Forward declaration
template <typename ...P> struct sum_type;

template <typename T>
struct sum_type<T>
{
    using type= T;
};

template <typename T, typename ...P>
struct sum_type<T, P... >
{
    using type= decltype( T() + typename
    sum_type<P...>::type() );
};
```