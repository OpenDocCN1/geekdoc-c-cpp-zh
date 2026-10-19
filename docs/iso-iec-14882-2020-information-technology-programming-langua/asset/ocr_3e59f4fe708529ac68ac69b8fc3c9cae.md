```
```cpp
};

constexpr T operator()(const T& x, const T& y) const;
```
```

_Returns:_ `x % y`.

```
```cpp
template<> struct modulus<void> {
  template<class T, class U> constexpr auto operator()(T&& t, U&& u) const
    -> decltype(std::forward<T>(t) % std::forward<U>(u));

  using is_transparent = unspecified;
};
```
```

```
```cpp
template<class T, class U> constexpr auto operator()(T&& t, U&& u) const
  -> decltype(std::forward<T>(t) % std::forward<U>(u));
```
```

_Returns:_ `std::forward<T>(t) % std::forward<U>(u)`.

# 20.14.7.7  Class template negate

```
```cpp
template<class T = void> struct negate {
  constexpr T operator()(const T& x) const;
};
```
```

```
```cpp
constexpr T operator()(const T& x) const;
```
```

_Returns:_ `-x`.

```
```cpp
template<> struct negate<void> {
  template<class T> constexpr auto operator()(T&& t) const
    -> decltype(-std::forward<T>(t));

  using is_transparent = unspecified;
};
```
```

```
```cpp
template<class T> constexpr auto operator()(T&& t) const
  -> decltype(-std::forward<T>(t));
```
```

_Returns:_ `-std::forward<T>(t)`.

# 20.14.8  Comparisons

# 20.14.8.1  General

The library provides basic function object classes for all of the comparison operators in the language ([7.6.9](7.6.9), [7.6.10](7.6.10)).

For templates less, greater, less_equal, and greater_equal, the specializations for any pointer type yield a result consistent with the implementation-defined strict total order over pointers ([3.24](3.24)).

> [_Note 1:_ If `a < b` is well-defined for pointers `a` and `b` of type P, then `(a < b) == less<P>()(a, b)`, `(a > b) == greater<P>()(a, b)`, and so forth. — _end note_]

For template specializations `less<void>`, `greater<void>`, `less_equal<void>`, and `greater_equal<void>`, if the call operator calls a built-in operator comparing pointers, the call operator yields a result consistent with the implementation-defined strict total order over pointers.

# 20.14.8.2  Class template equal_to

```
```cpp
template<class T = void> struct equal_to {
  constexpr bool operator()(const T& x, const T& y) const;
};
```
```

```
```cpp
constexpr bool operator()(const T& x, const T& y) const;
```
```

_Returns:_ `x == y`.

```
```cpp
template<> struct equal_to<void> {
  template<class T, class U> constexpr auto operator()(T&& t, U&& u) const
    -> decltype(std::forward<T>(t) == std::forward<U>(u));
```
```