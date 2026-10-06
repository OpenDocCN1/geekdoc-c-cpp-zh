# ISO/IEC 14882:2017(E)

```
template <class T, class U> constexpr auto operator()(T&& t, U&& u) const
-> decltype(std::forward<T>(t) / std::forward<U>(u));
Returns: std::forward<T>(t) / std::forward<U>(u).
```

# 23.14.6.5 Class template modulus [arithmetic.operations.modulus]

```
template <class T = void> struct modulus
constexpr T operator()(const T& x, const T& y) const;

constexpr T operator()(const T& x, const T& y) const;
Returns: x % y;

template <> struct modulus<void> {
template <class T, class U> constexpr auto operator()(T&& t, U&& u) const
-> decltype(std::forward<T>(t) % std::forward<U>(u));

using is_transparent = specified;

ntemplate <class T, class U> constexpr auto operator()(T&& t, U&& u) const
-> decltype(std::forward<T>(t) % std::forward<U>(u));
Returns: std::forward<T>(t) % std::forward<U>(u)).
```

# 23.14.6.6 Class template negate [arithmetic.operations.negate]

```
template <class T = void> struct negate
constexpr T operator()(const T& x) const;

constexpr T operator()(const T& x) const;
Returns: -x;

template <> struct negate<void> {
template <class T> constexpr auto operator()(T&& t) const
-> decltype(-std::forward<T>(t));

using is_transparent = specified;

templatetemplate <class T> constexpr auto operator()(T&& t) const
-> decltype(-std::forward<T>(t));
Returns: -std::forward<T>(t).
```

# 23.14.7 Comparisons [comparisons]

+   1 The library provides basic function objects for all of the comparison operators in the (8.9, 8.10).
2 For templates less, greater, less_equal, and greater_equal, the specializations for any pointer type define a strict order that is consistent with other specializations and also consistent with the partial order imposed by the built-in operators <, >, ==, !=. [Note: When a < b is well-defined for pointers of type P, this implies (a < b) == less<P>(a, b), (a > b) == greater<P>(a, b), and so forth. For template specializations less<void>, greater<void>, less_equal<void>, and greater_equal<void>, if the operator calls a built-in operator comparing pointers, the call operator yields a strict total