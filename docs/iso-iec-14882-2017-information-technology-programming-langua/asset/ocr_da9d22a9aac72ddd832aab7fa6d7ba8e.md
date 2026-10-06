# ISO/IEC 14882:2017(E)

2 The default move and copy constructor, respectively, of pair shall be constexpr function if and only if all required element-wise initializations for copy and move, satisfy the requirements for a constexpr function. The destructor of pair shall be a trivial destructor if (is_trivially_destructible_-v<T1> && is_trivially_destructible_v<T2>) is true.

```
constexpr pair();
```

3 Effects: Value-initializes first and second.
4 Remarks: This constructor shall not participate in overloads resolution unless is_default_constructible_v<second_type> is true. [Note: This behavior can be implemented by a constructor template argument. — The constructor is explicit if and only if either first_type or second_type is not implicitly default-constructible. [Note: This behavior can be implemented with a trait that checks whether a first_type or second_type can be initialized with {}. — end note]

```
constexpr pair(const T1& x, const T2 y);
```

5 Effects: Initializes first and second with y.
6 Remarks: This constructor shall not participate in overloads resolution unless is_copy_constructible_v<first_type> is true and is_constructible_v<second_type> is true. The constructor is explicit if and only if is_convertible_v<second_type, first_type> is false or is_convertible_v<second_type, second_type> is false.

```
template<class U1, class U2> constexpr pair(forward<U1> x, forward<U2> y);
```

7 Effects: Initializes first and second with x.
8 Remarks: This constructor shall not participate in overloads resolution unless is_constructible_v<first_type> is true and is_constructible_v<second_type, U2&> is true. The constructor is explicit if and only if is_convertible_v<U1, first_type> is false or is_convertible_v<U2&, second_type> is false.

```
template<class U1, class U2> constexpr pair(const U1& p, U2& q);
```

9 Effects: Initializes from the corresponding members of the argument.
10 Remarks: This constructor shall not participate in overloads resolution unless is_constructible_v<first_type> is true and is_constructible_v<second_type, U2&> is true. The constructor is explicit if and only if is_convertible_v<U1, first_type> is false or is_convertible_v<U2&, second_type> is false.

```
template<class U1, class U2> constexpr pair(pair<U1, U2>&& p);
```

11 Effects: Initializes first with std::forward<U1>(p.first) and second with std::forward<U2>(p.second).
12 Remarks: This constructor shall not participate in overloads resolution unless is_constructible_v<first_type> is true and is_constructible_v<second_type, U2&> is true. The constructor is explicit if and only if is_convertible_v<U1, first_type> is false or is_convertible_v<U2&, second_type> is false.

```
template<class... Args> pair(piecewise_construct<T
```

13 Requires: is_constructible_v<first_type, Args1&&...> is true and is_constructible_v<second_type, Args2&&...> is true.
14 Effects: Initializes first with arguments of types Args1... obtained by the elements of