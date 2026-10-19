# 20.14.7.3 Class template minus [arithmetic.operations.minus]

```
template<class T = void> struct minus {
    constexpr T operator()(const T& x, const T& y) const;
};
```

```
constexpr T operator()(const T& x, const T& y) const;
```

Returns: x - y.

```
template<> struct minus<void> {
    template<class T, class U> constexpr auto operator()(T&& t, U&& u) const
        -> decltype(std::forward<T>(t) - std::forward<U>(u));
    using is_transparent = unspecified;
};
```

```
template<class T, class U> constexpr auto operator()(T&& t, U&& u) const
    -> decltype(std::forward<T>(t) - std::forward<U>(u));
```

Returns: std::forward<T>(t) - std::forward<U>(u).

# 20.14.7.4 Class template multiplies [arithmetic.operations.multiplies]

```
template<class T = void> struct multiplies {
    constexpr T operator()(const T& x, const T& y) const;
};
```

```
constexpr T operator()(const T& x, const T& y) const;
```

Returns: x * y.

```
template<> struct multiplies<void> {
    template<class T, class U> constexpr auto operator()(T&& t, U&& u) const
        -> decltype(std::forward<T>(t) * std::forward<U>(u));
    using is_transparent = unspecified;
};
```

```
template<class T, class U> constexpr auto operator()(T&& t, U&& u) const
    -> decltype(std::forward<T>(t) * std::forward<U>(u));
```

Returns: std::forward<T>(t) * std::forward<U>(u).

# 20.14.7.5 Class template divides [arithmetic.operations.divides]

```
template<class T = void> struct divides {
    constexpr T operator()(const T& x, const T& y) const;
};
```

```
constexpr T operator()(const T& x, const T& y) const;
```

Returns: x / y.

```
template<> struct divides<void> {
    template<class T, class U> constexpr auto operator()(T&& t, U&& u) const
        -> decltype(std::forward<T>(t) / std::forward<U>(u));
    using is_transparent = unspecified;
};
```

```
template<class T, class U> constexpr auto operator()(T&& t, U&& u) const
    -> decltype(std::forward<T>(t) / std::forward<U>(u));
```

Returns: std::forward<T>(t) / std::forward<U>(u).

# 20.14.7.6 Class template modulus [arithmetic.operations.modulus]

```
template<class T = void> struct modulus {
    constexpr T operator()(const T& x, const T& y) const;
```