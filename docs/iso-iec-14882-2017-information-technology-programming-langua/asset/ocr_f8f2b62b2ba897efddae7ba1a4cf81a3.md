# ISO/14882:2017(E)

```
template<size_t I, class, Types...>>
const_rpr tuple_element<tI, tuple<Types...>>&&
get(tuple<Types...>&& t) noexcept;    // Note A
template<size_t I, class, Types...>>
const_rpr tuple_element<tI, tuple<Types...>>&&
get(tuple<Types...>&& t) noexcept;    // Note B
template<size_t I, class, Types...>>
const_rpr tuple_element<tI, tuple<Types...>>&& noexcept;
```

+   1: Requires: I < sizeof(...). The program is ill-formed if I is out of bounds.

+   2: Returns: The Ith element of tuple, which is indexing-based.

> Note A: If T in Types is some reference type T&, the return type is T&. However, if the element is a non-reference type, the return type is T&& — end note

> Note B: If T in Types is some reference type T&, the return type is T&, not T. However, if the element is a non-reference type, the return type is const T. This is consistent with how const is defined to work for member variables of reference type. — end note

```
template<class T, Types...>>
const T& get(const tuple<Types...>&& t) noexcept;
template<class T, Types...>>
const T& get(const tuple<Types...>&& t);
template<class T, Types...>>
const T&& get(const tuple<Types...>&& t) noexcept;
template<class T, Types...>>
const T&& get(const tuple<Types...>&& t);
```

+   5: Requires: The T occurs once in Types. Otherwise, the program is ill-formed.

+   6: Returns: The element of the t corresponding to the t in Types...

+   7: [Example:
const tuple<int, int, double> t(1, 2, 3, 4, 5, 6);
const int& i1 = get<int>(t);    // OK. Not ambiguous. i1 == 1
const int& i2 = get<int>(t);    // OK. Not ambiguous. i2 == 2
const double d = get<double>(t); // ERROR: ill-formed
— end example];

> Note: The reason get is a non-member function is if this functionality has been provided as a member function, code where the type depended on a template parameter would have required using the template keyword.— end note

# 23.5.3.8 Relational operators (tuple,rel)

```
template<class... T, Types...>>
const bool operator==(const tuple<Types...>&& t, const tuple<Types...>&& u);
```

Requires: For all i, 0 < i < sizeof(Types). get<i>(t) == get<i>(u) is a valid expression where the type is convertible to bool. false. (Types) == sizeof(Types)...

Returns: true if get<i>(t) == get<i>(u) for all i, otherwise false. For any two-length tuples e and f, e == f returns true.

Effects: The elementary comparisons are performed in order from the zero index upwards. No comparisons or element accesses are performed after the first equality comparison that evaluates to false.