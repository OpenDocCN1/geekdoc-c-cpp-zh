# ISO/IEC 14882:2020(E)

Remarks: Specializations of this function template for which *x == *y is a core constant expression are constexpr functions.

```
template<class T, class U> constexpr bool operator!=(const optional<T>& x, const optional<U>& y);
```

Mandates: The expression *x != *y is well-formed and its result is convertible to bool.

Returns: If bool(x) != bool(y), true; otherwise, if bool(x) == false, false; otherwise *x != *y.

Remarks: Specializations of this function template for which *x != *y is a core constant expression are constexpr functions.

```
template<class T, class U> constexpr bool operator<(const optional<T>& x, const optional<U>& y);
```

Mandates: *x < *y is well-formed and its result is convertible to bool.

Returns: If !y, false; otherwise, if !x, true; otherwise *x < *y.

Remarks: Specializations of this function template for which *x < *y is a core constant expression are constexpr functions.

```
template<class T, class U> constexpr bool operator>(const optional<T>& x, const optional<U>& y);
```

Mandates: The expression *x > *y is well-formed and its result is convertible to bool.

Returns: If !x, false; otherwise, if !y, true; otherwise *x > *y.

Remarks: Specializations of this function template for which *x > *y is a core constant expression are constexpr functions.

```
template<class T, class U> constexpr bool operator<=(const optional<T>& x, const optional<U>& y);
```

Mandates: The expression *x <= *y is well-formed and its result is convertible to bool.

Returns: If !x, true; otherwise, if !y, false; otherwise *x <= *y.

Remarks: Specializations of this function template for which *x <= *y is a core constant expression are constexpr functions.

```
template<class T, class U> constexpr bool operator>=(const optional<T>& x, const optional<U>& y);
```

Mandates: The expression *x >= *y is well-formed and its result is convertible to bool.

Returns: If !y, true; otherwise, if !x, false; otherwise *x >= *y.

# 20.6.7 Comparison with nullopt [optional.nullops]

```
template<class T> constexpr bool operator==(const optional<T>& x, nullopt_t) noexcept;
```

Returns: !x.

```
template<class T> constexpr strong_ordering operator<=>(const optional<T>& x, nullopt_t) noexcept;
```

Returns: bool(x) <=> false.

# 20.6.8 Comparison with T [optional.comp.with.t]

```
template<class T, class U> constexpr bool operator==(const optional<T>& x, const U& v);
```

Mandates: The expression *x == v is well-formed and its result is convertible to bool.