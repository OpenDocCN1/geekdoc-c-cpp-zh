# ISO/IEC 14882:2017(E)

```
template <> struct less_equal<void> {
template <class T, class U> constexpr auto operator()(T&& t, U& u) const
-> dectype(std::forward<T>(t) <= std::forward<U>(u));
```

```
using is_transparent = unspecified;
;
```

```
template <class T, class U> constexpr auto operator()(T&& t, U& u) const
-> dectype(std::forward<T>(t) <= std::forward<U>(u));
```

```
Returns: std::forward<T>(t) <= std::forward<U>(u).
```

# 23.14.8 Logical operations

+   1. The library provides basic function classes for all of the logical operations in the language (8.14, 15.8.3).

# 23.14.8.1 Class template logical_and

```
template <class T = void> struct logical_and {
constexpr bool operator()(const T& x, const T& y) const;
;
```

```
constexpr bool operator()(const T& x, const T& y) const;
```

```
Returns: x && y.
```

```
template <> struct logical_and<void> {
template <class T, class U> constexpr auto operator()(T&& t, U& u) const
-> dectype(std::forward<T>(t) && std::forward<U>(u));
```

```
using is_transparent = unspecified;
```

```
template <class T, class U> constexpr auto operator()(T&& t, U& u) const
-> dectype(std::forward<T>(t) && std::forward<U>(u));
```

```
Returns: std::forward<T>(t) && std::forward<U>(u).
```

# 23.14.8.2 Class template logical_or

```
template <class T = void> struct logical_or {
constexpr bool operator()(const T& x, const T& y) const;
;
```

```
constexpr bool operator()(const T& x, const T& y) const;
```

```
Returns: x || y.
```

```
template <> struct logical_or<void> {
template <class T, class U> constexpr auto operator()(T&& t, U& u) const
-> dectype(std::forward<T>(t) || std::forward<U>(u));
```

```
using is_transparent = unspecified;
```

```
template <class T, class U> constexpr auto operator()(T&& t, U& u) const
-> dectype(std::forward<T>(t) || std::forward<U>(u));
```

```
Returns: std::forward<T>(t) || std::forward<U>(u).
```