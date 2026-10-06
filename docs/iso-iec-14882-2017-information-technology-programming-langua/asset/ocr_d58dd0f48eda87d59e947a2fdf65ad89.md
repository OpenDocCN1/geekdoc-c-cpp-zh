# ISO/IEC 14882:2017(E)

```
template <class T1, class T2>
constexpr bool operator<(const pair<T1, T2>& x, const pair<T1, T2>& y);
```

2 RETURNS: x.first < y.first || !(y.first < x.first && x.second < y.second).

```
template <class T1, class T2>
constexpr bool operator!const pair<T1, T2>& x, const pair<T1, T2>& y);
```

3 RETURNS: !(x == y).

```
template <class T1, class T2>
constexpr bool operator>(const pair<T1, T2>& x, const pair<T1, T2>& y);
```

4 RETURNS: y < x.

```
template <class T1, class T2>
constexpr bool operator<=(const pair<T1, T2>& x, const pair<T1, T2>& y);
```

5 RETURNS: !(x < y).

```
template<class T1, class T2> void swap(pair<T1, T2>& x, pair<T1, T2>& y);
```

6 noexcept(except(x.swap(y)));

7 Effects: As if x.swap(y).

8 Remarks: This function shall not participate in overload resolution unless is_swappable_y<T1> is true and is_swappable_y<T2> is true.

```
template <class T1, class T2>
constexpr pair<V1, V2> make_pair(T1&& x, T2&& y, std::forward<T1>(x), std::forward<T2>(y));
```

9 RETURNS: pair<V1, V2>(std::forward<T1>(x), std::forward<T2>(y)), where V1 and V2 are determined as follows: Let Ui be decay_t<Ti> for each Ti. If Ui is a specialization of reference_wrapper, then Vi is Ui::::element_type; otherwise Vi is Ui.

10 [Example: In place of:

```
return pair<int, double>(5, 3.1415926); // explicit types
a C++ program may have:
return make_pair(5, 3.1415926); // types are deduced
// end example ]
```

# 23.4.4 Tuple-like access to pair

```
template <class T1, class T2>
struct tuple_size<pair<T1, T2>> : int_constant<size_t, 2> {};
```

```
tuple_element<0, pair<T1, T2>>::type
```

1 Value: The type T1.

```
tuple_element<1, pair<T1, T2>>::type
```

2 Value: The type T2.